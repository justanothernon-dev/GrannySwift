# Sources and evidence boundaries

This is a navigation aid for implementation, not a fresh compatibility certification. The design capture comes from the owner's architecture discussion. Upstream links identify the implementations discussed; inspect and pin the relevant revision when doing the actual integration. Public source is preferable to a private conversation or repository as a contributor's technical reference.

## Repository baseline inspected for this capture

Base commit: `bd20e83cbe2711ff61ba630349299f58674a8751`.

| File | What it establishes |
| --- | --- |
| `Package.swift` | Swift tools 6.0; macOS 14; `granny`, `GrannyCore`, and tests; Argument Parser and SwiftLintPlugins dependencies. |
| `Sources/granny/Granny.swift` | A placeholder command that prints the core version, not an implemented Apple integration. |
| `.github/workflows/ci.yml` | macOS 26 CI running build, tests, and plugin-based strict lint. |
| `AGENTS.md`, `CLAUDE.md` | Existing code-intelligence/build/privacy rules and a shared instruction symlink. |
| `.agents/skills/repository-management/SKILL.md` | Existing repository-maintenance procedure and explicit settings-change boundary. |

This PR changes documentation only. It does not establish a new local build, live Mac integration, signed release, model benchmark, or installed runtime. Do not interpret a later scaffold CI pass as evidence that the planned providers work.

## Upstream implementation map

| Area | Source to inspect | Important boundary |
| --- | --- | --- |
| Beeper CLI | [IMessageCLI.swift](https://github.com/beeper/platform-imessage/blob/a4491f19a390a0ebfa79c75518282556cbd04e4d/src/IMessage/Sources/IMessageCLI/IMessageCLI.swift) | Earlier assessment revision; recheck current API/CLI exposure before adding flags. |
| Beeper library and events | [PlatformAPI.swift](https://github.com/beeper/platform-imessage/blob/a4491f19a390a0ebfa79c75518282556cbd04e4d/src/IMessage/Sources/IMessage/PlatformAPI.swift), [event watcher](https://github.com/beeper/platform-imessage/tree/a4491f19a390a0ebfa79c75518282556cbd04e4d/src/IMessage/Sources/IMessage/EventWatcher) | Native capability, successful command completion, correctly targeted action, and durable replay are different claims. |
| Send Later | [imsg scheduled reader](https://github.com/openclaw/imsg/blob/5af52a029b3d027cc064f16ead5ed60b888febfb/Sources/IMsgCore/MessageStore%2BScheduled.swift) | Reference for a narrow read. Verify scheduling-state interpretation; do not infer write/scheduling functionality. |
| Calendar / Contacts | [Apple PIM](https://github.com/omarshahine/apple-pim) | Reuse native operations while checking executable/library and permission-host boundaries. |
| Rich Reminders | [RemCTL](https://github.com/viticci/remctl) | A specialized mixed-language provider; retaining it is intentional. |
| Notes / Photos | [Notes MCP](https://github.com/sweetrb/apple-notes-mcp), [osxphotos](https://github.com/RhetTbull/osxphotos) | Separate existing interfaces, not a mandate to build new facades. |
| Voice Memos | [TSRP Store](https://github.com/mattt/TSRP/blob/main/Sources/TSRP/Store.swift), [AudioFile](https://github.com/mattt/TSRP/blob/main/Sources/TSRP/AudioFile.swift) | The reviewed library returns recording/file information and leaves authorization to its caller. Locating a file does not implement a safe export or prove audio decoding. |
| Export safety reference | [macos-voice-memos-export](https://github.com/polarity-dev/macos-voice-memos-export) | Reference only. The reviewed implementation's `.m4a` restriction and ad-hoc signing should not be inherited blindly. |
| Calls / voicemail | [Phone.swift](https://github.com/mattt/iMCP/blob/main/App/Services/Phone.swift), [Voicemail.swift](https://github.com/mattt/iMCP/blob/main/App/Services/Voicemail.swift), [VoicemailStore.swift](https://github.com/mattt/iMCP/blob/main/App/Services/VoicemailStore.swift) | Local private stores; availability, schema, permission scope, and incomplete reads need actual acceptance. |
| Permission/communication patterns | [iMCP](https://github.com/mattt/iMCP) | Study protected-folder grants and bounded local operations. Do not copy its entire server/discovery stack or assume a private socket authenticates every same-user caller. |
| Speech engine | [FluidAudio](https://github.com/FluidInference/FluidAudio) | Check compatible model artifacts, decoding, long-form accuracy, diarization, and full workflow cost rather than extrapolating vendor benchmarks. |
| Event composition | [Swift Async Algorithms](https://github.com/apple/swift-async-algorithms) | Operators coordinate values over time; they do not provide cross-restart durability. |

Library selections and their intended jobs have one home: [design.md](../design.md). Popularity counts and earlier performance claims are deliberately not frozen into requirements.

## Language and coding-agent references

- [The Swift language guide](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/) and [Swift API design guidelines](https://www.swift.org/documentation/api-design-guidelines/): standard facilities and idioms before custom machinery.
- [Agent guidance sources](agent-guidance-sources-2026-11-04.md): official Codex/Claude instructions, Matt Pocock skills, community examples, and the patterns adopted from them.

The owner's private agent setup and earlier rebuild informed these practices, but this public repository has no dependency on private instructions, accounts, or personal evidence.
