# Product contracts: UI, client state, HTTP API, Telegram

What users and clients see: interface copy and feedback, client state, the wire contract, and the Telegram platform's own rules. Read it when you design or review a UI flow, a bot flow, an API endpoint or its errors.

Entry format and precedence: [SKILL.md](SKILL.md).

## Apple: Human Interface Guidelines and Swift API Design Guidelines

Motion, materials and typography are in the `emilkowalski-apple-design` skill; this covers the rest.

- **Write labels as actions and errors as fixes.** Put an error next to the problem, do not blame, and state what to do ("use at least 8 characters", not "too short"). Supports: no owner rule; advisory. [Writing][hig-w]
- **Match feedback to its weight.** Status stays passive; interrupt only for things like data loss. All feedback must be accessible. Supports: no owner rule; advisory. [Feedback][hig-f]
- **Show something as soon as possible.** Say that content is loading and how long it may take. Supports: no owner rule; advisory. [Loading][hig-l]
- **Onboarding is fast, optional and hands-on.** People learn by doing the task. Supports: no owner rule; advisory. [Onboarding][hig-o]
- **Never carry meaning by colour alone; meet contrast minimums.** Supports: no owner rule; advisory. [Accessibility][hig-a]
- **Clarity at the point of use.** Omit needless words; name a value by its role, not its type. This applies to Go, TypeScript and OpenAPI names too. Supports: no owner rule; advisory. [Swift guidelines][swift], [roles][swift-roles]

## React docs: state

- **Compute derived data during render.** Do not copy it into state and sync it with an Effect. Supports: engineering.md › Invariants 2 (derived data stays consistent with its one source). [You might not need an Effect][re-eff]
- **No contradictory or redundant state.** Replace flags that can disagree with one status value. Supports: engineering.md › Design (make invalid states unrepresentable). [state structure][re-st]
- **Reducers are pure; one action is one user interaction.** Supports: engineering.md › Invariants 3 (presentation only displays; logic lives elsewhere). [writing reducers][re-red]

## Google API Improvement Proposals

- **A client-supplied request ID makes a mutating call safe to retry.** A repeat returns the first result, or the current state if that result is gone. Supports: no owner rule; advisory. [AIP-155][aip155]
- **Errors carry a stable machine reason and a human message that says how to fix it.** The reason is short UPPER_SNAKE_CASE, unique in its domain; dynamic values go in metadata. Supports: engineering.md › Design (keep error causes). [AIP-193 ErrorInfo][aip193], [messages][aip193m]
- **Page tokens are opaque; paginate list calls from day one.** Adding pagination later breaks existing clients. Supports: no owner rule; advisory. [AIP-158][aip158]
- **Old clients keep working against new servers.** No new required fields; changed defaults and formats are breaking too. Supports: engineering.md › Invariants 2 (a shared contract evolves as a whole). [AIP-180][aip180]

## Telegram: Bot API, Mini Apps, TDLib

- **Long polling is at-least-once.** An update is confirmed when `getUpdates` is called with a higher offset, so advance the offset only after handling, and make handlers idempotent. The second half is our inference. Supports: no owner rule; advisory. [getUpdates][tg-upd]
- **Authenticate webhooks.** Set `secret_token` and check the `X-Telegram-Bot-Api-Secret-Token` header on every request. Supports: core.md › Engineering (check a fact once at its boundary). [setWebhook][tg-wh]
- **Obey flood control.** Wait `retry_after` seconds after a 429; send about one message per second per chat. Supports: no owner rule; advisory. [ResponseParameters][tg-rp], [limits][tg-faq]
- **Validate Mini App `initData` on the server.** Check its HMAC-SHA-256 hash and `auth_date`; never trust `initDataUnsafe`. Supports: engineering.md › Invariants 3 (authorization runs on a trusted server). [validation][tg-init]
- **One schema generates every binding.** TDLib builds its C++, C, Java and JSON interfaces from `td_api.tl`. Supports: engineering.md › Invariants 2 (a schema has one source). [td_api.tl][td-tl], [generator][td-gen]

[hig-w]: https://developer.apple.com/design/human-interface-guidelines/writing
[hig-f]: https://developer.apple.com/design/human-interface-guidelines/feedback
[hig-l]: https://developer.apple.com/design/human-interface-guidelines/loading
[hig-o]: https://developer.apple.com/design/human-interface-guidelines/onboarding
[hig-a]: https://developer.apple.com/design/human-interface-guidelines/accessibility
[swift]: https://github.com/swiftlang/swift-org-website/blob/02efa9a/documentation/api-design-guidelines/index.md#L51
[swift-roles]: https://github.com/swiftlang/swift-org-website/blob/02efa9a/documentation/api-design-guidelines/index.md#L267
[re-eff]: https://github.com/reactjs/react.dev/blob/046f17d/src/content/learn/you-might-not-need-an-effect.md#L22
[re-st]: https://github.com/reactjs/react.dev/blob/046f17d/src/content/learn/choosing-the-state-structure.md#L104
[re-red]: https://github.com/reactjs/react.dev/blob/046f17d/src/content/learn/extracting-state-logic-into-a-reducer.md#L879
[aip155]: https://github.com/aip-dev/google.aip.dev/blob/2ccc61a/aip/general/0155.md
[aip193]: https://github.com/aip-dev/google.aip.dev/blob/2ccc61a/aip/general/0193.md#L90
[aip193m]: https://github.com/aip-dev/google.aip.dev/blob/2ccc61a/aip/general/0193.md#L234
[aip158]: https://github.com/aip-dev/google.aip.dev/blob/2ccc61a/aip/general/0158.md#L118-L158
[aip180]: https://github.com/aip-dev/google.aip.dev/blob/2ccc61a/aip/general/0180.md
[tg-upd]: https://core.telegram.org/bots/api#getupdates
[tg-wh]: https://core.telegram.org/bots/api#setwebhook
[tg-rp]: https://core.telegram.org/bots/api#responseparameters
[tg-faq]: https://core.telegram.org/bots/faq#my-bot-is-hitting-limits-how-do-i-avoid-this
[tg-init]: https://core.telegram.org/bots/webapps#validating-data-received-via-the-mini-app
[td-tl]: https://github.com/tdlib/td/blob/a94b83d/td/generate/scheme/td_api.tl
[td-gen]: https://github.com/tdlib/td/blob/a94b83d/td/generate/CMakeLists.txt#L115-L172
