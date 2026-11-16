# HARBOUR AI — Public Roadmap

Current version: **v1.3.34** — released 12 November 2026
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

## The Platform — v1.3.34

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

### v1.3.34 — 12 November 2026

**Security update — please install.**

- 🛡️ **Deleting a custom agent erased every conversation**, for every account on the install. Fixed: it now removes only your own chats with that agent, and clearing a chat clears only your own messages. History already lost this way cannot be brought back by the update; a backup taken before it happened still has it.
- 🛡️ The Computer Operator now obeys your role rules and the injection firewall.
- 🛡️ Disabling an account or changing a password now stops live voice, dictation, shared documents and the developer API at once.
- 🛡️ Email, Teams, calendar, phone and WhatsApp settings, the video provider key, reseller client keys and the "refuse all external requests" switch now need an administrator. If you are the only user, you are the administrator and nothing changes.
- 🛡️ Project files, schedules and device lock/wipe commands are tied to the account they belong to.
- 🐳 Server (Docker) installs: the production file now really closes port 8000. Needs Docker Compose 2.24 or newer.
- 🔒 The PDF reader handles the remaining seven kinds of deliberately malformed PDF from this month's scan.
- 🍎 The Mac app for v1.3.34 was added on 13 November 2026 (Apple Silicon, macOS 14+). To update from v1.3.32: open the new .dmg and drag HARBOUR AI into Applications, replacing the old copy; if macOS stops it, use Open Anyway as before.

---

*For support or enterprise enquiries: Gregorymoores@proton.me*  
*Website: [harbour-ai.co.uk](https://harbour-ai.co.uk)*  
*Community: [Discord](https://harbour-ai.co.uk/discord)*
