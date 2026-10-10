# Architecture Decision Records

An ADR is a short, dated record of one consequential decision: what was decided, what forces led there, what it costs, and what was rejected. The idea comes from Michael Nygard's 2011 post [*Documenting Architecture Decisions*](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions). Decisions recorded in chat history or in your head are lost; recorded here, they are the most valuable artefact in the repository.

## When to write one

Write an ADR when a decision is **hard or expensive to reverse**, **affects more than one component**, or **someone would reasonably ask "why did you do it this way?"** Examples: authentication model, token design, database choice, tenancy isolation, how CI authenticates to the cloud. Do not write one for choices that are cheap to change.

## Rules

1. **One decision per file**, named `NNN-short-title.md` (three digits, zero-padded, never reused). Example: `001-webauthn-sole-factor.md`.
2. **Immutable once Accepted.** Do not edit the reasoning later. To change a decision, write a new ADR and mark the old one `Superseded by ADR-NNN`. The record of what was believed at the time, and why, is the point.
3. **Typo and link fixes are fine.** Changing the decision or its rationale is not.
4. **Same PR as the change.** A PR that changes a recorded decision adds or updates the ADR in that PR.
5. **Be honest about the negatives.** An ADR where every consequence is positive has not been examined.

## Statuses

`Proposed` then `Accepted`, or `Rejected`. Later: `Superseded by ADR-NNN` or `Deprecated`.

## Template

Copy this into a new `NNN-short-title.md`:

```markdown
# ADR-NNN: Title stating the decision as a sentence

## Status
Proposed | Accepted | Superseded by ADR-NNN · YYYY-MM-DD (or Week N)

## Context
The problem and the forces at play: requirements, constraints, threats,
and the options that were on the table. Facts, not advocacy.

## Decision
What we are doing, in active voice. "We will use X."

## Consequences
**Positive:** what becomes easier or safer.
**Negative:** what becomes harder, what risk we accept, what we now must build.

## Rejected alternatives
Each option and the specific reason it lost.

## Revisit when
The observable condition that should reopen this decision.
```

## Index

| ADR | Decision | Status |
| --- | --- | --- |
| 001 | Use WebAuthn/FIDO2 as the sole authentication factor set | Planned |
| 002 | Short-lived access tokens with rotating refresh tokens, not long-lived sessions | Planned |
| 003 | Store WebAuthn challenges in Valkey with `GETDEL` | Planned |
| 004 | Sign tokens with a KMS asymmetric key, not an in-process private key | Planned |
| 005 | Enforce tenant isolation with PostgreSQL row-level security | Planned |
| 006 | GitHub Actions authenticates to AWS via OIDC; no long-lived access keys | Planned |
| 007 | Verify tokens in the application, not in an API Gateway authorizer | Planned |

Update this table when an ADR is written, with a link to its file.

## Further reading

- ADR tooling and templates: <https://adr.github.io>
- A more structured template (MADR): <https://adr.github.io/madr/>
