# GrannySwift

A Swift-first macOS capability layer for people and local coding agents. The direction is to reuse strong Apple integrations, extend their interfaces where necessary, and return useful results without rebuilding the providers underneath them.

**Current state:** the repository is a Swift package scaffold with a placeholder command. The selected integrations below are design decisions, not implemented or installed features; [docs/design.md](docs/design.md) marks what is built and what is not.

## Start here

- [Design](docs/design.md): the product intent, locked decisions, selected providers and libraries, and boundaries, with each part not built yet marked.
- [Decision records](docs/adr/): why the hard-to-reverse choices were made.
- [Next design session](docs/GRILL.md): the unresolved questions and facts still to establish. Naming and the detailed CLI experience remain part of that work.
- [Research notes](docs/research/): upstream implementations to inspect and the important limits on earlier findings, and the sources behind the agent instructions.
- [Agent instructions](AGENTS.md): the concise, shared Codex/Claude entry point.

## Direction

One Swift command surface, compatibility aliases where needed, and a coherent signing/permission strategy. Messages uses Beeper; Calendar and Contacts use Apple PIM; Reminders uses RemCTL. Voice Memos uses TSRP with a small extraction/export addition. Call history and voicemail start read-only. Notes MCP stays separate and Photos retains osxphotos. FluidAudio is the selected transcription engine; its existing consumers and migration boundary must remain explicit.

The previous AppleSuite behavior is a useful reference, not a requirement to reproduce its Python architecture. GrannySwift should be usable without WobOS; any WobOS-specific watches, decisions, and notifications belong to that consumer.

## Understanding the components

As meaningful parts of the application are built, their own folder-level `README.md` files should explain **what that part does, how the important pieces work together, and what it means in practice**. They are readable walkthroughs grounded in the actual implementation—not exhaustive file catalogs or automatic boilerplate.

The owner will help shape their voice by dictating explanations, examples, and corrections. Coding agents should preserve that way of explaining the concept while keeping the mechanics accurate as the code changes. We will write these walkthroughs alongside real components rather than invent them for placeholder folders.

## Development

The current SwiftPM manifest and [macOS CI workflow](.github/workflows/ci.yml) show the actual build and verification setup. Their configuration is not a promise that every planned provider already works.

No migration, signing grant, model preparation, or production installation occurs just by building this scaffold.
