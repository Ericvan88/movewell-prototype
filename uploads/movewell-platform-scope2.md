# MoveWell — Platform Scope for Claude Design

**Purpose:** feed this into Claude Design to prototype every app experience. It sets the users, surfaces, information architecture, design tokens, and per-surface intent. It deliberately stops short of screen-by-screen layout so Design has room to map and shape each portal.

**Naming note:** *MoveWell* is canonical. It reuses the earlier *Wayflo* visual system unchanged (same coral/purple/gradient mark, same tokens); only the wordmark word differs. Brand assets live in this same bundle — see `README.md` and `/logo`. Business model: MoveWell runs **all supply models under one roof**. It launches as an **open marketplace** (Uber-style independent contractor drivers), then **layers in employed drivers** for complex/higher-acuity work, and **builds out its own fleet selectively** where demand justifies it — especially for complex disability needs the market won't supply. No white-label; MoveWell does not license its platform to other providers. The contractor-vs-employee distinction is **catered for, not solved** in this scope — treated as a role flag now, with logistics deferred.

---

## 1. The people to design for

Everyone who touches a trip. The support-side web around a single participant is the thing most transport apps get wrong, so it's made explicit here.

**Demand / participant side**
- **Participant (rider)** — the person travelling. Ranges from independent app users to non-verbal AAC users. Highest accessibility bar. Owns the account.
- **Supporter** — parent, guardian, family, or paid NDIS support worker/carer added to a participant's account to book and manage rides on their behalf. Can manage **many** participant accounts (e.g. one family member across several kids, one support worker across a caseload). Linked to an account two ways: **self-requests access** (looks up the participant by mobile number, sends a request) or **added by a Support Coordinator**. Either path needs the participant/existing account holder to confirm before access is granted — self-add is not silent.
- **Support coordinator** — manages many participants across providers; lives in budgets, recurring schedules, claims, and compliance evidence. Also the one who can *initiate* adding a Supporter to a participant's account on their behalf.
- **SIL / group-home operations lead** — recurring transport for many residents across houses.
- **Allied health (OT / physio)** — supplies transport assessments, vehicle/positioning requirements, appointment syncing. *(MoveWell-specific; not in the marketplace docs.)*
- **Plan manager** — receives invoices, approves spend. Mostly read/export, not a heavy UI user.
- **NDIA planner / LAC** — read-only outcomes for plan reviews.

**Supply side**
- **Driver — marketplace (contractor)** — independent, self-onboards, works online/offline, takes trip offers. The launch supply. CareDriver entry through to specialist.
- **Driver — employed (MoveWell staff)** — brought on for complex/high-acuity work the marketplace can't safely serve; has shifts/rosters, assigned vehicles, payroll. Same person may progress here from the marketplace (see §4).
- Both share one Driver App with a **role flag**; contractor-vs-employee logistics are deferred — catered for, not solved.

