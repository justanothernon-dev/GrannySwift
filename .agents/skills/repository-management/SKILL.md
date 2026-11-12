---
name: repository-management
description: Manage coherent task branches, PRs, worktrees and safe repository cleanup; audit repository guardrails with explicit settings approvals.
---

# Repository management

## Everyday task and repository hygiene

Prefer **Claude Code Desktop or Codex Desktop's native Git and worktree management**. No extra CLI is required for ordinary work. Use external cleanup tools only when existing controls cannot do the job safely.

**Start clean and with purpose.** Inspect the active branch, open PRs, any local changes and existing implementation before making another solution. Use one dedicated branch/worktree per coherent task, based on current `main` unless deliberately stacking dependent changes. Do not mix unrelated work or overwrite a dirty workspace.

**Keep the change understandable.** Make focused PRs with an outcome and acceptance evidence. Prefer extending existing providers/components over a second implementation. Remove obsolete code, unused packages, redundant tests and outdated guidance when replacing behavior; if compatibility is truly needed, name the consumer and give the temporary path an accountable retirement condition. Avoid dumping generated assets, build outputs, log files or temporary experiments into Git. When behavior changes, update relevant tests and code-grounded component READMEs in that PR.

**Hand off deliberately.** Record the task/PR, what was changed, verified, blocked and deferred, and whether any uncommitted/unpushed or worktree-local changes must be preserved. Do not claim a merge is a running release.

**Clean only completed work.** After a confirmed **merged PR**, verify no other agent/session is using its branch or worktree and inspect for unique, dirty, untracked or unpushed changes. Then remove its completed worktree/local branch and remote branch where appropriate. GitHub's option to delete merged PR branches is a useful opt-in setting, but do not switch settings without approval. Squash merges require actual PR-state checks; `git branch --merged` alone can be misleading. Never treat a closed-but-unmerged PR, an old branch, or an idle worktree as safe to delete. No unattended force deletion of uncertain work; surface it for review.

**Occasional tidying, not endless ceremony.** When the repository becomes harder to navigate or at a relevant milestone, identify duplicate implementations, obsolete compatibility adapters, abandoned PRs/workspaces, redundant documentation and accidental build artifacts. Propose small, verifiable cleanup rather than a new scheduler, daemon or maintenance framework. PRs and issues own per-task history; the repository keeps no status file.

## GitHub settings and governance

The practices from GitHub's [Introduction to Repository Management](https://github.com/skills/introduction-to-repository-management) course (MIT, © 2025 GitHub Skills), adapted to this repository. Settings can be reviewed in GitHub's UI or authorized tools; the CLI commands below are optional ways an agent can perform the work.

Verify the actual repository and default branch first. `gh repo view --json nameWithOwner,visibility,defaultBranchRef` is one optional agent-side method; use the verified `OWNER/REPO` below.

## Approval boundary

Files (`.gitignore`, `CONTRIBUTING.md`, `CODEOWNERS`, templates, `SECURITY.md`, `dependabot.yml`) are ordinary commits. **Settings** changes (rulesets, collaborators, Dependabot toggles, code scanning, vulnerability reporting) alter who can do what on the repository: explain the exact effect and obtain the repository owner's approval before each one, unless the request already explicitly authorizes that change.

A `main` ruleset that requires pull requests ends direct pushes to `main`, including the agent's own. Say so when proposing it, and only create bypass permissions after an explicit separate decision by the repository owner.

## Areas

Work through the areas the request touches. **Audit** means: report each area as present, missing or misconfigured, with the evidence (file path or API response). Done when every area is either in place and read back, or reported with its gap.

1. **Protect `main`** with a branch ruleset: restrict deletions, block force pushes, require a pull request (0 approvals, code-owner review on).
   ```bash
   gh api repos/OWNER/REPO/rulesets -X POST --input - <<'JSON'
   {"name":"Protect main","target":"branch","enforcement":"active",
    "conditions":{"ref_name":{"include":["~DEFAULT_BRANCH","refs/heads/main"],"exclude":[]}},
    "rules":[{"type":"deletion"},{"type":"non_fast_forward"},
     {"type":"pull_request","parameters":{"required_approving_review_count":0,
      "require_code_owner_review":true,"dismiss_stale_reviews_on_push":false,
      "require_last_push_approval":false,"required_review_thread_resolution":false}}]}
   JSON
   ```
   Read back with `gh api repos/OWNER/REPO/rulesets`.
2. **`.gitignore`**: start from [github/gitignore](https://github.com/github/gitignore) (`Swift.gitignore`), keep `.DS_Store`, and cover any file holding secrets (`.env`, signing material).
3. **Development workflow**: build/test truth lives in `Package.swift` and CI, the concise agent entry point in `AGENTS.md`, and Git/worktree/PR lifecycle here. Do not add a contributor guide without a demonstrated need.
4. **`CODEOWNERS`** (root or `.github/`): map core paths to the owner's handle so pull requests request the right reviewer. Personal repositories grant collaborators write only; finer roles need an organization.
5. **`CODE_OF_CONDUCT.md`**: adapt the [Contributor Covenant](https://www.contributor-covenant.org/) and name a real reporting contact. Ask the repository owner for the contact; never invent one.
6. **Issue templates** in `.github/ISSUE_TEMPLATE/`: a bug report and a feature request, as issue forms (`.yml`) for structured fields.
7. **Dependabot**: turn on alerts and security updates, then commit `.github/dependabot.yml` with `package-ecosystem: swift` (Swift Package Manager) and `github-actions`.
   ```bash
   gh api -X PUT repos/OWNER/REPO/vulnerability-alerts
   gh api -X PUT repos/OWNER/REPO/automated-security-fixes
   ```
8. **Code scanning**: enable CodeQL default setup (Swift is supported; it runs on macOS runners, which bill more minutes on private repositories).
   ```bash
   gh api -X PATCH repos/OWNER/REPO/code-scanning/default-setup -f state=configured
   ```
9. **Security policy**: enable private vulnerability reporting, then commit `SECURITY.md` telling reporters to use the Security tab's **Report a vulnerability** form instead of a public issue, with response times the repository owner agrees to.
   ```bash
   gh api -X PUT repos/OWNER/REPO/private-vulnerability-reporting
   ```

Once a `main` ruleset is active, deliver file changes on a branch with a pull request; keep its public PR body free of private material (see `AGENTS.md`).
