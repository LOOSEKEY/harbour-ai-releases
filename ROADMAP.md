# HARBOUR AI — Public Roadmap

Current version: **v1.3.21** — released 12 September 2026
*(Windows and Linux, built locally, shipping together)*

---

## Distribution Status

| Platform | Status |
|---|---|
| Linux AppImage | ✅ Available |
| Linux .deb | ✅ Available |
| Windows EXE | ✅ Available |
| Windows Portable | ✅ Available |
| HARBOUR AI Box (appliance) | ✅ Available — pre-configured on hardware; HARBOUR OS installer on request |
| macOS DMG | 🔶 In progress — coming soon |
| Flathub | 🔶 Submission pending |
| Microsoft Store | 🔶 In progress |

---

## The Platform — v1.3.21

HARBOUR AI is a private, multi-agent AI platform that runs **entirely on your own hardware** — no
cloud, no telemetry, no subscription. What's in the box today:

- **150+ specialist business modules** across legal, accounting, HR, healthcare, recruitment,
  education, planning, charity, financial services and compliance
- **Trust Layer (complete)** — cryptographic proof of what your AI did:
  - Signed AI receipts on every response — verifiable offline, in any browser
  - Tamper-evident, hash-chained audit ledger
  - Encrypted secrets vault (AES-256-GCM)
  - Prompt-injection firewall + output guardrails
  - Built-in e-signature, consent platform and bias auditor
  - Content credentials on generated outputs
- **Full UK GDPR compliance suite** — DPIA, RoPA, PII redaction, ICO breach workflow
- **Sector packs** — conveyancing, insurance, recruitment, property lettings, dental, veterinary,
  pharmacy, opticians, construction, hospitality, logistics, manufacturing and funeral services,
  on top of the core legal, NHS, accountancy, HR and education suites
- **Integrations** — Open Banking (15 UK banks), NHS FHIR R4, Enterprise SSO (SAML 2.0 / OIDC), MCP
- **Productivity** — Company Brain knowledge graph, meeting intelligence, workflow recorder, voice & vision
- **OpenAI-compatible REST API** — plug HARBOUR AI into your existing tools, all running locally
- **Deployment options** — install on your own Windows/Linux machines, or run it as the **HARBOUR AI Box**: a turnkey appliance (HARBOUR OS, Ubuntu-based) we or a partner pre-configure and ship to your organisation — ideal for NHS and other regulated environments. Self-install HARBOUR OS image available to IT teams on request.

---

## Coming Up

### Near term
- macOS DMG (signed, notarised)
- Flathub listing
- Microsoft Store listing

### Medium term
- External cryptography review of the Trust Layer
- G-Cloud registration (UK public-sector procurement)
- NHS and local-government pilot programme

### Longer term
- ARM / Raspberry Pi builds
- Multi-machine / federated deployment for larger organisations

---

## Changelog

### v1.3.21 — 12 September 2026

**The buttons that were pressing back.**

Every place the interface calls the engine was tested against a running copy, as a logged-in user.
Three features turned out to be wired to nothing at all.

- 🗂 **The Company Knowledge Base had not worked since 22 May.** You could open it, add a document
  and see no error — and nothing was ever stored. The part of HARBOUR that receives the upload had
  been removed during an internal reorganisation and never put back, and because a failed upload
  looks exactly like an empty knowledge base, it went unnoticed for nearly four months.
  ⚠️ *If you added documents during that time they were not kept. Please add them again.*
  Per-agent knowledge bases were never affected.
- ☁️ **"Disconnect" on a cloud drive did not disconnect.** The drive vanished from the screen while
  the server kept its access to your account, and a reload brought the connection back. It now
  genuinely revokes access. For a product built on your data staying where you put it, that one
  mattered most.
- 🔑 **A cloud AI provider key pasted during first-run setup was silently discarded.** If you set one
  up and it never seemed to take, that is why. It is saved properly now, encrypted, and tells you if
  it cannot be. **Claude can also now be chosen as the provider for all agents**, which was
  documented but not actually accepted by the app.
- ⚖️ **Data Subject Access Requests failed on every attempt** — a GDPR tool with a statutory 30-day
  deadline. Fixed, along with eighteen related faults that were failing *silently*, the worst of
  which meant **AI Director board packs were being written from none of your actual figures**.
- 📸 Webcam and pasted-image analysis, reseller key generation and tenant invites all work again.

