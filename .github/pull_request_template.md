<!--
Audience and voice
Write for a curious, sharp reader who is not a programmer by training and has not seen the tool calls, diffs, or session history. Teach as a professor of software engineering and AI development would: state the core idea first, ground it in one concrete example from this change, then give detail.

Use plain conversational English instead of shop jargon ("normal working case" rather than "happy path"; "four-part" rather than "four-rung"). Write connected prose in the opener and Rationale. Write short fragments without terminal periods in the File map and Proof block. When a build record or rationale is missing, state that plainly ("the build records do not say why") rather than guessing, because an invented reason reads as the reader's own decision.

Quote the reader's own words, in italics and without a date, where they were the reason for a choice. Give a trade-off's reason as one short clause, then one concise clause that explains it, linked to the decision record when one marks the choice: "A git-only lock was prioritized given minimal synchronization overhead: all three agents commit through git, so there is nothing to keep in step (ADR 40)."

Remove every one of these comments, and every part left out, from the finished description. GitHub hides them, but they bloat the text an agent reads back later.

Vocabulary and glossary
Leave general programming terms (worktree, diff, pre-commit hook) unexplained.
For repo-specific terms and outside ideas or authors this change leans on:
- If `GLOSSARY.md` and `docs/taught-terms.md` exist, run `bin/glossary check <draft>` (or read both files).
- Below 3 approved pull requests: teach a repo term once on first mention (plain words first, nickname in quotes), then use the nickname bare. For an outside idea or author, link the source and state the idea in one clause.
- At 3 or more approved pull requests: use the term or name bare.
- Before those files exist: treat every repo-specific term and outside idea as below 3.

Examples:
- Repo term: our code-review redirecting skill ("signpost") -> signpost
- Repo term: a check on whether a repo's copy deviates from the master ("drift check") -> drift check
- Outside idea: Drawing on Cindy Sridharan's debugging method, which hunts for one cited contradiction or unhandled corner case,...

Scaling (what shrinks or vanishes)
Size follows what the reader must learn or decide, not how much work went in. Decide the size before writing, from the kind of change, then let the triggers below add parts. Delete any heading, placeholder, or subsection that does not apply rather than leaving empty stubs or "None" fillers:
- Small fix or prose edit (1-3 files, no spec, no architecture shift): keep the H1 title, optional ticket line, a 2-3 sentence opener, a brief Proof note, and Impact & rollback only if non-obvious. Delete the visual, Walkthrough line, Rationale, How it works now (unless one diff block shows the whole edit), File map, Deviations, and Decisions & tracking.
- Medium change: keep sections with real substance; delete Walkthrough, roadmap alignment, and File map (for 5 or fewer files).
- Substantial or spec build: keep the full structure below.
Keep the closing `Closes` line at every size, even when `Decisions & tracking` is deleted, because that line is what moves the ticket.
Triggers that add a part at any size: an approved spec (the `Spec build:` title, full Rationale, a visual); a change to how parts connect, a new integration, or an edit to shared instructions or hooks (the Walkthrough line); more than 5 files (the File map); a new repo term (it is taught in the opener); a real deviation, open call, or non-obvious limit (that section).

Formatting and GitHub rendering
- Inline backticks: reserve for exact commands, flags, file paths, or config keys someone might run or search (`git revert`, `core.hooksPath`, `link`). Write agent roles, skills, concepts, and plain subcommand lists in normal text (Commands: lock, status, check, unlock --reason, log, and diff) so backticks do not cluster back-to-back in prose.
- Fenced `diff` blocks: use for exact before/after instruction or config diffs and for the Proof block. GitHub neither wraps fenced lines nor renders bold or links inside fences, so place clickable links in the prose above, and keep every Proof line under ~85 characters. An instruction diff shows each line whole even when it is long, because the exact wording is what the reader approves.
- Markdown tables: use only for compact multi-attribute comparisons with few-word cells (such as benchmarks); use fenced `diff` blocks or grouped bullets instead of wide prose tables.

Public repositories and tracking
Never include personal names, private tracker URLs, or private repository references in a public repository. Omit the Tickets line there or link public GitHub issues (`#123`) only.
Set the GitHub pull request title to plain English for what the change does, followed by the primary ticket ID in parentheses when tracked (e.g., `Add the pull request template and drift check (ISSUE-56)`). End the description with one visible `Closes` line naming every ticket this pull request finishes, because that line is what moves each ticket when it merges. In a public repository with a private tracker, leave that line out and close the tickets after the merge. Add no tool-generated footer.
-->

<!--
Title and tickets
H1 title in plain English, sentence case, no period. Prefix with `Spec build: ` when implementing an approved spec, or `Fix: ` for a bug fix.
No tickets line: this repository is public and its tracker is private. Only when a public GitHub issue exists, link it directly below the title (`**Issue #123** - [Short name](link)`).
-->
# {Spec build: Plain-English title}

