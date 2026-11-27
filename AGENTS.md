# GrannySwift

Swift project.

- `swift build` lints through the SwiftLint build plugin (errors fail the build). Before reporting a Swift change done, run `swift build`, `swift test` and `swiftlint --strict`; CI runs the same three on macOS.
- `.agents/checks.json` names the post-edit Swift build and lint checks; keep them at zero errors.
- This repository is public. Keep personal data, credentials and private notes out of every commit. GrannySwift is a Swift-first redesign around reliable upstream packages and native Apple frameworks; earlier private scripts serve only as a behaviour reference, and all test fixtures use invented data.
- Repository skills live in `.agents/skills/<name>/`, each with a tracked symlink at `.claude/skills/<name>` unless noted below. The five Apple SwiftUI, testing, device and Instruments skills come unedited from Xcode's bundle. For repository settings, collaboration files or security setup, use the `repository-management` skill.
- `skills/` holds the skills this repository ships (`skills/photos/` today), kept outside `.agents/skills/` so project discovery does not load them a second time. How shipped skills are installed across agents is still open.
- Apple Notes is served in Claude Code by the vendor's `apple-notes` plugin from the `sweetrb/apple-notes-mcp` marketplace (enabled in `.claude/settings.json` with marketplace auto-update on; install once per machine with `claude plugin marketplace add sweetrb/apple-notes-mcp` and `claude plugin install apple-notes@apple-notes-mcp --scope project`). For other coding agents, `.agents/skills/apple-notes/` carries an unedited copy of the vendor's skill (with no `.claude/skills/` link) and `.agents/mcp_config.json` provides the server entry; any per-machine config file stays untracked.