**Security.** EMMA monitors have always been private to the user who created them; the alerts those
monitors *produce* were not. On an installation with more than one account, any user could read
another's alerts — including the summary of whatever file or page the monitor was watching — and
mark or delete them. Found in our own monthly review, proven with two ordinary accounts, and fixed
the same day; existing alerts are kept and returned to their owners on update. Nothing was ever
reachable from another machine. Separately, **a password reset now ends sessions opened with the old
password**, which previously survived for up to seven days.

The PDF parser that reads your uploaded documents is updated for three security advisories.

### v1.3.20 — 4 September 2026

**Recovery, and the tools that were never reachable.**

- **Backups were being written to a temporary folder.** In every built installer the backup
  location resolved to a system temp directory — cleared on restart on most machines, and held
  in RAM on many — so a backup could be gone before you needed it, while the app reported
  success and listed the file. Nothing ever ran a backup automatically either, and there was no
  restore at all. Backups now live beside your data, run nightly, are taken through SQLite's
  online backup API so a snapshot made while you work is consistent, and **can be restored** —
  administrator-only, refusing any backup that fails an integrity check and taking a safety copy
  of your current database first.
  ⚠️ *If you are updating from an earlier build, take a fresh backup — older ones have most
  likely gone.*
- **A locked-out administrator can get back in.** Administrator could previously be granted only
  to the first account ever created and never again, so a forgotten password permanently removed
  every admin feature from your own machine. The role can now be granted, the last administrator
  cannot be removed by accident, and there is a local recovery path: a single-use code written
  into your HARBOUR data folder, usable only from the machine HARBOUR runs on, expiring in 15
  minutes and never sent anywhere. See the manual, *If you are locked out*.
- **Email addresses are validated**, and confirmed by email where you have SMTP configured. If
  you have no mail server — normal for a desktop install — nothing changes and nothing blocks.
  Existing accounts are unaffected.
- **35 sector tools that appeared but never worked.** Every dental, veterinary and pharmacy tool
  past the first four opened a form, accepted input and failed with "Generation failed" — Yellow
  Card reports, emergency supply documentation, controlled-drugs records, sedation consent,
  safeguarding notes. All now work.

Test suite 469 → 508. Built locally on both platforms.

### v1.3.19 — 31 August 2026
**The runtime that was never shipped.** HARBOUR's backend relies on a Microsoft system component —
the Visual C++ runtime — and our Windows installer never actually installed it. Most Windows
machines already have it, because a great many programs put it there, which is why this went
unnoticed for so long. On a machine that did not have it, HARBOUR did not start at all.

Three things changed. The installer now installs that component if it is missing. The application
also carries its own copy, which is what makes the **portable** version work on a machine you are
not allowed to install anything on. And a fault that made the whole backend stop has been contained,
so a missing component now costs you dictation rather than the entire product.

**If HARBOUR has ever failed to start for you on Windows, this is the release that fixes it.**

This also brings Windows back into step with Linux for the first time since v1.3.15, so Windows
users receive everything from v1.3.16, v1.3.17 and v1.3.18 in one update.

### v1.3.18 — 27 August 2026
**The front door.** Four fixes to how HARBOUR handles sign-in and accounts, all found by our own
review of the code rather than by any report from a customer.

**Removing someone's admin rights now takes effect immediately.** Previously the check read the
permissions recorded in your sign-in token, which is valid for seven days — so an administrator who
had been demoted, or whose account had been disabled, kept their access until that token expired.
The check now reads your account directly, so a change applies on the very next action.

**Two-factor codes can no longer be guessed at indefinitely.** The six-digit code screen had no
limit on attempts. It does now, counted per account so that changing network address does not reset
it. Account creation and directory sign-in are limited in the same way.

**On a new installation, self-registration closes once the first account exists.** Until now the
REGISTER button stayed available forever, which is reasonable on a personal laptop but not on a
server anyone can reach. ⚠️ **Existing installations are unaffected** — if self-registration was
open for your team, it stays open, and nothing about how you add people changes.

**Administrators can now create accounts directly**, at **Admin → Users → ADD A USER**. This was
genuinely missing: there had been no way to add someone without them registering themselves. If you
run HARBOUR in appliance mode, where self-registration is switched off, this is the change that
makes additional accounts possible — we are sorry it took this long.

Also fixed: on the sign-in screen, the "Sign in with work account" button for organisations using
single sign-on was never displayed, because the setting that controls it was only ever read *after*
signing in.

⚠️ **v1.3.18 was a Linux-only release.** Windows caught up in v1.3.19 on 31 August 2026.

