# GrannySwift

Swift project. This file holds only instructions specific to this repository; `CLAUDE.md` is a symlink to it, so Claude Code and Codex read the same text.

- Swift code intelligence comes from the `swift-lsp` Claude Code plugin (Apple's `sourcekit-lsp` from the Xcode toolchain). Read its diagnostics after each Swift edit and use definition/reference lookups before changing a shared symbol.
- `swift build` lints through the SwiftLint build plugin (errors fail the build). Before reporting a Swift change done, run `swift build`, `swift test` and `swiftlint --strict`; CI runs the same three on macOS.
- This repository is public. Keep personal data, credentials and private notes out of every commit. GrannySwift rewrites the private `applesuite` commands in Swift: port its code, and replace its real-message, contact and calendar fixtures with invented ones. Do not inherit ambient secrets into build plugins or subprocesses. Pull request and commit text is public too: no conversation excerpts, personal names or details, private repository links or sensitive examples.
- Repository skills live in `.agents/skills/<name>/`, each with a tracked symlink at `.claude/skills/<name>`. For repository settings, collaboration files or security setup, use the `repository-management` skill.
