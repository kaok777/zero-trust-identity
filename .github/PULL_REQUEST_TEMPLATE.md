<!--
PR title = the squash-commit message on main, so it must follow Conventional Commits:
  feat: add WebAuthn registration options endpoint
Types: feat | fix | chore | docs | refactor | test | infra
-->

## What and why
<!-- One or two sentences. Why is this change needed, not just what it does. -->

Closes #

## How I verified it
<!-- Commands run, tests added, screenshots, EXPLAIN output, load-test result. -->

## Checklist

- [ ] **Tests** added or updated, and they fail without this change
- [ ] **Docs** updated (README, CONTRIBUTING, runbook, inline comments where needed)
- [ ] **Security impact** considered. Write one honest sentence below, even if the answer is "none".
- [ ] **Rollback path:** how I undo this if it breaks (revert commit, redeploy previous image digest, `terraform` state step, migration down)
- [ ] **ADR** added or updated if this changes an architectural decision (supersede the old one, never edit it)
- [ ] **Evidence** committed to `docs/evidence/` if this changes performance-sensitive code (before/after `EXPLAIN` or load test)
- [ ] No secrets, tokens, `.env` files or `*.tfstate` in the diff
- [ ] I read the diff in GitHub's UI (not my editor) before merging

### Security impact
<!-- Auth, tokens, input handling, secrets, IAM, new dependencies, logging of sensitive data. -->

### Rollback
<!-- The exact steps, not "revert it". -->