### v1.3.17 — 24 August 2026
**Report emails now go through your own mail server. Nothing else.**

While reviewing the code that sends scheduled reports, we found it contained a path to send them via a
third-party email service. **It could never have run in any version you have ever installed** — it
required a setting we have never shipped and have never set — and we verified that no customer data
has ever gone through it.

We removed it anyway, and we want to be plain about why. A promise that your data stays on your
machine should not rest on a setting staying switched off. Worse, the interface actively suggested you
could switch it on, which is the opposite of how we want to treat a decision about your data. Report
emails now go through **your own mail server**, configured by you, and nowhere else. If you have not
set one up, HARBOUR tells you so rather than quietly finding another route.

We have also added an automated check that fails our build if any third-party email service is ever
referenced in the code again, so this cannot come back by accident.

### v1.3.16 — 24 August 2026
**A shared-installation fix, and five email features that had never worked.**

From our monthly security review, which this month looked at the parts of HARBOUR that run on a
schedule in the background rather than the parts you click.

**The access-control fix.** If you had not set up your own Companies House API key, HARBOUR would fall
back to looking for a shared one. But every stored key belongs to an individual account, so on an
installation with more than one account that fallback could return **another user's key** — showing
part of it, and making lookups that counted against their allowance. **If you are the only account on
your HARBOUR, this did not affect you**; there is no second account for it to find. The fallback is
gone: a key belongs to the person who entered it.

**The five features that had never sent an email.** The daily briefing, the monthly board pack, the
weekly health digest, candidate acknowledgements and invoice chasing all send email. None of them
could. They were reading your mail settings from the wrong place, finding nothing, and stopping
without saying so — while the settings screen reported itself as configured. This had been true since
those features shipped.

They work now. Just as importantly, they no longer fail silently: if mail cannot be sent, HARBOUR says
so in its log rather than pretending it succeeded. If you had given up on these features, it is worth
setting your mail details again under Settings → Integrations → Email.

⚠️ **v1.3.16, v1.3.17 and v1.3.18 were Linux-only releases.** The Windows installer stayed at
v1.3.15 throughout. **Windows caught up in v1.3.19 on 31 August 2026**, which delivers all three.

### v1.3.15 — 10 August 2026
**A fix for shared installations: live collaboration sessions are now properly private.**

This came out of our monthly security review rather than a customer report.

HARBOUR has a real-time collaboration feature: open a session and other people working in it see who
is present and what is being said as it happens. The part that checks *who you are* worked correctly.
The part that should have checked *whether the session you asked for is actually yours* was missing.
On an installation with more than one account, that meant a signed-in user who named someone else's
session could join it — seeing who was in it and the messages passing through it while they were
connected, and able to send messages into it.

**If you are the only account on your HARBOUR, this did not affect you.** There is no second user to
be a stranger, and nothing here is reachable from outside your machine — HARBOUR's engine only listens
locally. Nothing was sent anywhere and nothing left your machine. This also only ever concerned live
traffic while connected: it was not a way to read stored conversation history, which has been properly
separated per user since v1.3.5.

Our July review tested every real-time connection for whether it accepts a valid sign-in and refuses
an invalid one, and all of them passed — that part was sound. This review asked the next question:
having established who someone is, does the connection also check that what they asked for belongs to
them? That question had not been asked of these connections before, and for this one the answer was
no. Ownership is now checked by the same single piece of logic the rest of the app already used, and
we have added an automated guard that fails the build if a future real-time feature is added without
that check.

Also in this release: an update to the library HARBOUR uses to read PDFs, closing two reported issues
where a deliberately malformed PDF could consume excessive memory or time while its text was being
extracted.

If you are running v1.3.15 or later you have this; auto-update will bring it to you.

### v1.3.14 — 1 August 2026
**HARBOUR now works even when another program is using its port.**

HARBOUR's engine runs on your own machine and, until now, insisted on one specific port: 8000. That
is a popular port — local web servers, developer tools and Docker containers commonly take it — so on
a machine where something already had it, HARBOUR's engine could not start at all.

There was a worse version of that. The app assumed anything answering on that port was its own engine,
without checking. So if another program was sitting there, HARBOUR would load *that program's* page
inside the HARBOUR window. To be clear about what this was and was not: both programs were already
running on your own computer, nothing was sent anywhere and nothing left your machine. But a window
with our name on it should never show you someone else's application, and it will not again.

