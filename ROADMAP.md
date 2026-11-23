# HARBOUR AI — Public Roadmap

Current version: **v1.3.40** — released 23 November 2026
*(Windows and Linux; macOS added 13 November 2026)*

---

## Distribution Status

| Platform | Status |
|---|---|
| Linux AppImage | ✅ Available |
| Linux .deb | ✅ Available |
| Windows EXE | ✅ Available |
| Windows Portable | ✅ Available |
| HARBOUR AI Box (appliance) | 🔶 Pilot — x86-64 installer exists, needs internet during install, not yet shipped to a customer |
| macOS DMG | ✅ Available since v1.3.31 — Apple Silicon (M1+), macOS 14+; not yet Apple-signed (first launch: Open Anyway) |
| Flathub | ❌ Dropped (1 Oct 2026) |
| Microsoft Store | 🔶 In progress |

---

## The Platform — v1.3.40

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
- **Integrations** — Xero / QuickBooks / Sage, HMRC MTD, Cloud Drive Sync (OneDrive, SharePoint, Google Drive), Enterprise SSO (LDAP + SAML 2.0), MCP. Bank transaction analysis and NHS FHIR records work on local data; neither connects to banks or NHS systems
- **Productivity** — Company Brain knowledge graph, meeting intelligence, workflow recorder, voice & vision
- **OpenAI-compatible REST API** — plug HARBOUR AI into your existing tools, all running locally
- **Deployment options** — install on your own Windows, Linux or Mac machines, or run it as the **HARBOUR AI Box**: a turnkey appliance (HARBOUR OS, Ubuntu-based) we or a partner pre-configure and ship to your organisation — ideal for NHS and other regulated environments. Self-install HARBOUR OS image available to IT teams on request.

---

## Coming Up

### Near term
- macOS: Apple Developer signing + notarisation (then updates install themselves on a Mac too)
- Microsoft Store listing

### Medium term
- External cryptography review of the Trust Layer
- G-Cloud registration (UK public-sector procurement)
- NHS and local-government pilot programme

### Longer term
- ARM / Raspberry Pi builds
- Multi-machine / federated deployment for larger organisations

---

## Changelog — latest release

### v1.3.40 — 23 November 2026

**The phone receptionist works, plus security fixes.**

- 📞 The Phone Receptionist panel saves your Twilio details and has an Answer calls switch; before, it couldn't be switched on. Every call is checked as really coming from Twilio.
- 🔐 Cloud Drive Sync needs an administrator or reviewer, because synced files go into company knowledge.
- 🛑 The kill-switch that refuses outbound requests stays on after a restart.
- 🔧 Fixed: the daily briefing's renewals and at-risk clients, the cashflow forecast's dates and sums, and three screens that ignored synced accounting data.
- 🍎 Mac: this release carries the v1.3.34 Mac app until the next Mac build is ready.

---

### v1.3.39 — 23 November 2026

**MSP tenants keep client firms apart.**

- 🏢 On an install that serves several client organisations, each one's company knowledge, phone calls, WhatsApp messages, consent register, signed documents and chargeback departments now stay with that organisation. Before, staff in one tenant could see another's.
- 🔐 A tenant invite can give the user or power user role, never administrator of the whole install.
- 👌 Installs without tenants work exactly as before.
- 🔧 Fixed: the cashflow forecast (it failed with an error), the daily briefing's outstanding invoices (always "Data unavailable"), and alerts from six features (cashflow, pricing scans, client sentiment, regulatory watch, scheduled compliance reports, knowledge decay), which failed the moment they had something to report.
- 🍎 Mac: this release carries the v1.3.34 Mac app until the next Mac build is ready.

---

### v1.3.38 — 23 November 2026

**Every panel matches the new layout.**

- 🎨 In the new layout, the panels and menus that open from the sidebar, Settings and Ctrl+K (admin, Trust, Tenants, integrations, the business tools and the rest) now use readable text, sentence-case labels, proper inputs, dropdowns and buttons, and the new colours, in day and night.
- 🧩 The panels that open above the chat (Scheduler, Jobs, Create agent, Usage, Public API, Plugins, Vision) match too.
- 👌 The classic layout is unchanged.
- 🍎 Mac: this release carries the v1.3.34 Mac app until the next Mac build is ready.

---

### v1.3.37 — 23 November 2026

**New colours and fixes for the new layout.**

- 🎨 New colours: navy at night and blue-white by day, a brighter pink, and the four assistants in colours of their own (Bella cyan, Sapphire violet, Jade gold, Ellie orange), so none of them looks like a success or error message. The new colours meet the WCAG AA contrast standard. The classic layout is unchanged.
- 🧭 A lighter assistants panel: one row per assistant, with its settings behind its name. Emma's on/off switch is back.
- 🌗 A sun/moon button in the chat bar switches day and night in one click.
- 🔗 Share shows the link with a Copy link button, and a failed share can no longer copy a broken link.
- 👥 Work together shows that it's on and who is in the chat; whoever joins second now sees who was already there.
- 🔧 The Next.js interface framework is updated to 16.4.6. Its advisories concern Next.js servers; HARBOUR doesn't run one, so they never applied.
- 🍎 Mac: this release carries the v1.3.34 Mac app until the next Mac build is ready.

---

### v1.3.36 — 17 November 2026

**A new layout.**

- 🎨 New installs open in the new layout, in day mode: a sidebar of places, each opening as a page (Documents & knowledge as one page with the firm's documents, your documents and memory; Business tools with your sector's tools at the top); Settings with a Health page; the assistants, Emma and what's switched on in a side panel; a calmer chat.
- 👋 Existing installs keep their layout; a bar offers the new one once, and Settings › Appearance switches back at any time.
- 📖 The user manual and all 25 onboarding videos are redone for the new layout.
- 🔧 The Tactical Monitor no longer says "1 MODELS" when the local AI engine isn't running.
- 🐳 Server (Docker) installs: optional database connection reuse for many people at once, off by default (`HARBOUR_DB_REUSE=1`).
- 🍎 Mac: this release carries the v1.3.34 Mac app until the 1.3.36 Mac build is ready.

---

*For support or enterprise enquiries: Gregorymoores@proton.me*  
*Website: [harbour-ai.co.uk](https://harbour-ai.co.uk)*  
*Community: [Discord](https://harbour-ai.co.uk/discord)*
