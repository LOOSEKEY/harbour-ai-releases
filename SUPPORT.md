# HARBOUR AI — Support

**Who to contact, about what, and what to expect.** Written 9 October 2026.

HARBOUR runs on your own hardware and is built to be run by your own people. Most of what
comes up day to day — a new starter, a forgotten password, a document that should be in
the Knowledge Base — is something your administrator or IT partner can do in a few
minutes with the manuals. HARBOUR's developer handles what only the developer can fix:
faults in the software, and security.

---

## The three kinds of request

| | What it is | Who handles it | What to expect |
|---|---|---|---|
| **1. Everyday use** | "How do I…?" Adding or removing users, resetting a user's password, uploading documents, setting up backups, choosing a model, training staff. | **Your administrator, or your IT partner** if you have one. | The **User Manual** ([harbour-ai.co.uk/manual.html](https://harbour-ai.co.uk/manual.html)) and **"What do you want to do?"** ([harbour-ai.co.uk/manual-actions.html](https://harbour-ai.co.uk/manual-actions.html)). Offices with no internet should keep a saved copy of both. Partners also have the **Partner Handbook**. |
| **2. Software faults** | HARBOUR doing something wrong: a feature that errors, a panel that won't load, data that doesn't save, a crash. | **HARBOUR's developer**, for HARBOUR CARE customers and partners. | A reply within **2 working days**. A workaround where there is one, and the fix in the next release. |
| **3. Security** | A vulnerability in HARBOUR, or a suspicion that HARBOUR has been compromised. | **HARBOUR's developer**, any day of the year. | Our target is a **fixed release within 8 hours** of a confirmed vulnerability, day or night. Report it privately to Gregorymoores@proton.me with the subject `SECURITY`, never in a public issue. |

**Not covered by HARBOUR support:** the computer or appliance itself, the operating
system, networks, printers, email servers, backup drives and other hardware. Those belong
to your IT team or IT partner.

---

## Before you report a fault

1. **Run the self-test** — ⚙ SYSTEM → Diagnostics → *Self-test — check everything works*.
   It checks the engine, the AI models, documents, voice and storage, and it often names the
   problem outright.
2. **Download the support bundle** from the same screen. It holds the self-test results,
   the HARBOUR version, the AI models in use and recent log lines, with keys, email
   addresses and your home folder masked. It is made on your machine and shown to you
   first. Read it before you send it.
3. Email **Gregorymoores@proton.me** with: what you were doing, what happened, what you
   expected, the HARBOUR version (⚙ SYSTEM → Software updates shows it), and the support
   bundle.

Partners: send the request after your first-line checks, with the support bundle. Saying
what you have already tried saves a round trip.

---

## Getting fixes onto your machines

A fix is published as a new release. How it then reaches a machine depends on how that
machine gets updates (⚙ SYSTEM → Software updates):

- **Automatic (the default)** — the desktop app downloads it and installs it on the next
  restart.
- **From an update folder on your network** — your IT partner puts the new release in that
  folder when they have approved it.
- **By hand** — someone runs the new installer, from a USB drive for example.
- **Docker / server installations** — your IT partner loads the new image.

An office with no internet only receives a security fix when someone installs it. If you
run HARBOUR that way, agree with your IT partner who does that, and how quickly.

---

## HARBOUR CARE

Your licence never expires and HARBOUR keeps working without CARE. CARE is the annual plan
for customers who want faults handled directly by the developer:

- **£59 / year** — updates and priority email support for software faults.
- **£199 / year** — the same, plus an onboarding call.

Everyday "how do I" questions are covered by the manuals and by your administrator or IT
partner, not by CARE.

---

## Partners

An IT partner who installs and supports HARBOUR for its own clients handles everyday use
(level 1) itself, and passes software faults and security issues (levels 2 and 3) to
HARBOUR's developer. The **[Partner Handbook](https://harbour-ai.co.uk/partner-handbook.html)** covers installing, daily checks, updates,
backups and restore, locked-out administrators, collecting logs, and when to escalate.
Response times, hours and continuity arrangements for a partner are set out in that
partner's written agreement.