Three changes. The engine now looks for a free port instead of giving up. The app checks that whatever
answers really is HARBOUR before it loads anything, and if it is not, it refuses and tells you what is
in the way rather than showing it to you. And the app no longer has a port written into it anywhere,
so it is correct wherever the engine ends up.

One side effect worth knowing: if HARBOUR does end up on a different port, your saved sign-in does not
follow it, so you will be asked to log in again and your theme returns to the default.

If you are running v1.3.14 or later you have this; auto-update will bring it to you.

### v1.3.13 — 30 July 2026
**Tighter limits on what an agent's tools can reach.**

A customer asked a precise question: the Trust Layer includes an injection firewall, so if a prompt
injection made an agent try to call a tool with harmful arguments, what actually stops it?

The honest answer is that the firewall is not the thing that stops it. The firewall reads untrusted
content — web results, scraped pages, your documents — and strips hidden instructions before the
model ever sees them, which makes a harmful call less likely to be produced in the first place. What
actually *stops* one is the tools themselves refusing to trust whoever called them: only registered
tools run, only the arguments a tool declares are passed to it, terminal commands never go through a
shell and must be on a fixed list of read-only utilities, file access is confined to permitted
folders, and network fetches refuse private addresses.

Answering that question properly meant re-reading that code rather than the feature list, and it
turned up gaps worth closing. Folder confinement is now enforced however a path is written — including
paths relative to your home folder, and paths that reach outward through a shortcut — and a few
allowed commands that could be persuaded to start *other* programs no longer can.

Nothing you could do before has been taken away: reading and searching your own documents through an
agent works exactly as it did.

Two things worth stating plainly. This confines the agent within your own user account — it is not a
sandbox escape barrier, and the container image is the answer if you need isolation at that level.
And if you are running v1.3.13 or later you have the fix; auto-update will bring it to you.

### v1.3.12 — 29 July 2026
**When a voice feature refuses to connect, it can now tell you why.**

If your session had quietly expired, clicking the dictation microphone did nothing at all — no
message, no explanation. The app had always been *trying* to say "please log in again"; the message
just never made it out. The refusal was being sent in a way the browser could not read, so the app
received an unexplained failure and showed you nothing.

That is fixed for every real-time feature: dictation, live voice, live meetings, the computer
operator, and collaborative documents. When one of them turns a connection away you now get the
actual reason.

Behind it, all six of those connections were audited end to end for the first time — each one
checked that it accepts a valid session, and equally that it refuses an invalid one. All six passed.
We have also added automated guards so this class of fault is caught before a release rather than by
someone clicking a button that does nothing.

### v1.3.11 — 29 July 2026
**The message box holds more than one line now.**

Press **Shift+Enter** and you get a new line. The box grows as you type — up to about eight lines,
then it scrolls — and shrinks back when you send. Enter still sends, as always.

**Pasting keeps its shape.** Until now the message box was a single-line field, so anything you
pasted had its line breaks quietly turned into spaces: a multi-paragraph brief arrived as one long
run-on, and a code snippet lost its indentation. Paste now survives intact.

This also quietly fixes the document scanner. When OCR hands its text to the chat, it formats it with
blank lines between the instruction and the scanned text — and those were being stripped before the
AI ever saw them. That handoff now arrives as intended.

For long documents, attaching (📎 or drag-and-drop, see v1.3.10) is still the better route: an
attachment is parsed properly rather than pasted in as plain text.

### v1.3.10 — 29 July 2026
**You can drag a document straight into the chat. You could always — we just never showed you.**

Dropping a file onto the chat panel has worked for a long time, but it gave you no sign it was
possible: no highlight, no cursor change, nothing. So essentially nobody used it. (We only noticed
because it got suggested as a *new feature to build* — by the people who wrote it.)

Now, when you drag a file over the chat, the panel turns green and says **DROP TO ATTACH**, with the
formats it accepts. Let go and it's attached. Dragging ordinary selected text around the page won't
trigger it — only real files.

**Dropping several files at once no longer loses them quietly.** It used to attach the first and
discard the rest without saying anything, so three dropped contracts became one with no warning.
HARBOUR still takes one document at a time, but now tells you exactly which ones it skipped.

Worth knowing: attaching beats pasting for anything long. The message box is a single-line field, so
pasted line breaks flatten into spaces — fine for a sentence, poor for a contract or a code snippet.
An attachment is parsed properly and keeps its structure. The manual on the website now covers all of
this; it previously had no attachments section at all.

