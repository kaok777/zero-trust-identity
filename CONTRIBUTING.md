# Contributing

This is currently a solo project. These rules exist anyway: they are the conventions I would otherwise forget by week four, and they apply to every change, including mine.

## Ground rules

- **One issue, one branch, one pull request.** If a PR needs the word "and" to describe it, it should have been two.
- **No direct pushes to `main`.** The only exception was the initial `chore: repository scaffolding` commit.
- **`main` is always deployable.** Branches live hours to two days, not weeks (trunk-based development).

## Branch naming

`type/short-description`, lowercase, hyphen-separated.

| Type | Use for | Example |
| --- | --- | --- |
| `feat` | New behaviour | `feat/webauthn-registration-options` |
| `fix` | Bug fix | `fix/refresh-token-reuse-race` |
| `chore` | Tooling, deps, housekeeping | `chore/bump-node-22-patch` |
| `docs` | Documentation only | `docs/adr-003-challenge-storage` |
| `refactor` | No behaviour change | `refactor/extract-decide-rotation` |
| `test` | Tests only | `test/audit-chain-tamper` |
| `infra` | Terraform / CI / deployment | `infra/ecs-service-module` |

## Commit messages and PR titles

[Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/): `type: summary`, imperative mood, lowercase, no trailing full stop, under about 72 characters.

```text
feat: add refresh-token rotation with reuse detection
fix: reject expired WebAuthn challenges
chore: repository scaffolding
```

Breaking change: add `!` after the type (`feat!: ...`) and a `BREAKING CHANGE:` footer.

Merges are **squash and merge**, and the **PR title becomes the commit message on `main`**, so the PR title must follow the format above. Individual commits on a branch can be scrappy.

## Pull requests

1. Open the PR against `main` and fill in the template completely, including the security-impact sentence. "No security impact" on a PR that touches token handling is the habit that makes the checklist worthless.
2. Link the issue with `Closes #NN`.
3. Self-review in GitHub's diff view, not your editor, before merging. Look for stray debug logging, TODOs, disabled tests.
4. CI must be green and conversations resolved.
5. A PR that changes a recorded decision must add or update an ADR in the same PR. Mark the old one *Superseded*; never edit it.

## Review policy (and why it looks like this)

Branch protection on `main`:

| Setting | Value | Reason |
| --- | --- | --- |
| Require a pull request before merging | On | Every change passes through checks and a review moment |
| Required approvals | **0** | GitHub does not allow approving your own PR, so 1 would deadlock every merge. Raise to 1 when a second maintainer exists. |
| Require review from Code Owners | **Off** | Same reason: I am the only code owner. `CODEOWNERS` still auto-requests review and documents ownership. |
| Require status checks to pass | On (once CI has run once) | The real gate while I am the only reviewer |
| Require branches to be up to date | On | Prevents "both PRs passed alone, main is broken" |
| Require conversation resolution | On | Cannot merge past my own review comment |
| Force pushes / deletions | Blocked | History on `main` is an audit trail |
| Signed commits | On once signing is configured | Commit authorship should be verifiable, not self-declared |
| Bypass actors | None | No routine bypass |

Honest summary: with one maintainer, the enforced controls are the PR requirement, CI and the self-review checklist, not a second pair of eyes. That gap is known and the condition for closing it is stated above.

## Local setup and running tests

See the [README](README.md#run-locally-in-under-five-minutes). Before opening a PR, run the same stages CI runs, cheapest first:

```bash
# TODO: fill in as each tool is introduced. Target commands:
npm run lint          # lint and format check
npm test              # unit tests (no containers)
npm run build         # type-check and build all workspaces
npm run test:integration   # Testcontainers: real PostgreSQL and Valkey
```

## Secrets

- Never commit credentials, `.env` files or Terraform state. `.env.example` lists the configuration contract with obviously fake values.
- If a secret is committed, treat it as compromised: **revoke and rotate it first**, then clean history. Deleting the commit is not remediation.

## Decisions

Anything hard to reverse gets an ADR in [`docs/adr/`](docs/adr/). Open a "decision" issue first if the question is still open.
