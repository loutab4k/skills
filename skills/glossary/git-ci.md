# Git and CI vocabulary

Words for asking an agent to change history, integrate a branch, gate a merge or cut a release, precisely enough that the permission rules apply to the right action.

## Language

### Undoing changes

Sources: https://git-scm.com/docs/git-revert, https://git-scm.com/docs/git-reset, https://git-scm.com/docs/git-push

**Revert**:
A new commit that applies the inverse of an earlier commit, leaving history intact. Reverting a merge commit needs `-m` and makes Git treat that merge's changes as unwanted in later merges of the same branch.
_Avoid_: undo, roll back, reset

**Reset**:
Moving the current branch ref to another commit. `--soft` keeps index and files, `--mixed` (default) resets the index and keeps files, `--hard` resets both and discards uncommitted work, and `--keep` keeps local edits but aborts when one is in a file that differs between the two commits.
_Avoid_: revert, rollback, undo commit

**Restore**:
Rewriting files in the working tree or index from a commit without moving any branch.
_Avoid_: checkout (for files), revert, reset

**Rollback**:
Returning a deployed system to a previous release or config. It is an operations action, not a Git command, and is often done by deploying an earlier tag. Not the same as reverting the code on main.
_Avoid_: revert, roll back main, downgrade

**Roll forward**:
Fixing a bad deployment by shipping a new release with the fix instead of returning to the old one.
_Avoid_: hotfix (a hotfix is the change; roll forward is the strategy), fix forward

**Amend**:
Replacing the last commit with a new one that has changed content or message. It rewrites that commit's SHA.
_Avoid_: edit commit, fixup (a fixup is a separate commit meant for autosquash)

**Force push**:
A push that replaces the remote branch even when it is not an ancestor of the new tip, discarding remote commits. Needs separate explicit permission.
_Avoid_: overwrite push, push -f (as a casual synonym)

**Force-with-lease**:
A force push that succeeds only if the remote ref still equals what you last fetched or an explicit expected SHA. A background fetch can defeat the implicit form; `--force-if-includes` or an explicit `<ref>:<sha>` closes that hole.
_Avoid_: safe force push, force push (when the lease is meant)

**Reflog**:
The local, per-repository log of where each ref and HEAD pointed. It is the recovery path after a reset or rebase, and is never pushed.
_Avoid_: history, git log

### History shapes and integration

Sources: https://git-scm.com/docs/git-merge; GitHub merge methods: https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/about-merge-methods-on-github; Forgejo merge styles: `MergeStyle*` in https://codeberg.org/forgejo/forgejo/raw/branch/forgejo/models/repo/repo_unit.go and https://forgejo.org/docs/latest/user/repository/merge-message-templates/

**Merge base**:
The common ancestor commit from which a three-way merge compares both sides (`git merge-base`).
_Avoid_: fork point (a different, reflog-based notion), branch point, base (unqualified)

**Base branch**:
The branch a PR merges into. The **head branch** is the PR's own branch.
_Avoid_: target branch, main (when the base is something else), upstream

**Fast-forward**:
Moving a branch ref forward to a descendant commit, which is possible when the branch tip is an ancestor of it. No new commit and no rewritten SHAs.
_Avoid_: linear merge, rebase merge

**Merge commit**:
A commit with two or more parents that joins diverged histories. `--no-ff` forces one even when a fast-forward is possible. GitHub's "Create a merge commit" method.
_Avoid_: true merge, merge (unqualified, when the method matters)

**Squash merge**:
Landing a PR as one new commit containing its combined change. The PR's individual commits, SHAs and timestamps do not reach the base branch. The owner's default method.
_Avoid_: squash (as a verb for local `rebase -i` fixups), squash and rebase

**Rebase merge**:
Landing each PR commit on the base branch as a replayed commit with a new SHA and updated committer, without a merge commit. The result looks like a fast-forward but is not one. On GitHub it drops originally empty commits and leaves commits unsigned.
_Avoid_: fast-forward merge, rebase (unqualified)

**Semi-linear merge**:
Rebasing the PR onto the base and then adding a merge commit, giving linear commits plus a merge marker. Forgejo's `rebase-merge` style; GitHub has no equivalent.
_Avoid_: rebase-merge (ambiguous with rebase merge), merge with rebase

