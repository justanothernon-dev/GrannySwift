# GrannySwift

An agent-first, Swift-first macOS and Apple integration layer for people and coding agents, built on reliable open-source packages and native Apple frameworks with System Integrity Protection left enabled.

## Where it stands

The repository currently holds the Swift Package Manager scaffold (`granny` and `GrannyCore`), macOS CI (`swift build`, `swift test`, and `swiftlint --strict`), post-edit checks, repository and Apple Notes skills, and the `photos` skill. Component designs and upstream package selections are being mapped before implementation.

## Development

Build, test, and lint from the repository root on macOS:

```bash
swift build
swift test
swift package plugin --allow-writing-to-package-directory swiftlint --strict
```

Optional local Xcode agent skills (`swiftui-specialist`, `swiftui-whats-new-27`, `device-interaction`, `modernize-tests`, `xctrace`) are intentionally excluded from git under Apple's Xcode license; export them locally on macOS with `xcrun agent skills export --output-dir <dir>` and copy any you want into `.agents/skills/` (with symlinks in `.claude/skills/`).

## License

Licensed under the [MIT License](LICENSE). See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) for third-party dependency and skill notices.

See [AGENTS.md](AGENTS.md) for repository conventions and agent setup.
