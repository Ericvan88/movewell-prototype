# MoveWell — Platform Scope for Claude Design

**Purpose:** feed this into Claude Design to prototype every app experience. It sets the users, surfaces, information architecture, design tokens, and per-surface intent. It deliberately stops short of screen-by-screen layout so Design has room to map and shape each portal.

**Naming note:** *MoveWell* is the operating brand. *Wayflo* appears in earlier strategy docs as the working name and carries the same visual system; treat MoveWell as canonical. Where the model differs: MoveWell is a **registered NDIS provider running its own transport plus a white-label platform licensed to other providers**, not a pure open marketplace.

---

## 1. The people to design for

Everyone who touches a trip. The support-side web around a single participant is the thing most transport apps get wrong, so it's made explicit here.

**Demand / participant side**
- **Participant (rider)** — the person travelling. Ranges from independent app users to non-verbal AAC users. Highest accessibility bar.
- **Family / informal carer (booker)** — books and monitors on a participant's behalf; may manage several participants.
- **Support coordinator** — manages many participants across providers; lives in budgets, recurring schedules, claims, and compliance evidence.
- **SIL / group-home operations lead** — recurring transport for many residents across houses.
- **Allied health (OT / physio)** — supplies transport assessments, vehicle/positioning requirements, appointment syncing. *(MoveWell-specific; not in the marketplace docs.)*
- **Plan manager** — receives invoices, approves spend. Mostly read/export, not a heavy UI user.
- **NDIA planner / LAC** — read-only outcomes for plan reviews.

**Supply side**
- **Driver** — front-line. CareDriver sole-trader through to specialist/complex-needs. The tiering is the core of the recruitment story (see §4).
- **Operator partner** — runs a fleet under MoveWell branding/standards (incl. rural partners); relevant to the white-label model.

**Internal**
- **MoveWell operations / dispatch**, **compliance**, **admin/RBAC**.

Design implication: same data plane, role-aware views. One human can hold several roles (e.g. rider + booker).

---

## 2. Surfaces

Modular. Five build targets. The **Fleet/Asset portal lives inside the MoveWell Admin portal**, not as a standalone app.

| # | Surface | Primary users | Platform | Notes |
|---|---------|---------------|----------|-------|
| 1 | **Client App** (role-aware: rider / booker / coordinator) | Participants, families, coordinators, SIL, allied health | iOS + Android + accessible web | Coordinator + SIL + allied-health modes are web-first |
| 2 | **Driver App** | Drivers | iOS + Android | One-handed, offline-tolerant, high accessibility |
| 3 | **Driver Onboarding & Recruitment Portal** | Prospective + active drivers | Web (mobile-friendly) | New. Recruit → credential → **level up support tier** (§4) |
| 4 | **Operator / Fleet Portal** | Operator partners, fleet managers | Web (desktop + tablet) | Partner-facing fleet + driver + trip + claims management |
| 5 | **MoveWell Admin Portal** | Ops, compliance, admin | Web (desktop) | Live ops, IMS, claims, config, RBAC — **contains the Asset/Fleet Management module** |

---

## 3. Information architecture (per surface, intent-level)

Enough to orient Design; not a screen list. Let Design expand each into flows and layouts.

**Client App**
- Rider: home (next ride + book), book-a-ride (where → when → vehicle tier → eligibility/line-item → confirm), live tracking, 2FA pickup, in-trip + SOS, trip complete + rating, receipt/claim view, bookings history, profile (accessibility, support contacts, consent), help/complaint.
- Booker: rider flows + managed-participants list + consent-scoped visibility + support-contact notification routing.
- Coordinator (web): multi-participant dashboard (budget burn-down, claim status), participant detail, recurring trip planner, claims pipeline, plan-manager invoice export, compliance/credential view, outcome reports, team & permissions, integrations.
- Allied health (web, lightweight): participant transport assessment, vehicle/positioning requirements attached to profile, appointment-sync, consented outcome view.

**Driver App**
- Online/offline + today; document/credential hub with expiry alerts; trip offer (accept/decline, timeout); pre-trip detail (accessibility + behaviour notes, nav); on-the-way; arrived; 2FA pickup; in-trip (waypoints, SOS, deviation alerts); end trip; post-trip wrap; earnings + payout; schedule; training centre; incident report; support.