**Internal**
- **MoveWell operations / dispatch / fleet** (runs day-to-day scheduling, employed-driver rosters, and owned vehicles — internal, inside Admin; also holds a **book-on-behalf** capability for riders who call in and can't self-serve — this is an ops tool, not a participant-facing role), **compliance**, **admin/RBAC**.

Design implication: same data plane, role-aware views. One human can hold several roles (e.g. rider + Supporter for a sibling).

---

## 2. Surfaces

Modular. **Four build targets.** Fleet management is internal-only and lives **inside the MoveWell Admin portal** (there is no external/partner portal).

| # | Surface | Primary users | Platform | Notes |
|---|---------|---------------|----------|-------|
| 1 | **Client App** (role-aware: rider / Supporter / coordinator) | Participants, Supporters, coordinators, SIL, allied health | iOS + Android + accessible web | Coordinator + SIL + allied-health modes are web-first |
| 2 | **Driver App** (role-aware: contractor / employed) | Marketplace + employed drivers | iOS + Android | One-handed, offline-tolerant, high accessibility. Role flag switches offer-based vs roster-based mode |
| 3 | **Driver Onboarding & Recruitment Portal** | Prospective + active drivers | Web (mobile-friendly) | Recruit → credential → **level up support tier** → path to employment (§4) |
| 4 | **MoveWell Admin Portal** | Ops, dispatch, fleet, compliance, admin | Web (desktop) | Live ops, dispatch/rostering, IMS, claims, config, RBAC — **contains the Fleet/Asset Management module** |

---

## 3. Information architecture (per surface, intent-level)

Enough to orient Design; not a screen list. Let Design expand each into flows and layouts.

**Client App**
- Rider: home (next ride + book), book-a-ride (where → when → vehicle tier → eligibility/line-item → confirm), live tracking, 2FA pickup, in-trip + SOS, trip complete + rating, receipt/claim view, bookings history, profile (accessibility, support contacts, consent), help/complaint.
- Supporter: linking flow first — self-add (look up participant by mobile number → send request → wait for confirmation) or accept a request initiated by a Support Coordinator; once linked, gets rider flows for each linked participant + a **managed-accounts switcher** (many participants under one Supporter login) + consent-scoped visibility + support-contact notification routing + ability to remove their own access or see who else supports each participant.
- Coordinator (web): multi-participant dashboard (budget burn-down, claim status), participant detail, **add-a-Supporter to a participant's account** (by mobile number, sends confirmation request to the participant/existing account holder), recurring trip planner, claims pipeline, plan-manager invoice export, compliance/credential view, outcome reports, team & permissions, integrations.
- Allied health (web, lightweight): participant transport assessment, vehicle/positioning requirements attached to profile, appointment-sync, consented outcome view.

**Driver App** *(role-aware: contractor / employed — role flag, mechanics deferred)*
- Shared: document/credential hub with expiry alerts; trip detail (accessibility + behaviour notes, nav); on-the-way; arrived; 2FA pickup; in-trip (waypoints, SOS, deviation alerts); end trip; post-trip wrap; training centre; incident report; support.
- Contractor mode: online/offline toggle; trip offer (accept/decline, timeout); earnings + payout.
- Employed mode: shift/roster view; assigned vehicle for the shift; dispatched jobs (vs open offers); timesheet instead of payout.

**Driver Onboarding & Recruitment Portal** *(see §4 for the tiering logic)*
- Public recruitment landing → apply → identity/screening capture → credential upload → training modules → readiness/verification status → activation → **tier-progression hub**.

**MoveWell Admin Portal**
- Live ops dashboard; **dispatch + rostering** (assign jobs, manage employed-driver shifts, manual reassignment); trip search/detail; riders; drivers register + suspension (contractor/employed flag); onboarding queue; compliance hub + audit calendar; incident management (IMS + NDIS Commission workflow); claims monitor; pricing/line-item config; plan-manager + provider directories; privacy/access logs; outcomes console; configuration/feature flags; user management/RBAC.
- **Fleet / Asset Management module (embedded here — internal only):**
  - Vehicles as tracked assets: type/config (standard, WAV, **sensory-calm, bariatric, high-dependency, child-specific, EV**), capacity, accessibility, registration, insurance, inspection/maintenance schedule + expiry. *(Fleet is built out demand-led — owned vehicles added where the market won't supply complex needs; the module should read gracefully whether there are 2 vehicles or 200.)*
  - Devices/equipment as assets: restraints, positioning aids, AAC/comms kit, child restraints inventory.
  - Credentials as assets: screening, training, first-aid — expiry-tracked and linked to the driver/vehicle they belong to.
  - Assignment view: which driver ↔ which vehicle ↔ which participant requirements; utilisation and compliance traffic-lights.

---

## 4. Driver recruitment & support-tier progression (design this as a growth loop)

The onboarding portal isn't just intake — it's built to **recruit broadly, then encourage drivers to level up their support capability**, because higher tiers unlock more work and higher pay. Design should make progression visible and motivating.

**Tier ladder (capability, not seniority):**
1. **CareDriver (entry)** — ambulatory participants; sedan. Screening + disability-awareness + insurance.
2. **Specialist** — WAV, manual handling, complex acuity. Vehicle audit + restraint compliance + practice-standards alignment.
3. **Complex / high-dependency + communication specialisations** — high-dependency transport, plus **verified badges**: Auslan, AAC, paediatric, mental-health first aid, sensory-calm. This tier is also the **path from contractor to employed MoveWell driver** — complex work is where employment kicks in (mechanics deferred; shown as a destination on the ladder, not built out).

**Design intent for the portal:**
- Show a driver where they are on the ladder and what the *next* badge/tier unlocks (more trip types, higher pay, priority matching).
- Treat each badge/credential as a completable module with a clear reward.
- Surface earnings/opportunity uplift per tier to drive upgrade behaviour.
- Credential portability: recognise existing NDIS Worker Screening on entry (reduce switching friction).
- Public-profile tie-in: earned badges appear on the participant-viewable driver profile (transparency is a MoveWell brand pillar), which reinforces the incentive.

---

## 5. Design system tokens (apply across all surfaces)

MoveWell brand (copied from Wayflo). Full values are in `brand-tokens.css` in this bundle — load that as the source of truth. Summary below. WCAG 2.1 AA minimum on all surfaces; AAA target on book-a-ride and incident flows.

**Colour**
| Token | Hex | Role |
|-------|-----|------|
| Brand coral | `#FF6B6B` | Primary brand, CTA fill, gradient start. Client-app signature colour |
| Coral light / dark | `#FF8E8E` / `#E85555` | Hover / pressed |
| Brand purple | `#6C5CE7` | Secondary, links, gradient end. Driver/Operator/Admin signature colour |
| Purple light / dark | `#8B7EEE` / `#5647C9` | Tints / hover-pressed |
| Brand yellow | `#FFD93D` | Highlight/celebration only, never body text |
| Background | `#FAFAF9` | Page background |
| Surface | `#F7F6F4` | Cards/containers |
| Border | `#E8E5E1` | Dividers |
| Text | `#2D3748` | Primary body |
| Text muted | `#4A4540` | Secondary |

**Gradients**
- Hero: `linear-gradient(135deg, #FF6B6B 0%, #6C5CE7 100%)`
- Subtle background: `linear-gradient(180deg, #FFF5F5 0%, #FFFFFF 50%, #F5F3FF 100%)`

**Surface colour identity**
- Client App → coral. Driver App → purple. Admin Portal → purple gradient (`#6C5CE7 → #8B7EEE`). Marketing/recruitment → full coral→purple gradient.

**Type & shape**
- Wordmark/UI sans: Atkinson Hyperlegible or Inter, semibold for headings.
- Corner radius: `0.75rem` (12px).
- Coral is accent/CTA only — never body text (fails contrast).

**Accessibility primitives (bake in from V1)**
- High-contrast, large-text, voice, and switch-access modes in the Client App.
- Driver App: ≥56px hit targets on driving-critical actions; voice prompts; one-handed.
- Plain-English throughout; person-first language.

---

## 6. Reference points for Claude Design (what's already solved elsewhere)

Take the solved patterns from mainstream rideshare and layer the disability-transport specifics on top.

**Borrow from Uber rider app:** map-first home, where-to autocomplete, live ETA + driver card, clean confirm step, post-trip rating.
**Borrow from Uber driver app:** online/offline toggle, offer card with timeout, turn-by-turn handoff, earnings summary, weekly payout view.

**Then layer the market-specific requirements Uber does not handle:**
- Accessibility profile drives vehicle tier auto-selection; specialist fleet types (WAV, sensory-calm, bariatric, high-dependency, child, EV), added to the owned fleet demand-led.
- NDIS line-item eligibility shown *before* confirm; claim auto-built after trip; driver never sees/enters price.
- 2FA pickup verification (code/QR); support-network live visibility; in-trip SOS with ops-desk SLA.
- Behaviour-support-plan attachment when required; incident reporting → IMS.
- Booking *on behalf of* (Supporter/coordinator), recurring trip subscriptions, plan-manager invoicing.
- Public, credential-rich driver profiles and the tier/badge system.

---

## 7. Build order suggestion (for prototyping)

1. Client App — rider mode (highest accessibility bar; anchors the design system).
2. Driver App — contractor mode (marketplace is the launch supply).
3. Driver Onboarding & Recruitment Portal (incl. tier progression + employment path).
4. Admin Portal + embedded Fleet/Asset module (incl. dispatch/rostering).
5. Driver App — employed mode (roster/shift layer on top of #2).
6. Client App — coordinator + Supporter + allied-health modes.
