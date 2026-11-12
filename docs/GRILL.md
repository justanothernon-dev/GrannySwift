# Next design session

**Purpose:** the open decisions and facts for the first design session, kept here so it can start from the repository and not from a remembered chat.  
**State:** ready for refinement; the recommendations below have not been accepted.

[design.md](design.md) holds the locked choices and [research/upstream-sources-2026-11-04.md](research/upstream-sources-2026-11-04.md) the upstream reading map. The owner asked for the design capture first, with the design session afterward; the recommendations below are not approvals.

## Open owner decisions

These were raised before the destination changed to GrannySwift. None was answered; they are not requirements.

| Question | Recommendation previously proposed, not adopted | Why it matters |
| --- | --- | --- |
| How far must compatibility extend beyond aliases? | Allow better flags/JSON where useful, with explicit migration of real consumers rather than indefinite adapters. | One executable and compatibility aliases are locked; exact old schemas are not. |
| What is the first public release boundary? | A useful Messages-focused increment including the agreed Send Later and v1 awakening work, rather than waiting for every domain. | All selected domains remain target scope; delivery order and first-release completeness are not fixed. |
| How should missing permissions behave in ordinary commands? | Separate interactive setup from unattended reads/actions; return an actionable error rather than a surprise offscreen dialog. | This determines the user experience before the host/IPC mechanism is designed. |
| Does transcription alone imply a retained audio export? | Use direct authorized access or temporary staging where appropriate; retain audio only when export is requested. | Extraction capability is locked; staging lifetime and retained artifacts still need policy. |
| What platform breadth does the first release promise? | Evaluate Apple silicon/macOS 26+ first, but decide only after dependency requirements and target use are clear. | The current scaffold says Swift tools 6.0/macOS 14 and CI uses macOS 26. Do not silently raise the deployment target or treat either as validated support. |
| How should upstream patches be maintained? | Permit narrow pinned patches with attribution and an upgrade path; contribute generic improvements upstream when practical. | Beeper CLI extensibility and TSRP extraction are chosen, but fork/patch ownership and delivery policy remain open. |

The next command-design pass should also resolve names, hierarchy, semantic defaults, output examples, partial-result conventions, and the relationship of the existing transcription capability to GrannySwift. Do not treat previous illustrative commands or the placeholder `granny` command as a finalized API.

## Facts for the implementing agent to establish

These are research/acceptance tasks, not preference questions for the owner:

- Which selected APIs are exposed by the chosen upstream revisions, and which CLI additions actually remain necessary?
- Which process is responsible for each macOS grant, including external providers, and what survives an update?
- Can Beeper's event identities and history cursors support the intended catch-up/recovery behavior without losing source messages?
- How are scheduled rows distinguished from genuinely pending scheduled sends on supported macOS versions?
- Does copying a resolved Voice Memos file reproduce the expected original/edited recording, and can the transcription pipeline decode real `.m4a` and `.qta` assets?
- Which call/voicemail records and audio assets are present locally, and how is incomplete synchronization reported?
- Which compatible Core ML artifact preserves the chosen model family, and what accuracy, long-form, speaker, memory, startup, and cancellation behavior does the actual pipeline exhibit?

During planning, read source and existing evidence. Run live checks or benchmarks when an implementation change or explicit verification request justifies them; do not launch a broad test campaign simply to resume the conversation.
