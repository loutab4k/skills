---
name: owner-procedure
description: Rehearse a multi-step procedure yourself before handing it to the owner to run. Use before giving the owner commands, a runbook, a setup, a migration or a fix to carry out.
---

# Owner procedure

The owner runs only what you have already run. Every step you hand over is either **rehearsed** (you ran it where it will run and attach its output) or **marked** (`not run: <reason>`). A procedure that was only written is a guess, and the owner becomes the one who finds its mistakes.

If a `BINDINGS.md` sits next to this file, read it first: it names this host's files, checks and tools for this skill.

## Steps

1. **Write it as the owner will run it.** One fenced block per machine and directory, complete commands, no placeholders you could fill yourself. Name the shell: the owner's Mac terminal is `/bin/zsh` (your Claude shell there is Homebrew bash); from the Mac, reach a server by its SSH alias (`grep '^Host' ~/.ssh/config` lists the aliases).
2. **Rehearse each step where it will run.** Pick the place by what the step changes:
   - Reads, and changes the owner already approved on that machine: run it on the target with the owner's shell. On the Mac that is `env -i HOME="$HOME" USER="$USER" TERM=xterm-256color /bin/zsh -ilc '…'`: a clean environment, and an interactive login shell that reads `.zshrc`, where Homebrew and mise set `PATH` (`/bin/zsh -lc` skips `.zshrc` and keeps your own `PATH`, so it finds Homebrew's `node` where the owner's terminal runs mise's). For a remote script, write it to the scratchpad and run `ssh <alias> bash -s < <script>`.
   - Anything else on Linux: a disposable OrbStack container from the target's image (`docker run --rm -i <image> bash -s < <script>`), or a disposable machine when the step needs systemd or a full OS (`orbctl create --isolated <distro> <name>`, which shares no files with the Mac and has no integration, then `orbctl delete -f <name>`).
   - A Mac step that writes only under `$HOME` (dotfiles, a CLI's config files): a throwaway home (`HOME="$(mktemp -d)"`), then the real target only with the owner's approval. A throwaway home does not isolate `defaults` (cfprefsd writes the real preferences; `HOME=<tmp> defaults read com.apple.dock orientation` prints the real value), Homebrew (`/opt/homebrew`), `launchctl`, `sudo` or any absolute path outside `$HOME`: such a step runs its tool's dry run (`brew install --dry-run`, `brew bundle check`) or is marked `not run: writes the real Mac, needs the owner's yes`.

   Run the steps in order, from the state the owner starts in, so a missing tool, PATH entry or earlier step shows up as it would for them. Done when every step has run or been marked.
3. **Mark what you cannot run.** For each step write `not run: <reason>` with the reason: a password or `sudo` prompt, a GUI or browser step, a secret only the owner holds, a production or irreversible write that needs their per-action yes. Add what the owner should see when it works (an exit code, a line of output, a state to check).
4. **Hand it over** with the procedure, the rehearsal output (each step's command, exit code and the lines that prove it; long output in a `<details>` block) and the list of marked steps. Stop the containers and machines you started before you reply.

## Gotchas the rehearsal catches

- `ssh host cmd` reads the caller's stdin: a loop or a later command loses its input. Use `ssh -n` for a single command, `bash -s < <script>` for a script.
- A non-login or remote shell has a different `PATH` (`gh`, Homebrew and mise tools missing): rehearse in the shell the owner uses.
- A Mac may run OrbStack or Docker Desktop: check `docker context show` before naming either.
- A workflow or script input that the owner types (a GitHub `workflow_dispatch` input, a prompt) needs a rehearsal with the exact value and type they will give.
