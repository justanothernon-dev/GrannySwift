# GrannySwift

Swift project. This file holds only instructions specific to this repository; `CLAUDE.md` is a symlink to it, so Claude Code and Codex read the same text.

- Swift code intelligence comes from the `swift-lsp` Claude Code plugin (Apple's `sourcekit-lsp` from the Xcode toolchain). Read its diagnostics after each Swift edit and use definition/reference lookups before changing a shared symbol.
- `swift build` lints through the SwiftLint build plugin (errors fail the build). Before reporting a Swift change done, run `swift build`, `swift test` and `swiftlint --strict`; CI runs the same three on macOS.
- This repository is public. Keep personal data, credentials and private notes out of every commit. GrannySwift rewrites the private `applesuite` commands in Swift: port its code, and replace its real-message, contact and calendar fixtures with invented ones.
- Repository skills live in `.agents/skills/<name>/`, each with a tracked symlink at `.claude/skills/<name>`. For repository settings, collaboration files or security setup, use the `repository-management` skill.
- `skills/photos/` is the `photos` skill this repository ships, meant to be linked globally from here. It stays outside `.agents/skills/` (project discovery) so this repository does not load it a second time.
- Apple Notes comes from the vendor's Claude Code plugin (`apple-notes` from the `sweetrb/apple-notes-mcp` marketplace), which `.claude/settings.json` enables for this repository with marketplace auto-update on; the plugin supplies both the `apple-notes` server and skill, so this repository carries neither. It needs macOS and Node 20 or newer on the PATH of the app that launches Claude Code. Each machine installs it once: `claude plugin marketplace add sweetrb/apple-notes-mcp`, then `claude plugin install apple-notes@apple-notes-mcp --scope project`.
