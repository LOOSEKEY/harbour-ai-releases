# HARBOUR AI — Public Roadmap

Current version: **v1.3.4** — released 20 July 2026

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

## The Platform — v1.3.4

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
*Community: [Discord](https://discord.gg/eGtd6Wsh)*
