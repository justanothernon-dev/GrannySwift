# Third-Party Notices

GrannySwift is licensed under the MIT License (see [LICENSE](LICENSE)). This file tracks attribution and license notices for third-party packages and vendored agent skills used or distributed by this repository.

## Swift Package Dependencies

- **swift-argument-parser** (`https://github.com/apple/swift-argument-parser`) — Apache License 2.0 with Runtime Library Exception.
- **SwiftLintPlugins** (`https://github.com/SimplyDanny/SwiftLintPlugins`) — MIT License (build-time plugin; not linked into compiled binaries).

## Vendored and Adapted Repository Skills

- **`.agents/skills/apple-notes/`** — Unedited skill from `sweetrb/apple-notes-mcp` (`https://github.com/sweetrb/apple-notes-mcp`), MIT License (full notice retained in `.agents/skills/apple-notes/LICENSE`).
- **`.agents/skills/repository-management/`** — Adapted from GitHub's *Introduction to Repository Management* (`https://github.com/skills/introduction-to-repository-management`), MIT License, © 2025 GitHub Skills.

## Release Attribution Policy

Whenever a compiled release links an upstream library or metadata bundle under Apache-2.0 (without Swift's Runtime Library Exception), BSD, or MIT, add its license text and upstream `NOTICE` entries to this file before distributing binaries.
