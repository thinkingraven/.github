# Public repository rules

Everything in this organisation can be read, cloned, forked and archived by anyone, permanently. Deleting a file later does not remove it from git history, forks, caches or AI training sets. These rules apply to every public repository and to everyone (and every AI agent) committing to one.

## 1. Never publish

- **Secrets:** API keys, tokens, passwords, private keys, `.env` files, cloud credentials. This includes tests, examples, screenshots, logs and old commits.
- **Employer, client or customer material:** code, data, names, URLs, screenshots or logs. Use fictional demo data (an "acme" org) instead.
- **Personal data:** personal email addresses, phone numbers, home addresses, other people's details.
- **Internal details:** hostnames, IP addresses, dashboards, ticket links.

If something slips through, **rotate the secret first**, then remove it from history (`git filter-repo`) and force-push. Rotation is what actually protects you; history rewrites don't reach existing forks and clones.

## 2. Before a repository goes public

Repositories start **private** and are made public deliberately.

- [ ] Scan the **full git history** for secrets (for example with gitleaks), not just the latest commit.
- [ ] Scan agent files with `npx @thinkingraven/rookery scan .`.
- [ ] Check screenshots, fixtures and examples for real names, data and URLs.
- [ ] Commits are authored with a GitHub `noreply` address.
- [ ] A README and a LICENSE are present (security, conduct and support files are inherited from this repository).
- [ ] Apply the baseline in section 3 straight after flipping it public.

## 3. Every public repository has

- Secret scanning with push protection
- Dependabot alerts and security updates
- CodeQL code scanning (when it contains code)
- Private vulnerability reporting
- A **Protect main** ruleset: no force-push or deletion; changes arrive by pull request with passing checks (owners may bypass)
- Protected release tags (`v*`) where releases are tagged
- Wiki and Projects off unless they're used

## 4. GitHub Actions

- The default `GITHUB_TOKEN` is read-only; grant extra `permissions:` per job, only where needed.
- Only GitHub-owned actions and actions from verified creators. Pin any other action to a full commit SHA.
- Never combine `pull_request_target` with checking out pull-request code. Never print secrets.
- Workflow runs from outside contributors need a maintainer's approval.
- Packages are published from CI with provenance (`npm publish --provenance`), from an npm account with 2FA.

## 5. Accounts and access

- Two-factor authentication on every member account; the organisation requires it.
- As few owners as possible; everyone else gets the least access that works.
- Review third-party app and token access regularly.

## 6. AI agents

Coding agents working in these repositories follow the same rules. They never paste secrets or employer or client material into code, commits, issues or prompts, they use demo data for screenshots and examples, and they read the repository's `AGENTS.md` first.