### v1.3.9 — 28 July 2026
**The manual now matches the app — and fixing it turned up a bug that was eating chats.**

The user manual had not been properly updated since v1.0.140, fifteen releases ago, and it showed.
It still described the old 84-button toolbar that was replaced by the ☰ WORKSPACE / ⚙ SYSTEM menus
and Ctrl+K search back in v1.2.0. Worse, around 55 sections told you to open panels that have never
existed — an "M-SERIES panel", a "TOOLS › REDACT" menu. Those features are real and working; the way
you reach them is to **ask EMMA in plain English**, or call them from the API. Every one of those
sections now tells you which.

Newly documented, having shipped without ever making it into the manual: the **self-test** (which
proves each feature works on your own machine rather than just pinging it), the **problems tray**,
the **egress meter and its kill-switch**, **signed data-residency attestation**, **day mode and the
six colour palettes**, **UI scale**, and eleven panels including Invoices, Phone Receptionist,
Meeting Capture, Cloud Drive Sync and Whistleblowing.

**🐛 The bug.** Writing up the keyboard shortcuts meant reading the code behind them, which is how we
found that **Ctrl+K was doing two things at once**: opening the command palette, *and* clearing the
current chat — including deleting it from disk, with no confirmation. It only happened when your
cursor wasn't in the message box, which is exactly why it had gone unnoticed. If you have ever had a
conversation vanish on you, this was almost certainly why. It is fixed: Ctrl+K opens the palette and
nothing else. Clearing a chat is the 🗑️ button beside the message box, as it always was.

Checking that fix in a real browser turned up a second one: **Ctrl+/ had never focused the message
box** in any language. Also fixed.

### v1.3.8 — 28 July 2026
**Windows, verified on real Windows.**

v1.3.7's Windows installers were built by our CI but had never actually been run on a Windows
machine — only the Linux build had. Both were installed on a clean Windows 11 machine and taken
through the whole path: install, activate, 14-day trial, register, full cockpit.

The standard installer passed end to end. The **portable build** did not, and it exposed a real
bug: on its *first* launch it showed a fatal "HARBOUR AI Offline" error while the backend was still
starting up perfectly normally. It now waits properly and retries before reporting any problem —
fixed, rebuilt, and re-verified by downloading the published file and running it again.

*Note for portable users:* the portable build stores its data in the same place as an installed
copy, so the two share a database on the same machine.

### v1.3.7 — 27 July 2026
**Three small bugs, fixed the same night they were found.**

**The microphone button in the chat box now works.** Clicking it previously did nothing —
silently, with no error — since a very early version of HARBOUR. It now uses the same
local speech pipeline as Live Voice. Alongside it, a privacy fix: the speech-recognition
engine was checking online for its own updates every time it started, even though it runs
entirely on your machine. It no longer does.

**The webcam feature could occasionally show a message from an oddly-named placeholder
"agent" instead of a real one.** Fixed to always use a real agent.

**HARBOUR could occasionally insist on the wrong date.** The "save to memory" button saves
a reply as a fact HARBOUR remembers about you going forward. A small number of saved facts
turned out to be old, incorrect statements about the date — which were then being trusted
over the actual current date. HARBOUR no longer saves, or trusts, a "fact" that is really
just a stale snapshot of the date and time.

### v1.3.6 — 27 July 2026
**Your assistant has a real voice, and document search now works in the installed app.**

**EMMA speaks properly now.** A natural British voice, generated entirely on your own machine —
no cloud service, nothing sent anywhere, and no extra software to install. It works offline like
everything else, and speech is produced roughly twice as fast as it plays. If you use HARBOUR on
Linux and had no spoken replies at all, that is why: the old voice relied on a system component
many Linux machines do not include. The new one needs nothing.

**Document search works in the installed app.** This one is worth being straight about. HARBOUR's
document features worked when run from source, but the packaged application was missing a
component they depend on — so uploading a document to the installed app failed. It was found by
running the new **Self-test** panel against the published release rather than against a
development machine, which is exactly the sort of gap it was built to catch. Uploading, searching,
the Company Knowledge Base and Cloud Drive Sync all work now.

Your existing documents are unaffected. The change was verified to produce identical results to
the previous method before it was made, precisely so that nothing already indexed would need
rebuilding.

**Also fixed.** Installing a model from inside the app used to report success even when the
download had failed — it now checks, and tells you what actually happened. Deleting a model never
actually removed it, despite saying it had.

