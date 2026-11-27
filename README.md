# GrannySwift

An agent-first, Swift-first macOS and Apple integration layer for people and coding agents, built on reliable open-source packages and native Apple frameworks with System Integrity Protection left enabled.

## Where it stands

The repository currently holds the Swift Package Manager scaffold (`granny` and `GrannyCore`), macOS CI (`swift build`, `swift test`, and `swiftlint --strict`), post-edit checks, project skills, and the `photos` skill. Component designs and upstream package selections are being mapped before implementation.

## Development

Build, test, and lint from the repository root on macOS:

```bash
swift build
swift test
swift package plugin --allow-writing-to-package-directory swiftlint --strict
```

See [AGENTS.md](AGENTS.md) for repository conventions and agent setup.