<!--
Opener (no heading; one paragraph, four beats):
1. The gap or problem before this change ("Until now,...").
2. What this pull request changes and what it covers.
3. What happens on merge (installs, removals, behavior shifts), teaching new repo terms once.
4. Through line (final sentence): trace in plain prose from upstream roadmap, research, or design issues to this build with named links rather than bare ticket IDs or arrow chains. Omit beat 4 on standalone fixes.
On a spec build with no material deviations, close the paragraph with one italic sentence saying so (*No deviations from the spec.*) and delete the Deviations section.
-->
{Opening paragraph ending in the prose through line.}

<!--
Visual and walkthrough (place directly below the opener so it trims opener prose; delete on small fixes or prose-only edits):
Choose one visual by kind of change:
- Spec build, multi-step workflow, or architecture mechanism: an animated SVG (self-contained, with CSS @keyframes or SMIL, dark mode via prefers-color-scheme, reduced motion via prefers-reduced-motion, <title> and <desc>, no JS). Motion shows the mechanism, with no decorative loops. A diagram that documents lasting design is committed to `docs/diagrams/{name}.svg` on the PR branch and linked from docs/design.md or the ADR. A one-off that should not live on `main` goes on a long-lived side branch (`pr-assets`), or is drawn as inline Mermaid. Either way, embed it by commit, `https://github.com/{owner}/{repo}/blob/{commit sha}/{path}.svg?raw=true`, so it shows in a private repo and keeps working after the branch is deleted. Open the pull request page once and check that it renders. Never embed raw <svg> tags or bare relative paths in a GitHub PR body.
- Simpler static flow or module map: an inline ```mermaid block.
- App or UI change: a screenshot, before/after pair, or short GIF.
- Instruction or config-only change: omit here and show real diff blocks in "How it works now".

Follow the visual with one *italicized sentence* narrating what it shows in plain English.

Walkthrough: include only on substantial PRs (large or sensitive changes, shifts in how modules connect, new integrations, global-instruction or hook changes). Build the four-part page (Boundaries, Data flow, Failure modes, Trade-offs) via the `walkthrough` skill and link it below. If triggered and skipped, write `Walkthrough: none built for this pull request (see Deviations).` On all other PRs, delete the Walkthrough line.
-->
![{What the picture shows}](https://github.com/{owner}/{repo}/blob/{commit sha}/{path}.svg?raw=true)

*{One plain-English sentence narrating the visual.}*

Walkthrough: {link to the four-part walkthrough page, or delete this line}

## Rationale

<!--
Delete this section on small fixes whose reason fits in the opener.
Open with `**The principle: <core concept>.**` plus 1-2 sentences teaching the underlying engineering or AI-development idea before implementation detail.

Then, when more than one driver follows, one lead-in line saying how many and from where ("Three findings from the research shaped it:"), and one block per major design driver (usually 1-3):
1. Standalone bold header in regular font, no terminal period.
2. One paragraph on what led to it: link any prior ADR and state what it decided, weave in the reader's own words or prior picks as evidence (in italics, no date), and cite outside ideas per the glossary rule.
3. One to three bullets starting with `- Now,...` stating the concrete change. A chosen trade-off gets one short clause and one concise explanatory clause, linked to its decision record when there is one.

Example block:
**Lock the exam in git, not in three agent settings files**

In ADR 27, where we decided each approved scenario gets a failing test first, nothing stopped an agent from bending tests to fit buggy code. In review the reader asked, *"{their own words}"*, and picked a human-team split.

- Now, before a worker builds, a git lock blocks edits to the failing acceptance tests the build lead writes first.
- A git-only lock was prioritized given minimal synchronization overhead: all three agents commit through git, so there is nothing to keep in step (ADR 40).

If this PR is one slice of a larger research report or roadmap, close Rationale with:
**How this matches <report or roadmap>:**
- **Already merged:**...
- **Lands here:**...
- **Still ahead:** (break multiple follow-ups into nested sub-bullets)
-->

## How it works now

<!--
Cover edge rules and mechanics the opener and visual did not already explain (fallbacks, caps, solo vs multi-agent paths), as bullets that each open with a bold label (`- **Lock edge rules:**...`); skip repeating the visual's normal sequence.

For instruction, prompt, or config edits, open with one bold line naming the file, then show each real before/after change under a bold 3-6 word header with no terminal period, followed by a ```diff block:
**Done requires a failure check**
```diff
- old line
+ new line
```

For PRs changing more than 5 files, add a folded File map grouped by role (Commands, Agents, Skills, Docs, Tests). Bold key files inline and link them to their PR diff anchors; use clean plain labels for docs and ADRs (`ADR 40`, `global instructions file`) instead of raw paths. Keep this as markdown bullets (not a fenced diff block) so bold and links render. Delete the <details> block for 5 or fewer files.
-->

<details><summary>File map ({N} files: {X} lines added, {Y} removed)</summary>

- **{Group}**
  - **{Key file label}** (new): {short fragment, no period}
  - {Supporting item}: {short fragment, no period}

Bold marks the key files. All {N} are in the pull request's file view.

</details>

## How we know it works

