# GHL Client Acquisition System

A native GoHighLevel automation system built for a social media agency, demonstrating workflow-builder proficiency independent of third-party orchestration tools (Zapier, Make, n8n). The system captures leads, scores and routes them by intent, runs a multi-touch nurture sequence with engagement-based branching, and includes a safeguard workflow to prevent post-conversion follow-up.

**Note on artifacts:** GHL does not support exporting individual workflows as JSON/config files the way n8n and Zapier do. Account Snapshots (GHL's portability mechanism) require a paid tier not available on the trial account used for this build. This document, the Loom walkthrough, and the screenshots below serve as the equivalent proof of architecture.

---

## System Overview

Three workflows, each with a single responsibility, plus a shared configuration layer:

| Workflow | Trigger | Responsibility |
|---|---|---|
| `01 - Speed to Lead` | Form Submitted | Capture, pipeline entry, hot/cold scoring, instant response |
| `02 - Cold Nurture` | Tag Added (`cold-lead`) | 5-touch drip sequence with click-based engagement branching |
| `03 - Booking Cleanup` | Appointment Booked | Removes converted contacts from active nurture |

---

## Foundations

- **Pipeline:** `Client Acquisition` — 6 stages (New Lead → Nurturing → Booked → Showed → Won → Lost)
- **Custom Field:** `service_interest` — single-select dropdown (Social Media Management / Paid Ads / Content Creation), bound to Contact object. Dropdown chosen over free text specifically so branch conditions can perform exact-match comparisons instead of parsing inconsistent user input.
- **Custom Values:** `business_name`, `owner_name`, `booking_link` — referenced via merge tags across every message in the system, so updating a link or detail requires one edit instead of hunting through every email/SMS.
- **Calendar:** `Strategy Call` — Personal Booking type, 30-minute duration.

---

## Workflow 01 — Speed to Lead

**Trigger:** Form Submitted, scoped to a specific intake form (not "any form").

**Flow:**
1. **Create/Update Opportunity** — fires before any branching, so every lead is tracked in the pipeline regardless of score.
2. **Condition (IF/ELSE)** — branches on `service_interest = "Paid Ads"`. Paid Ads inquiries are treated as a stronger buying signal (budget already earmarked) than general content/social requests.
3. **Hot branch:** Add Tag (`hot-lead`) → instant personalized Email → SMS (built, not live-fired — see note below) → **Internal Notification** (GHL's dedicated staff-facing action type, distinct from a standard Email/SMS action which would route to the contact instead of the team).
4. **Cold branch:** Add Tag (`cold-lead`) → softer intro Email → handed off to Workflow 02 via tag trigger.

**A2P note:** SMS actions are fully built and wired but not live-fired during testing/demo. The trial account isn't A2P 10DLC registered — a US carrier-level compliance requirement for business SMS, independent of GHL, typically taking 3–5 business days to clear regardless of account tier.

---

## Workflow 02 — Cold Nurture

**Trigger:** Contact Tag Added, filtered to `cold-lead`. Built as an independent workflow so nurture cadence can be modified without touching lead-capture logic.

**Flow:**
1. Wait (2 days) → Email (Touch 2, value-add, non-salesy)
2. **Wait for Email Event** — GHL's dedicated node type for gating on email engagement (a standard Condition node can't read open/click state directly). Configured to watch for **link clicks** specifically, not opens — opens are unreliable due to image-blocking and email client pre-fetching; a click is a stronger, intentional signal. 3-day timeout ensures contacts who don't engage still continue through the sequence rather than stalling indefinitely.
3. **Engaged branch:** Add Tag (`warm-lead`) → direct, high-intent Email pushing the booking link → sequence ends.
4. **Timeout branch:** SMS (Touch 3, not live-fired) → Wait → Email (Touch 4, social-proof angle) → Wait → Email (Touch 5, closing/breakup message) → Add Tag (`nurture-no-response`) → Remove Tag (`nurture-active`) → END.

**Workflow setting:** `Stop on Response` enabled at the workflow level — ends the entire sequence immediately if the contact replies to any message, preventing continued automated sends during an active human conversation.

---

## Workflow 03 — Booking Cleanup

**Trigger:** Customer Booked Appointment, filtered to the `Strategy Call` calendar specifically.

**Flow:** Single action — **Remove from Workflow** (`02 - Cold Nurture`).

**Why this exists:** Workflow 02's engagement branch only detects clicks on tracked links within its own emails. A contact could book directly from an untracked touch (or any other channel) without ever clicking a monitored link or replying — meaning neither the click-branch nor Stop on Response would catch it. This workflow acts as a hard backstop: any confirmed booking on this calendar pulls the contact out of active nurture immediately, regardless of how they got there.

---

## Design Principles Applied

- **Single responsibility per workflow** — capture/routing, nurture, and cleanup are independently editable.
- **Data layer separated from message content** — custom values and fields drive logic and copy, nothing hardcoded.
- **Exit conditions built deliberately, not assumed** — engagement branching, reply detection, and booking cleanup all exist specifically to stop automation the moment it's no longer appropriate.
- **Compliance-aware** — SMS consent language matches TCPA/A2P expectations; SMS actions are architecturally complete but not fired against real numbers on an unregistered trial account.
