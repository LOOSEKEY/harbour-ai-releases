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
- The HARBOUR AI version and platform (Windows / Linux / Mac), and whether the instance was
  exposed on a network or running locally only

### What to expect

- Security reports are handled **any day of the year**, not only on working days.
- Once a vulnerability is confirmed, our target is a **fixed release within 8 hours**, day
  or night. The release notes say plainly that it is a security fix.
- Coordinated disclosure: we'll work with you on the fix and a sensible timeline, and we're
  happy to credit you once the issue is resolved (or keep you anonymous — your choice).

How the fix reaches a machine depends on its update setting (⚙ SYSTEM → Software updates):
automatically, from an update folder on the office network, or by someone running the new
installer. **A machine with no internet gets the fix only when someone installs it.**
Support for everything other than security is described in [SUPPORT.md](SUPPORT.md).

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

Security fixes ship in the **latest release**. Please keep your installation up to date:
on Windows and Linux the in-app updater pulls the newest version unless it has been switched off
or pointed at a local update folder; on a Mac, HARBOUR tells you a new version is out and opens
the download. You can always download it from the
[Releases page](https://github.com/LOOSEKEY/harbour-ai-releases/releases/latest). Older
versions do not receive backported fixes.

## Security posture (overview)

- **Local-first by design** — model inference and your data stay on your own device; nothing
  is sent to a cloud service.
- **Trust Layer** — every AI response carries an Ed25519-signed receipt, recorded in a
  tamper-evident audit ledger you can verify independently; secrets are held in an encrypted
  local vault; a prompt-injection firewall and output guardrails sit in front of the model.
- **Authentication** — token-based auth with password hashing; the API enforces auth on
  protected routes. Optional two-factor codes (TOTP). Each user changes their own password (from
  v1.3.32; the current password is required and every other session is signed out), so an
  administrator never needs to know anyone's.
- **Testing** — the platform receives ongoing internal security review. Every release must pass an automated test gate (including an
  auth-enforcement and route-safety harness) before it can be published, and the codebase now
  receives a **monthly security scan** — static analysis, a dependency-CVE audit, and live
  authentication / injection / path-traversal probes run against a running instance.
- **Dependencies** — third-party dependencies are monitored continuously and updated as
  upstream fixes land; each monthly scan brings every dependency with an available fix up to
  date. **Most recent scan: 12 November 2026.**

> **Latest scan — 12 November 2026 (v1.3.34):** a deep scan of every signed-in route. Deleting a
> custom agent erased every user's chat history (and clearing a chat cleared it for everyone); the
> Computer Operator screen did not apply the role rules or the injection firewall; live-voice and
> developer-API sessions outlived a disabled account or a password change; reseller client keys and
> install-wide settings (email, Teams, calendar, phone, WhatsApp, video provider, the egress
> kill-switch) could be changed by any signed-in account and now need an administrator; project
> files, device lock/wipe acknowledgements and schedules were not tied to their owner; and the
> production Docker Compose file left port 8000 published beside the HTTPS proxy. All fixed, each
> with a regression test. The PDF reader also received the remaining seven crafted-PDF fixes.

Thank you for helping keep HARBOUR AI and its users safe.