<!--
Report honestly what ran, what checks could still miss, and what was not verified, naming every known gap and obstacle. Prose-only or docs-only PRs skip runtime verification; state what reviewer or a direct read checked instead.

Open with 2-3 sentences: the headline result (defects caught and fixed, round count, head commit SHA), plain-English glosses for any test jargon used below (e.g., `fake call-logging scripts ("stand-ins")`), and the legend (`+` proved, `!` what checks could still miss, `-` not verified).

Follow with one compact ```diff block of short fragments without terminal periods, every line under ~85 characters, and no bold or links inside the fence:
- `@@ {Check group and scope} @@`
- `+` what was proved (normal working case and failure case where applicable)
- `!` what that check could still miss (stand-ins, single-platform runs, narrow scope)
- `@@ Not verified @@` followed by `-` lines for everything unchecked.

Omit command-by-command logs and requirement-by-requirement checklists from this description. Post the full verifier run log and requirement map in one collapsed PR comment (`<details><summary>Verification log & requirement map ({sha})</summary>...</details>`) so it stays attached to the PR without crowding the description.
-->

{Headline outcome, test-term glosses, and legend: (`+` proved, `!` what checks could still miss, `-` not verified)}

```diff
@@ Automated tests (head commit {sha}) @@
+ {What passed and what real behavior it exercised}
! {Stand-ins, mocks, or gaps this suite cannot catch}

@@ Live check / verifier run @@
+ {Normal working case and failure case proved}
! {Scope limits or edge cases not exercised}

@@ Not verified @@
- {Anything unchecked before merge}
```

## Deviations

<!--
Keep only departures with material functional or process implications: behavior differing from the spec, changed install order, unsupported repo setups, a skipped substantial-PR walkthrough, or any unlocked acceptance test with its logged reason.
Skip routine expected work such as updating assertions in existing tests, syncing supporting docs/skills, or fix-round history already summarized in Proof. Delete this entire section when there are no material deviations; on a spec build the opener then says so.
-->

- **{Material deviation}:** {Plain-English impact and reason; say plainly if records do not explain why.}

## Impact & rollback

<!--
One lead sentence stating what this touches and when it takes effect. Follow with concrete breakage risks and rollback reality (clean `git revert`, residual state outside git, or one-way door). For a trivial reversible fix, fold this into one sentence or the opener.
-->

{What this affects and when it takes effect.}

- **Could break:** {Specific realistic risks}
- **Rollback:** {Clean `git revert` plus any manual cleanup, or note if one-way}

## Public & macOS checks

<!--
Keep every bullet that applies to this pull request; delete bullets that do not apply (for example, delete the Swift and macOS bullets on a docs-only or config-only change). Keep this section concise and do not repeat test output already in "How we know it works".
- **Public hygiene & attribution:** confirm the diff, commit messages, and PR text hold no personal names, emails, local home paths, private repo or tracker references, real Apple data (messages, contacts, calendars, notes, photos, recordings), or signing material. Note that any test fixtures are invented and that adapted upstream code or vendored skills keep their source and license notices.
- **Swift & CI gate:** for Swift or manifest changes, state that `swift build`, `swift test`, and `swiftlint --strict` passed locally (matching `.github/workflows/ci.yml` on `macos-26`). Where a placeholder or unit build passes without live provider integration, say so plainly.
- **macOS permissions & live-data boundary:** for provider, plugin, or permission-host changes, name required macOS privacy grants (TCC, Full Disk Access, Accessibility), signing/entitlement expectations, or one-time machine setup steps. Confirm reads stayed read-only and any live writes targeted isolated disposable records.
-->

- **Public hygiene & attribution:** {Diff and PR text scanned for personal data, local paths, private references, and signing material; invented fixtures and upstream license notices verified}
- **Swift & CI gate:** {`swift build`, `swift test`, and `swiftlint --strict` status, or delete if no Swift code changed}
- **macOS permissions & live-data boundary:** {Required macOS grants, signing, or one-time setup steps, and read-only / disposable-target status, or delete if not applicable}

## Decisions & tracking

<!--
Keep only subsections with real content; delete this entire section when nothing applies. Accepted limitations cite their decision record, never a separate open-items file.
- **Decided:** calls already settled during review so they are not re-asked.
- **Waiting on your go:** put each requested action on its own bold line, followed by concise context, a bold **Recommendation:**, and a link to where it can be answered, if there is one.
- **Accepted limitations:** non-blocking caveats logged in an ADR (link the ADR and state what it chose). When a limitation appears to conflict with how the system normally works, explain the underlying mechanism in one sentence so the reader sees why.
-->

**Decided:** {Resolved call, or delete}

**Waiting on your go:** **{Action needed on its own bold line}**
{Concise context.} **Recommendation:** {Recommended choice and reason.}

**Accepted limitations** (no action needed to merge; logged in {ADR N}, where we chose {brief summary}):
- **{Limitation}:** {Underlying mechanism in plain English, then practical effect.}

Closes {TEAM-N}, {TEAM-N}
