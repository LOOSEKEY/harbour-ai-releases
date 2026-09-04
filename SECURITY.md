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
  date. **Most recent scan: 24 August 2026.**

> **Earlier review — 27 July 2026 (v1.3.5):** a full security scan — dependency-CVE audit, static
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

> **Earlier review — 10 August 2026 (v1.3.15):** our monthly review, covering dependency CVEs, a
> secrets sweep, and live probes against a running instance. Runtime defences were re-tested and
> verified holding: agent tool confinement (every escape attempt from the July review was re-run and
> refused), sign-in token handling, local-only network binding, and the guarantee that nothing is sent
> externally — measured at **zero bytes** across a full document-indexing cycle. **An access-control
> fault affecting multi-user installations was found and fixed:** the real-time collaboration
> connection confirmed who a user was, but did not confirm that the session they asked for was theirs,
> so on an instance with more than one account a signed-in user could join another user's live session.
> **Single-user installations were not affected** — there is no second account, and the connection is
> reachable only from your own machine. It concerned live traffic only, not stored history. Our July
> follow-up had tested these connections for whether they accept a valid sign-in and refuse an invalid
> one, which they did; this review asked the further question of whether they also check ownership of
> what was requested, and added an automated guard so future real-time features cannot skip it. A
> PDF-parsing library was also updated. All fixes ship in **v1.3.15** — please keep your installation
> up to date; the in-app updater will pull it automatically.

> **Previous review — 24 August 2026 (v1.3.16 / v1.3.17):** our monthly review. Runtime defences were
> re-tested and verified holding: agent tool confinement (all nine escape attempts from the July
> review re-run and refused), sign-in token handling against tampered and forged tokens, local-only
> network binding, every real-time connection, and the guarantee that nothing is sent externally —
> measured again at **zero bytes**, this time across a full document index *and* search.
>
> This review looked at the parts of the system that run on a schedule in the background, which
> earlier reviews had covered less systematically than the parts you click. **An access-control fault
> affecting multi-user installations was found and fixed:** where a user had not set up their own
> Companies House API key, the software fell back to looking for a shared one — but every stored key
> belongs to an individual account, so it could return another user's key and make lookups against
> their allowance. **Single-user installations were not affected** — there is no second account for it
> to find.
>
> **We also removed something that was not a vulnerability, because we would rather it simply did not
> exist.** Scheduled report emails contained code to send results through a third-party email service.
> It could never run in any released version — it required a setting we have never shipped, and we
> confirmed **no customer data has ever been sent through it** — but a privacy promise should not
> depend on a setting staying switched off, and the interface wrongly suggested you could turn it on.
> Report emails now go through **your own mail server** and nowhere else, and an automated check now
> fails our build if any third-party email service is ever referenced again.
>
> Separately, five email features (the daily briefing, board pack, health digest, candidate
> acknowledgements and invoice chasing) had never been able to send at all — they were reading your
> mail settings from the wrong place and failing silently while reporting themselves as configured.
> That is a reliability fault rather than a security one, but it is fixed in the same release and
> those features now tell you when something is wrong instead of failing quietly.
>
> All fixes ship in **v1.3.17** — please keep your installation up to date; the in-app updater will
> pull it automatically. ⚠️ **v1.3.16 and v1.3.17 were Linux-only releases.** The Windows installer
> stayed at v1.3.15 and was unaffected by both faults in a single-user installation; Windows caught
> up in v1.3.19 on 31 August 2026 and now carries both fixes.

> **Latest review — 4 September 2026 (v1.3.20):** three findings, all fixed in this release.
> **No evidence of misuse was found.** One of them needs an action from you.
>
> **Your backups were not being kept.** HARBOUR wrote them to a temporary system folder — a
> location most operating systems clear when the machine restarts, and which on many Linux
> systems is held in memory rather than on disk. The backup was created, reported as
> successful and listed in the app; it simply did not survive a reboot. Nothing was exposed
> and no data was sent anywhere, but a backup you were relying on may not exist.
> **⚠️ Please take a fresh backup after updating.** Backups now sit beside your data, run
> automatically every night, and can be restored from within HARBOUR.
>
> **A locked-out administrator had no way back in.** Administrator rights could only ever be
> granted to the first account created on an installation, and no route could grant them
> again. A forgotten administrator password therefore removed every administrative feature
> from your own machine, permanently, with your data intact but unreachable. There is now a
> local recovery path — a single-use code HARBOUR writes into your data folder, usable only
> from the machine HARBOUR runs on and never transmitted — and the last remaining
> administrator can no longer be removed by accident.
>
> **Email addresses were never checked.** Any text containing an "@" was accepted at sign-up.
> Addresses are now validated, and confirmed by email where you have configured a mail
> server. Where you have not — the normal case for a desktop installation — nothing changes,
> and existing accounts are unaffected.
>
> All three ship in **v1.3.20** on Windows and Linux together, delivered as an in-app update.

> **Previous review — 27 August 2026 (v1.3.18):** an unscheduled review of sign-in and account
> handling, prompted by a question about how logins work rather than by any customer report. **No
> evidence of misuse was found, and nothing here requires any action from you.** Four faults were
> fixed:
>
> **Removing an administrator's rights did not take effect immediately.** The permission check read
> the rights recorded in the user's sign-in token, valid for seven days, instead of reading their
> account. An administrator who had been demoted — or whose account had been disabled — therefore
> kept administrative access until that token expired. This affected every installation, including
> single-user ones, though it required someone to have held admin rights in the first place. The
> check now reads the account directly.
>
> **Two-factor codes could be guessed at without limit.** The screen that accepts the six-digit code
> had no attempt limit, unlike the password screen beside it. It now does, counted per account so
> that changing network address does not reset it. Account creation and directory sign-in gained the
> same protection.
>
> **Self-registration was switched on by default and never closed.** On a personal machine this only
> matters to someone already sitting at it, because HARBOUR listens only to that computer. On a
> networked or server installation it meant anyone who could reach the address could create an
> account. New installations now close registration once the first account exists. ⚠️ **Existing
> installations are deliberately left exactly as they were** — we will not change how your team signs
> in underneath you.
>
> **And administrators could not create accounts at all.** There was no such function; the only route
> to an account was for the person to register themselves. This one is a reliability fault rather
> than a security one, but it mattered most where security was tightest: in appliance mode, with
> self-registration off, no second account could ever be added. **Admin → Users → ADD A USER** now
> exists. If this has affected your deployment, please contact us and we will help.
>
> All fixes ship in **v1.3.18**. ⚠️ Linux-only at the time; the Windows installer stayed at v1.3.15.
> **Windows caught up in v1.3.19 on 31 August 2026** and now carries all of these fixes.


Thank you for helping keep HARBOUR AI and its users safe.
