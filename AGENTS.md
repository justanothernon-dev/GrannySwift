# GrannySwift

Swift project. This file holds only instructions specific to this repository; `CLAUDE.md` is a symlink to it, so Claude Code and Codex read the same text.

- Swift code intelligence comes from the `swift-lsp` Claude Code plugin (Apple's `sourcekit-lsp` from the Xcode toolchain). Read its diagnostics after each Swift edit and use definition/reference lookups before changing a shared symbol.
- `swift build` lints through the SwiftLint build plugin (errors fail the build). Before reporting a Swift change done, run `swift build`, `swift test` and `swiftlint --strict`; CI runs the same three on macOS.
- This repository is public. Keep personal data, credentials and private notes out of every commit. GrannySwift rewrites the private `applesuite` commands in Swift: port its code, and replace its real-message, contact and calendar fixtures with invented ones.
- Repository skills live in `.agents/skills/<name>/`, each with a tracked symlink at `.claude/skills/<name>`. For repository settings, collaboration files or security setup, use the `repository-management` skill.
- `skills/photos/` is the `photos` skill this repository ships, meant to be linked globally from here. It stays outside `.agents/skills/` (project discovery) so this repository does not load it a second time.
- `.agents/skills/apple-notes/` is the vendor skill from sweetrb/apple-notes-mcp, paired with the `apple-notes` server in `.mcp.json`, which starts the applesuite launcher instead of the vendor's `npx` command because desktop-app sessions have no `node` on PATH and the launcher finds it; it works only on a Mac with applesuite installed. The skill stays as the vendor ships it; refresh it with `npx skills add sweetrb/apple-notes-mcp --skill apple-notes`.