**Privacy.** Two components were reaching the network without needing to: a database library with
usage telemetry switched on by default, and the search model checking for updates on every start.
Both are gone. The "0 bytes sent externally" meter is now literally true from a cold boot.

**The download is bigger — around 640 MB, up from 320 MB.** The AI models for document search and
speech now ship inside the installer instead of being missing or fetched later. Nothing is
downloaded behind your back, and everything runs offline.

### v1.3.5 — 27 July 2026
**The release that made the features already there actually work.** A full review of the codebase
asked why the last few releases had each been "a feature that never ran at all", and found the
same cause underneath every one: the groundwork was built, and the code that was meant to use it
never was. Nine more instances of that turned up. These are the ones you'll notice.

**HARBOUR was throwing away most of what you asked it.** The setting that tells the local AI
engine how much it may read was never actually sent, so the engine fell back to a small default
and **discarded 52–76% of every prompt — starting from the top**, which is exactly where your
Company Knowledge Base and your uploaded documents were placed. That is the "it ignores my
documents" complaint, and it was real. HARBOUR now sizes this from your machine's own memory, and
when something genuinely will not fit it trims the least important part and tells you, rather than
letting the engine silently cut the top off.

**Half of every document you uploaded could not be found by search.** Documents were being split
into pieces larger than the search index can actually read, so roughly **38% of the text in every
file was stored, shown to you, and never searchable**. Now none of it is lost. Search is also
better at the things it used to be worst at — invoice numbers, clause references, case numbers,
surnames — because it now matches exact terms alongside meaning. If you have documents indexed by
an older version, the Documents panel will offer you a one-click **Re-index**.

**Cloud Drive Sync had never indexed a single file.** If you connected OneDrive, SharePoint or
Google Drive, it reported success every 30 minutes and did nothing at all. Fixed.

**Errors are no longer silent.** When something failed, HARBOUR often showed you an empty panel
rather than a problem, which is how several broken buttons went unnoticed for weeks. Failures now
appear as a plain-English message and are collected in a **Problems** list you can copy and send
us.

**A new Self-test panel** (System ▸ Diagnostics) checks that each part of HARBOUR genuinely works
on *your* machine — it indexes a real document and searches for it back, asks the model a real
question, encrypts and decrypts a real secret — and gives you a pass/fail grid plus a support
bundle you can read before sending. Everything stays on your machine.

**Security.** This release also completes a full security review — a dependency audit, static
analysis, and live attack testing against a running instance. Runtime defences all held. Two
issues in HARBOUR's own code were found and fixed, the more significant being an **access-control
fault on multi-user installations**: on an instance with more than one account, a signed-in user
could reach data belonging to another user of the same machine. **Single-user installations were
not affected in practice.** Dependencies with available fixes were updated at the same time. If
you run HARBOUR with more than one account, please make sure you are on v1.3.5.

### v1.3.4 — 20 July 2026
**Twenty buttons that quietly did nothing now work.** Creating a new session, deleting one,
exporting a conversation, clearing chat history, creating or removing an agent, summarising a
session, image analysis, creating and assigning jobs, creating schedules, creating or revoking API
keys, running a backup or HDD mirror, and reloading plugins were all sending requests without your
login attached — so they failed quietly, usually showing nothing at all.

Chat itself was never affected, which is why this went unnoticed: the thing you use every day
worked fine while the buttons around it didn't. Creating a new session was doubly broken — it also
sent an incomplete request.

Every screen in the app has now been checked against the server, one call at a time, and an
automatic check was added so this cannot creep back in.

### v1.3.3 — 20 July 2026
**The wake phrase now runs entirely on your machine.** Saying "hey emma" previously used your
browser's built-in speech recognition, which sends microphone audio to an online service. That
isn't how HARBOUR should work, so it's gone.

The wake word now uses the same local speech engine as Live Voice: your microphone, the
transcription, the reasoning and the reply all stay on your computer. Anything you say that
doesn't contain your wake phrase is discarded immediately — it never reaches the AI, your
conversation history, or your disk.

Because it shares the Live Voice pipeline, wake-word commands can now also *do* things and answer
you out loud, which the old version could never do. Your wake phrase is configurable as before.

### v1.3.2 — 20 July 2026
**Voice repair — and EMMA can now act on what she hears.** Live Voice (the always-on
conversation mode) had never actually connected, and the wake-phrase button couldn't work in the
desktop app. Both are fixed, and voice now runs tools: ask out loud and EMMA can check real system
state and answer you, all locally — microphone, transcription, reasoning and speech never leave
your machine.