**Fast-forward-only merge**:
A PR merge that is refused unless the base can be fast-forwarded to the PR head, preserving the PR's exact SHAs. Forgejo offers it as a merge style; GitHub's UI does not.
_Avoid_: rebase merge, ff merge

**Linear history**:
A branch history without merge commits. GitHub's "Require linear history" enforces it by allowing only squash and rebase merges.
_Avoid_: clean history, flat history

**Rebase**:
Replaying a branch's commits onto a new base, producing new SHAs. Updating a PR this way requires a force-with-lease push.
_Avoid_: rebase merge (the platform method), sync, update

**Cherry-pick**:
Applying the change of one existing commit as a new commit on another branch.
_Avoid_: backport (a backport is the purpose; cherry-pick is the mechanism), copy commit

**Stacked PRs**:
A chain of PRs where each PR's base branch is the previous PR's head branch, reviewed and merged in order. In the owner's setup, made with `gh-stack` on GitHub only (`engineering.md`, Pull requests).
_Avoid_: dependent PRs, PR chain, stack (unqualified, it also means tech stack)

### Merge requirements

Sources: https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches, https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets, https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/collaborating-on-repositories-with-code-quality-features/about-status-checks; Forgejo fields: https://codeberg.org/forgejo/forgejo/raw/branch/forgejo/models/git/protected_branch.go

**Branch protection rule**:
A GitHub or Forgejo setting tied to a branch pattern that restricts pushes and merges, for example required reviews and checks or no force push. On GitHub only one rule applies to a branch.
_Avoid_: ruleset, protected branch (that is the branch, not the rule)

**Ruleset**:
GitHub's newer, layered form of branch and tag rules. Several can apply at once and the strictest wins; each has an enforcement status and a bypass list. GitHub Team and Enterprise plans per the docs; availability on Free and Pro for private repos not verified here.
_Avoid_: branch protection (when a ruleset is meant), policy

**Status check**:
A pass, fail or pending signal attached to a commit by CI or another service. GitHub has two kinds: **commit status** (simple, via the statuses API) and **check run** (rich, from a GitHub App such as Actions).
_Avoid_: CI (CI is the system; a check is one signal), test

**Required check**:
A status check that a branch protection rule or ruleset requires to succeed (success, skipped or neutral count) before a PR can merge. A repo with no rule has no required checks, whatever CI runs.
_Avoid_: required status check (fine, but shorter wins), gate, mandatory checks

**Gate**:
The owner's word for the full set of the project's checks that must pass before a push or merge, wherever it runs (locally, in a pre-push hook, in CI). Unlike a required check, a gate is enforced by the agent's procedure unless the platform also requires it.
_Avoid_: full gate, merge gate, quality gate, required checks (platform term); `merge-gate` stays the name of the owner's merge workflow

**Affected checks**:
The subset of the gate that the changed files can influence, run between fixes. Never a substitute for the gate before a push.
_Avoid_: changed checks, partial gate, quick check

**Base check**:
The check that the branch already contains the current tip of its base branch: an empty `git log HEAD..origin/<base>` after a fetch. A platform can enforce it too, as GitHub's strict status checks and Forgejo's outdated-branch block do.
_Avoid_: freshness check, up-to-date check, behind check; the `edit-freshness` hook checks single files, a different thing

**Stale approval**:
A review approval given before the PR's diff changed. GitHub's "Dismiss stale pull request approvals" and Forgejo's `DismissStaleApprovals` withdraw it.
_Avoid_: outdated review, old approval

**Auto-merge**:
A per-PR switch that makes the platform merge the PR once all required reviews and checks pass, without testing it against the latest base. GitHub needs the repo to allow it; Forgejo calls it "merge when checks succeed".
_Avoid_: merge queue, merge when green, `gh pr merge --auto` (the command, which merges at once when the PR is already mergeable, failing optional checks included)