**Driver Onboarding & Recruitment Portal** *(see §4 for the tiering logic)*
- Public recruitment landing → apply → identity/screening capture → credential upload → training modules → readiness/verification status → activation → **tier-progression hub**.

**Operator / Fleet Portal**
- Dashboard (utilisation, trips, revenue, on-time); drivers + driver detail; vehicles + vehicle detail; trip pipeline + manual reassignment; earnings/statements; claims; compliance/audit pack; incident log; reports; profile/billing.

**MoveWell Admin Portal**
- Live ops dashboard; trip search/detail; riders; drivers/operators register + suspension; onboarding queue; compliance hub + audit calendar; incident management (IMS + NDIS Commission workflow); claims monitor; pricing/line-item config; plan-manager + provider directories; privacy/access logs; outcomes console; configuration/feature flags; user management/RBAC.
- **Asset / Fleet Management module (embedded here):**
  - Vehicles as tracked assets: type/config (standard, WAV, **sensory-calm, bariatric, high-dependency, child-specific, EV**), capacity, accessibility, registration, insurance, inspection/maintenance schedule + expiry.
  - Devices/equipment as assets: restraints, positioning aids, AAC/comms kit, child restraints inventory.
  - Credentials as assets: screening, training, first-aid — expiry-tracked and linked to the driver/vehicle they belong to.
  - Assignment view: which driver ↔ which vehicle ↔ which participant requirements; utilisation and compliance traffic-lights.

---

## 4. Driver recruitment & support-tier progression (design this as a growth loop)

The onboarding portal isn't just intake — it's built to **recruit broadly, then encourage drivers to level up their support capability**, because higher tiers unlock more work and higher pay. Design should make progression visible and motivating.

**Tier ladder (capability, not seniority):**
1. **CareDriver (entry)** — ambulatory participants; sedan. Screening + disability-awareness + insurance.
2. **Specialist** — WAV, manual handling, complex acuity. Vehicle audit + restraint compliance + practice-standards alignment.
3. **Complex / high-dependency + communication specialisations** — high-dependency transport, plus **verified badges**: Auslan, AAC, paediatric, mental-health first aid, sensory-calm.

**Design intent for the portal:**
- Show a driver where they are on the ladder and what the *next* badge/tier unlocks (more trip types, higher pay, priority matching).
- Treat each badge/credential as a completable module with a clear reward.
- Surface earnings/opportunity uplift per tier to drive upgrade behaviour.
- Credential portability: recognise existing NDIS Worker Screening on entry (reduce switching friction).
- Public-profile tie-in: earned badges appear on the participant-viewable driver profile (transparency is a MoveWell brand pillar), which reinforces the incentive.

---

## 5. Design system tokens (apply across all surfaces)

Working brand — coral/purple/yellow. WCAG 2.1 AA minimum on all surfaces; AAA target on book-a-ride and incident flows.

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
- Client App → coral. Driver App / Operator Portal → purple. Admin Portal → purple gradient (`#6C5CE7 → #8B7EEE`). Marketing/recruitment → full coral→purple gradient.

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
- Accessibility profile drives vehicle tier auto-selection; specialist fleet types (WAV, sensory-calm, bariatric, high-dependency, child, EV).
- NDIS line-item eligibility shown *before* confirm; claim auto-built after trip; driver never sees/enters price.
- 2FA pickup verification (code/QR); support-network live visibility; in-trip SOS with ops-desk SLA.
- Behaviour-support-plan attachment when required; incident reporting → IMS.
- Booking *on behalf of* (booker/coordinator), recurring trip subscriptions, plan-manager invoicing.
- Public, credential-rich driver profiles and the tier/badge system.

---

## 7. Build order suggestion (for prototyping)

1. Client App — rider mode (highest accessibility bar; anchors the design system).
2. Driver App.
3. Driver Onboarding & Recruitment Portal (incl. tier progression).
4. Admin Portal + embedded Asset/Fleet module.
5. Operator/Fleet Portal.
6. Client App — coordinator + booker + allied-health modes.