For safety, actions that change your machine (running commands, writing files) are deliberately
**not** available by voice — speech recognition can mishear, so those stay in the chat box where
you see the exact words first.

Also fixes Deep Research reports, which were rendering with stray characters through the text.

*Voice quality itself is the next step: the natural-sounding neural voice is still to come.*

### v1.3.1 — 20 July 2026
**The data-loading patch.** Some saved data wasn't showing up in the app. Your session tabs, jobs,
schedules, API keys and plugins were being requested without your login token attached, so they came
back empty — most visibly, the session bar showed a single blank session instead of your real
conversations after restarting.

**Nothing was ever lost.** Everything stayed safely in your local database the whole time; the app
just couldn't display it, and Conversation Search could always still find your history. This release
reconnects them. Also fixes the sector recipe cards not appearing on the start screen until you
pressed reload.

### v1.3.0 — 16 July 2026
- **A proper night/day toggle.** HARBOUR now has a real light mode as well as dark — one click in the top bar. Day mode is a genuine light theme, not a dark theme with the colours flipped: text stays crisp and readable on light panels, and the important signals (red for errors, green for success, amber for warnings) stay exactly where you expect them.
- **Pick your palette.** A new palette picker lets you choose the whole cockpit's colour family — **Neutral, Ocean, Teal, Amber, Rose or Violet** — separately from night/day. That replaces the old flat list of 16 themes with something that actually makes sense: choose a mood *and* a light/dark mode, independently.
- **Your current look is safe.** If you'd already picked one of the old themes, HARBOUR maps it to the closest new palette automatically, so you reopen to the look you chose — nothing changes under you. And in night mode the app looks identical to before, down to the pixel.
- **The colours are now consistent everywhere.** Under the hood, ~2,000 hardcoded colours were moved onto one shared system, so the whole app re-colours together — no more panels that look slightly off. Every text-and-background pairing is checked against accessibility contrast standards.

### v1.2.0 — 15 July 2026
- **The toolbar is fixed.** The row of toggles across the top had grown to 84 buttons on one line, with a scrollbar you had to drag sideways to reach the ones at the end. It's now **8 buttons you actually use mid-conversation**, plus two tidy menus: **☰ WORKSPACE** for the things you *do*, and **⚙ SYSTEM** for the things you *set up or govern*. The sideways scrollbar is gone.
- **Nothing was taken away.** Every panel and tool you had is still there — now grouped under a clear heading and findable by name instead of hidden behind a drag. WORKSPACE covers Chat & Session, Knowledge, Research, Agents & Automation, Business, Meetings and Create; SYSTEM covers Models, Governance, Account, Connections and Display.
- **The menus and Ctrl+K always agree.** Both are built from the same list, so anything you can reach in a menu you can also jump to by typing — and the two can never fall out of step as HARBOUR grows.
- The rest of the app is unchanged, and everything from v1.1.0 and v1.1.1 carries forward.
- *Next up: a proper night/day toggle and a set of colour palettes to pick from.*

### v1.1.1 — 13 July 2026
- **Security & stability update.** A full end-to-end check of the running app plus the monthly security scan. Everything from v1.1.0 stays the same — no features changed.
- **Security** — three third-party components with newly published advisories were updated to their fixed versions, including one that removes a way a specially crafted PDF could tie up your processor while its text was being read. All the app's own protections (sign-in, admin access, injection and path-traversal defences) were re-checked against a live instance and hold.
- **Fixes** — using web search in chat could return an error on some turns; that's fixed. The assistant's built-in tools now run reliably instead of occasionally being skipped, and EMMA's autonomous "agentic" mode now stops as soon as it has your answer instead of wandering.

### v1.1.0 — 7 July 2026
- **Biggest feature release since launch — ~80 new capabilities.** HARBOUR came out of maintenance mode and shipped a major update, all running entirely on your own machine.
- **Deeper sector tools** — the professional packs now cite the actual UK rules they rely on, include real calculators (e.g. NHS dental UDA bands, BNF drug-interaction checks), chain into multi-step case workflows, and keep first-class case records linked to your Company Brain.
- **New compliance & sovereignty suite** — one-click signed "no data left this machine" attestation for any date range; automated-decision explainability with a human-review workflow; an air-gapped edition (offline licence + USB-verified updates); and a live counter in the cockpit showing bytes sent externally (0 when fully local) with an optional kill-switch.
- **Business intelligence** — negotiation rehearsal, synthetic test-data generation, point-in-time "what did this say on date X" knowledge, a privacy-preserving data clean room, a live business digital twin, a claim-checking truth engine, and full source provenance.
- **Professional packs** for regulated work — safeguarding, AML/SAR, criminal defence, probate, insolvency and immigration assistants (each assists a qualified professional, never replaces them).
- **Easier to use** — a Ctrl+K command palette to jump anywhere, an in-app help that answers "how do I…?" fully offline, first-run "fits your machine" model badges, interface scaling and more colour themes.

