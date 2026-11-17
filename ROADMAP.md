# HARBOUR AI — Public Roadmap

Current version: **v1.3.35** — released 17 November 2026
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

## The Platform — v1.3.35

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

### v1.3.35 — 17 November 2026

**Security update — please install.**

- 🛡️ A document-indexing route accepted any file in HARBOUR's own data folder, where the key that signs sign-ins is kept, so a signed-in account calling it directly could read that key and act as an administrator. It now accepts only the account's own uploaded documents.
- 🛡️ Each account's documents under RAG / Documents are kept in a folder of their own: a same-named upload from another account can no longer replace yours, re-indexing never uses another account's file, and removing a document deletes the stored file. If you are the only user, nothing changes; on an install with several accounts, documents added before this version may ask to be uploaded again when you press RE-INDEX NOW.
- 🍎 Mac: this release carries the v1.3.34 Mac app until the 1.3.35 Mac build is ready.

---

*For support or enterprise enquiries: Gregorymoores@proton.me*  
*Website: [harbour-ai.co.uk](https://harbour-ai.co.uk)*  
*Community: [Discord](https://harbour-ai.co.uk/discord)*
