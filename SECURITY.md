# Security Policy

HARBOUR AI is built privacy- and security-first: inference runs **100% locally**, and your
data never leaves your machine. We take security reports seriously and welcome responsible
disclosure from the community.

## Reporting a vulnerability

**Please report security issues privately — do not open a public GitHub issue.**

- **Email:** Gregorymoores@proton.me
- Use the subject line `SECURITY` so it's triaged quickly.

Please include, where possible:
- A description of the issue and its potential impact
- Steps to reproduce (proof-of-concept welcome)
- The HARBOUR AI version and platform (Windows / Linux), and whether the instance was
  exposed on a network or running locally only

### What to expect

- **Acknowledgement** within 5 business days.
- An initial assessment and severity triage shortly after.
- Coordinated disclosure: we'll work with you on a fix and a sensible timeline, and we're
  happy to credit you once the issue is resolved (or keep you anonymous — your choice).

We ask that you give us a reasonable opportunity to fix an issue before any public
disclosure, and that testing is done only against your own installation — never against
another user's instance or data.

## Scope

In scope:
- The HARBOUR AI desktop application (Electron) and its local backend API
- The licence/activation flow
- This project's published installers and update mechanism

Out of scope:
- Vulnerabilities in third-party dependencies that are already publicly known and awaiting an
  upstream fix (we monitor these and update as fixes land)
- Issues that require physical access to an already-compromised machine
- Social engineering, or denial-of-service against your own local instance
- Findings on the marketing site that have no security impact

## Supported versions

Security fixes ship in the **latest release**. Please keep your installation up to date —
the in-app auto-updater will pull the newest version, or you can download it from the
[Releases page](https://github.com/LOOSEKEY/harbour-ai-releases/releases/latest). Older
versions do not receive backported fixes.

## Security posture (overview)

- **Local-first by design** — model inference and your data stay on your own device; nothing
  is sent to a cloud service.
- **Trust Layer** — every AI response carries an Ed25519-signed receipt, recorded in a
  tamper-evident audit ledger you can verify independently; secrets are held in an encrypted
  local vault; a prompt-injection firewall and output guardrails sit in front of the model.
- **Authentication** — token-based auth with password hashing; the API enforces auth on
  protected routes.
- **Testing** — the platform has undergone external penetration testing and ongoing internal
  security review. Every release must pass an automated test gate (including an
  auth-enforcement and route-safety harness) before it can be published, and the codebase now
  receives a **monthly security scan** — static analysis, a dependency-CVE audit, and live
  authentication / injection / path-traversal probes run against a running instance.
- **Dependencies** — third-party dependencies are monitored continuously and updated as
  upstream fixes land; each monthly scan brings every dependency with an available fix up to
  date.

> **Latest review — 27 July 2026 (v1.3.5):** a full security scan — dependency-CVE audit, static
> analysis, a secrets sweep, and live authentication / injection / path-traversal probes against a
> running instance. Runtime defences (token handling, admin gating, injection and path-traversal
> protection, rate limiting) were all verified holding. **An access-control fault affecting
> multi-user installations was found and fixed:** on an instance with more than one account, a
> signed-in user could reach data belonging to another user of the same machine. **Single-user
> installations were not affected in practice.** A second, smaller access-control issue was fixed
> alongside it. **Dependencies with available fixes were updated**, including a PDF-parsing library
> reachable from uploaded documents. All fixes ship in **v1.3.5** — please keep your installation
> up to date; the in-app updater will pull it automatically.
>
> **Follow-up audit — 29 July 2026 (v1.3.12):** every real-time connection in the app (dictation, live voice, live meetings, the computer operator, and collaborative documents) was tested end to end — each one checked that it accepts a valid session and, just as importantly, that it refuses an invalid or missing one. **All six passed; no way in was found.** One usability fault was fixed alongside: a refused connection could not tell you *why* it had been refused, so an expired session looked like nothing happening.

Thank you for helping keep HARBOUR AI and its users safe.