### v1.0.143 — 4 July 2026
- Improved — **honest offline/online status.** When you ask an agent whether it's offline, it answers truthfully: fully offline by default, and — on a turn where *you* switched on web search — it now says plainly that those specific results were fetched from the web over your connection. Its reasoning still runs entirely on your machine, and nothing else ever leaves your device.

### v1.0.142 — 4 July 2026
- New — **ask EMMA to run the platform for you.** 41 built-in tools now let you drive HARBOUR from plain language in chat — draft a DSAR or breach response, value a business, forecast cashflow, prepare VAT/ITSA figures, translate, compare documents, check an IR35 status, look up Companies House and more, without hunting for the right panel. Every action still runs under your own login with full audit, and tools only draft and analyse — nothing is sent or filed on your behalf.

### v1.0.141 — 3 July 2026
- Improved — images EMMA finds on the web now appear **inline** in chat instead of as plain links.
- Fixed — copy and paste restored in the desktop app (Edit menu + right-click).

### v1.0.140 — 21 June 2026
- Stability — final stabilisation release closing out the platform build. Internal code clean-up and a startup reliability fix, with new automated checks to keep startup healthy. No change to features.

### v1.0.139 — 15 June 2026
- New — self-evolving assistant (opt-in, off by default): learns from how you work and *suggests* new agents and workflows for you to approve. It never changes itself silently.

### v1.0.138 — 15 June 2026
- Reliability — full end-to-end test of every endpoint; fixed two edge-case errors (invoice chaser and scheduling).

### v1.0.137 — 15 June 2026
- New — smarter, faster answers (automatic model routing, response caching, self-critique, built-in evaluation).
- New — 9 more sector packs (dental, veterinary, pharmacy, opticians, construction, hospitality, logistics, manufacturing, funeral).
- New — everyday tools (slides, spreadsheet AI, handwriting OCR, whiteboard-to-notes, data lineage, auto-classification, vendor risk, board packs) and a confidential whistleblowing portal.

### v1.0.136 — 14 June 2026
- Reliability — fixed several panels (Companies House, charts, kiosk, team management) that could error on a brand-new install
- Quality — added an automated test gate so every release is checked before it ships

### v1.0.135 — 14 June 2026
- Security hardening — tightened authentication on the OpenAI-compatible API
- Fixed Projects setup on fresh installs
- Smarter default-model selection
- Stability and test-coverage improvements

### v1.0.131–134 — 12 June 2026
- **Trust Layer complete (M0–M5)** — signed AI receipts, tamper-evident audit ledger, encrypted
  vault, prompt-injection firewall, e-signature, consent platform, bias auditor, content credentials
- MSP console — per-tenant guardrails, fleet control, signed remote lock/wipe, per-agent RBAC
- Sector packs — conveyancing, insurance, recruitment, property lettings
- Workflow Recorder — turn any task you do once into a reusable workflow
- First-run fix — default model now matches the install instructions

### v1.0.128 — 8 June 2026
- HARBOUR Box — plug-in private AI appliance for UK organisations
- Pricing: Solo £149, Business £999, Reseller £2,499, Enterprise £9,999+

### v1.0.127 — 7 June 2026
- AI Video Interviews — automated candidate screening with scoring
- Client Sentiment Monitor — weekly digest, at-risk flagging
- Knowledge Decay Alerts
- Advanced Regulatory Horizon Scanning
- HARBOUR CARE annual plans

### v1.0.119 — June 2026
- Enterprise SSO (SAML 2.0 / OIDC)
- Open Banking — 15 UK banks
- NHS FHIR R4 APIs
- Always-On Background Monitors

---

*For support or enterprise enquiries: Gregorymoores@proton.me*  
*Website: [harbour-ai.co.uk](https://harbour-ai.co.uk)*  
*Community: [Discord](https://harbour-ai.co.uk/discord)*
