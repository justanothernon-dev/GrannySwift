---
name: repository-management
description: Sets up and audits this GitHub repository's guardrails: branch rulesets, .gitignore, CONTRIBUTING, CODEOWNERS, code of conduct, issue templates, Dependabot, code scanning, security policy.
---

# Repository management

The practices from GitHub's [Introduction to Repository Management](https://github.com/skills/introduction-to-repository-management) course (MIT, © 2025 GitHub Skills), rewritten as `gh` CLI work an agent can do for this repository. The course clicks through the web UI; every step below has a command instead.

Resolve the repository once: `gh repo view --json nameWithOwner,visibility,defaultBranchRef`. Use the result as `OWNER/REPO` below.

## Approval boundary

Files (`.gitignore`, `CONTRIBUTING.md`, `CODEOWNERS`, templates, `SECURITY.md`, `dependabot.yml`) are ordinary commits. **Settings** changes (rulesets, collaborators, Dependabot toggles, code scanning, vulnerability reporting) alter who can do what on the repository: state the exact effect to the repository owner and get their yes before each one, unless their request already named that change.

A `main` ruleset that requires pull requests ends direct pushes to `main`, including the agent's own. Say so when proposing it, and add the repository owner as a bypass actor (`"bypass_actors":[{"actor_type":"RepositoryRole","actor_id":5,"bypass_mode":"always"}]`, role 5 = admin) if they want to keep pushing directly.

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
3. **`CONTRIBUTING.md`**: development setup (exact build and test commands for this repo), branch-and-PR flow, code style, where to ask for help.
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

Once a `main` ruleset is active, deliver file changes on a branch with a pull request; the `pr` skill writes its body.