**Merge queue**:
A platform-run queue that tests each PR combined with the latest base and the PRs ahead of it (a merge group on a temporary `gh-readonly-queue/<base>/...` branch) and merges only groups that pass. CI must trigger on `merge_group`. GitHub only; no Forgejo equivalent found.
_Avoid_: auto-merge, merge train (GitLab's name), bors

**Merge group**:
The combined commit a merge queue tests: the latest base plus the queued PRs ahead plus this PR.
_Avoid_: queue branch, batch

### CI

Source: https://docs.github.com/en/actions/get-started/understand-github-actions; Forgejo Actions is compatible in shape: https://forgejo.org/docs/latest/user/actions/overview/

**Workflow**:
A YAML-defined automated process in `.github/workflows/` (Forgejo also `.forgejo/workflows/`), made of jobs and triggered by events.
_Avoid_: pipeline (GitLab and Jenkins word), action, CI (for one file)

**Workflow run**:
One execution of a workflow for one event and commit. "CI is red" means a required workflow run failed.
_Avoid_: build, pipeline run, CI run (fine in speech; pick workflow run in writing)

**Job**:
A set of steps that runs on one runner. Jobs run in parallel unless one declares `needs`.
_Avoid_: stage, task

**Step**:
One shell command or one action inside a job, run in order on the job's runner.
_Avoid_: task, command

**Action**:
A reusable packaged unit a step calls with `uses:`, such as `actions/checkout`. Not the CI system as a whole.
_Avoid_: GitHub Actions (the product), plugin

**Reusable workflow**:
A whole workflow called from another workflow's job with `uses:` and inputs, such as the owner's merge-gate workflow.
_Avoid_: composite action (a step-level reuse), shared pipeline

**Runner**:
The machine or container that executes a job: GitHub-hosted or self-hosted. One job at a time per runner.
_Avoid_: agent, worker, executor

**Event**:
The repository activity that triggers a workflow, such as `push`, `pull_request` or `merge_group`.
_Avoid_: trigger (fine as a verb), hook

**Rerun**:
Executing an already finished workflow run or job again on the same commit. It is not a fix: a red-then-green rerun of the same commit suggests a flaky test.
_Avoid_: retry (test-level), restart

### Releases

Sources: https://semver.org/ (2.0.0), https://keepachangelog.com/en/1.1.0/, https://git-scm.com/docs/git-tag, https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases

**Version**:
A SemVer number MAJOR.MINOR.PATCH: MAJOR for incompatible changes to the public API, MINOR for compatible additions or deprecations, PATCH for compatible fixes. `0.y.z` promises no stability.
_Avoid_: release (the published artifact), build number

**Public API**:
What SemVer versions: the declared surface whose compatibility the version number promises. It must be stated somewhere for SemVer to mean anything.
_Avoid_: interface (in `mattpocock-codebase-design` that is a module's caller contract, at any scale)

**Breaking change**:
A change that requires some consumer of the public API to change, so it needs a MAJOR bump (or any bump under `0.y.z`).
_Avoid_: incompatible change, major change

**Pre-release version**:
A version with a hyphen suffix (`1.2.0-rc.1`) that sorts before the plain version and promises no stability.
_Avoid_: beta (one kind of pre-release), unstable release

**Build metadata**:
A plus suffix (`1.2.0+sha.5114f85`) that SemVer ignores when ordering versions.
_Avoid_: pre-release, version suffix

**Annotated tag**:
A tag object with tagger, date, message and optional signature: the kind for releases, and the kind `git describe` uses by default. A **lightweight tag** is a bare name for a commit, for private or temporary marks. A published tag is never moved; a fix gets a new version.
_Avoid_: tag (unqualified, when the kind matters), version tag, retag

**Release**:
A published version: on GitHub a release object built on a Git tag, with notes and assets. A tag alone is not a release.
_Avoid_: tag, deploy, version

**Changelog**:
A curated, human-readable file of notable changes per version, grouped as Added, Changed, Deprecated, Removed, Fixed and Security, with an `Unreleased` section at the top. It is not a git log dump.
_Avoid_: release notes (per-release prose, may be derived from it), commit log, history

**Yanked release**:
A published version withdrawn for a serious bug or security issue. It stays listed in the changelog marked `[YANKED]`, and the version is never reused.
_Avoid_: deleted release, unpublished, retracted

**Hotfix**:
An urgent fix to a released version, shipped as a PATCH release, sometimes from a release branch via cherry-pick.
_Avoid_: patch (the version part), quick fix, roll forward (the strategy)
