# MoveWell: user stories and sizing

Derived on 6 September 2026 from the prototype as built (eight apps, 116 screens and
sections, 242 wired interactions, 21 commits). Every story below exists as a clickable
flow in the prototype, so the acceptance criteria describe behaviour that can be seen,
not guessed. Use this as the backlog seed for a build estimate and as the basis for the
business model.

How to read a story: persona, story, acceptance criteria (AC), size. Sizes are
engineering effort for a production build (not the prototype), assuming a team that
already has a mobile app shell, a web shell and an API: **S** under a week, **M** one
to two weeks, **L** three to five weeks, **XL** more than five weeks. Sizes include
API, data model, tests and the two clients where relevant, not design.

Personas: Participant (Maya), Supporter (Anna), Contractor driver (Deb), Employed
driver (Lena), Support coordinator (Leo), Allied health OT (Amy), Operations lead
(Priya), Finance (Fiona), Compliance and Quality (Marcus, Nadia), Plan manager
(external), NDIA and PRODA (external).

---

## Epic 1 · Identity, sign-up and onboarding

| # | Persona | Story | Acceptance criteria | Size |
|---|---|---|---|---|
| 1.1 | Participant | Sign up with my mobile and an SMS code so nobody needs to type a password. | OTP by SMS; resend; no password; session persists on device. | M |
| 1.2 | Participant | Give my NDIS number, plan management type and plan dates once, so bookings know how they are funded. | Self, plan-managed (with plan manager pick), agency; validated format; stored on the participant record only. | M |
| 1.3 | Participant | Set my address and usual destinations so booking is one tap. | Home address; 3 favourites; editable later. | S |
| 1.4 | Participant | Accept the service terms (no gap fees, cancellations, tolls and parking) before my first trip. | Agreement version recorded with timestamp; transport blocked until accepted. | M |
| 1.5 | Supporter | Sign up and request access to the person I support, and get in only when they approve. | Lookup by mobile; request; approval by participant or nominee; consent scope set at approval. | L |
| 1.6 | Coordinator | Add a participant through a guided wizard (identity, plan, access, needs, assessment, agreement, review) so nothing is missed. | 7 steps as in the prototype; funding profile created; agreement sent for e-signature or marked signed in person; referral raised optionally. | L |
| 1.7 | Coordinator | Activate transport only once the service agreement is signed. | Bookings blocked until signed; status visible on the participant record. | S |
| 1.8 | Driver | Apply in the app: mobile, identity, vehicle, tier, and see my pipeline (identity, screening, credentials, training). | Screening ported or applied for; document upload; status pipeline; ops queue entry. | L |
| 1.9 | Ops | Review the onboarding queue, see waiting time and screening state, and approve or hold applicants. | Queue with stage, screening, waiting; approve action; audit trail. | M |

## Epic 2 · Consent, supporters and who sees what

| # | Persona | Story | AC | Size |
|---|---|---|---|---|
| 2.1 | Participant | Decide per person what my supporters and coordinator can see and do (book, view trips, view claims, live tracking). | Per-contact toggles; changes take effect immediately; history kept. | M |
| 2.2 | Participant | Know that SOS and incident alerts always reach my chosen safety contact even if I share nothing else. | SOS scope cannot be disabled by consent. | S |
| 2.3 | Supporter | See one home for everyone I support, with what each has shared. | People list; per-person access line; locked items shown as locked. | S |
| 2.4 | Supporter | Book on someone's behalf using their accessibility profile and have them told. | Booking flow with their destinations and suggested vehicle; notification to the person; they can cancel. | M |
| 2.5 | Coordinator | See only participants assigned to me, within each person's consent. | Scope per participant; consent expiry shown; renewal request action. | M |
| 2.6 | Allied health | See a consented slice (assessment, attendance, punctuality) and never claims, costs or unrelated locations. | Field-level scope enforced by the API. | M |
| 2.7 | Ops | Every read of a participant record is logged with who, what, when and the consent that allowed it. | Immutable access log; visible under Privacy & access logs. | M |

## Epic 3 · Accessibility profile, assessment and vehicle requirements

| # | Persona | Story | AC | Size |
|---|---|---|---|---|
| 3.1 | Participant | Edit my accessibility profile (getting around, in the car, talking with me, what to call me, who travels with me) and see what it changes for bookings. | Chip groups as in the prototype; impact text; drivers see the practical items only. | M |
| 3.2 | Coordinator | Refer a participant to an OT for a transport assessment and see its status. | Referral record; assessor; status (requested, booked, requirements set). | M |
| 3.3 | Allied health | Accept a referral, complete the transport assessment (transfers, seating, equipment, sensory and communication) and save requirements to the profile. | Selections resolve to vehicle tier and requirements; change history; participant can request a review. | L |
| 3.4 | Participant | See the requirements my OT set and ask for a review. | Read-only requirements; review request creates a referral. | S |
| 3.5 | Ops | Requirements drive matching: a booking that cannot be met is flagged before confirmation. | Matching rules on tier, hoist, restraint, sensory-calm, 2:1, Auslan. | L |
| 3.6 | Driver | Get a pre-trip brief: badges, how to address the person, support level, risk level and reason, behaviour plan status, practical requirements. | Brief shown before Start driving; no diagnosis or plan data. | M |

## Epic 4 · Booking and matching

| # | Persona | Story | AC | Size |
|---|---|---|---|---|
| 4.1 | Participant | Book a trip in four steps (where, when, vehicle, review) with the estimated claim shown as NDIS lines, not a fare. | Lines per support item; non-labour line only where the agreement allows; no gap fee wording. | L |
| 4.2 | Participant | Book now or schedule ahead and get a confirmed driver the day before. | Scheduled trips; driver confirmation notification. | M |
| 4.3 | Participant | See the suggested vehicle from my profile and change it if I need to. | Suggested pill; override allowed within requirements. | S |
| 4.4 | Coordinator | Set up recurring trips that book automatically 7 days ahead and notify everyone. | Schedule; pause; generated bookings visible to participant and supporter. | L |
| 4.5 | Ops | Funding checks run at booking: funding source, remaining budget, eligible support item, agreement permissions. | Over-budget and unsigned-agreement bookings blocked with an exception raised. | L |
| 4.6 | Allied health | Suggest a booking from a clinic appointment and let the participant confirm. | Calendar integration (Cliniko or similar); suggestion sent, never booked on their behalf. | M |
| 4.7 | Ops | Match and dispatch: radar offers to contractors, direct offers with a countdown, rostered jobs for employed drivers. | First-to-grab and direct-offer modes; offer expiry passes to the next driver; roster assignment. | XL |

## Epic 5 · Trip execution and safety

| # | Persona | Story | AC | Size |
|---|---|---|---|---|
| 5.1 | Participant | Track my driver live and see their name, vehicle and plate. | Map, ETA, vehicle line. | M |
| 5.2 | Participant | Show a 4-digit code or QR at pickup so only the right driver can start my trip. | Code per trip; driver entry; mismatch handling; photo-ID alternative for self-managed adults. | M |
| 5.3 | Driver | Enter the pickup code, then see the destination and in-trip controls. | Keypad; route deviation alerts on; End trip. | M |
| 5.4 | Participant | Press SOS in the app and reach the ops desk within 60 seconds. | SOS state; ops call-back SLA; safety contact notified; cannot be disabled. | L |
| 5.5 | Driver | Press SOS, see the ops desk join, call 000, and report what happened afterwards. | SOS screen; location and dashcam preserved from 10 minutes before; hand-off to incident intake. | L |
| 5.6 | Driver | Wrap up with a checklist (handover, equipment, vehicle check) and see my pay for the trip. | Checklist gates completion; claim built automatically; pay breakdown shown. | M |
| 5.7 | Participant | Rate the trip and add compliments that reach the driver. | Stars; compliment chips; routed to quality record. | S |
| 5.8 | Ops | Watch live operations: map, KPIs, attention queue (coverage gaps, late running, demand spikes) and dispatch from the queue. | Live tiles; filters; dispatch action; coverage nudges to offline drivers (supply, never price). | XL |

## Epic 6 · Notifications and messages

| # | Persona | Story | AC | Size |
|---|---|---|---|---|
| 6.1 | Participant | See an inbox of transport alerts: running late, cancelled, collected, not collected, budget check, consent expiring, agreement renewal. | Unread badge; each with a follow-up action; safety alerts always on. | M |
| 6.2 | Supporter | Get the messages I have turned on per person (picked up, arrived safely, live trip, SOS) and see them in one feed. | Per-person toggles; feed; bookings I make appear in it. | M |
| 6.3 | Coordinator | Be alerted to consents expiring, budgets running out, claims stuck with plan managers, and agreements due. | Dashboard counters; renewal actions. | M |
| 6.4 | All | Receive push and SMS with the same content as the in-app feed. | Delivery preferences; quiet hours except safety. | M |

## Epic 7 · Driver supply, credentials and tiers

| # | Persona | Story | AC | Size |
|---|---|---|---|---|
| 7.1 | Driver | See my documents (worker screening, first aid, insurance, training) and renew before they lapse. | Expiry warnings at 21 days; upload renewals; matching suspended on lapse. | M |
| 7.2 | Ops | Keep one credential register across drivers and vehicles with expiry and status. | Register; filters; drawer per credential; audit calendar. | M |
| 7.3 | Ops | Suspend and reinstate drivers with a reason and review date, effective immediately. | Suspension pauses offers; driver notified; history kept. | S |
| 7.4 | Driver | Progress through tiers (CareDriver, Specialist, Complex) with training modules and see what each unlocks. | Module tracking; tier gates matching; pay effect shown honestly. | L |
| 7.5 | Employed driver | See my roster, vehicle check, today's jobs and timesheet, and flag a correction. | Shifts; pre-shift vehicle check; dispatch list; timesheet with correction flow. | L |
| 7.6 | Driver | Report a vehicle fault and have the vehicle taken off duty and jobs reassigned. | Fault intake; fleet notified; reassignment. | M |

## Epic 8 · Incident management (Practice Standards Module 2A)

| # | Persona | Story | AC | Size |
|---|---|---|---|---|
| 8.1 | Driver | Report an incident in three steps (what, details and evidence, sent) from a trip, wrap-up or the home screen. | Category, severity, actions taken, photos and voice; reference returned; reportable outcome explained. | M |
| 8.2 | Compliance | Work every incident through logged, classified, safety actions, notified, corrective actions, closed. | Lifecycle with advance action; owners and due dates on corrective actions; evidence preserved 7 years. | L |
| 8.3 | Compliance | Apply the reportable test automatically and start the NDIS Commission 24-hour and 5-day timers. | Rule by category and severity; Commission notification forced; timers visible; 5-day report from the record. | L |
| 8.4 | Ops | Record an incident from any trip and see linked incidents on the trip. | Wizard prefilled with trip; link both ways. | S |
| 8.5 | Compliance | Generate the incident report and Commission report from the record. | PDF; immutable once lodged. | M |

## Epic 9 · Complaints and feedback (complaints management rules)

| # | Persona | Story | AC | Size |
|---|---|---|---|---|
| 9.1 | Participant | Make a complaint, report a trip problem, or send a compliment in writing, by voice or by call-back. | Three types; three modes; optional trip link. | M |
| 9.2 | Participant | Complain anonymously and still track it by reference. | No identity on the record; reference-only tracking. | M |
| 9.3 | Participant | Add an advocate or support person who is copied on updates, and attach evidence. | Advocate options including an independent advocate referral; photo, screenshot, receipt. | S |
| 9.4 | Participant | Track my complaint (received, acknowledged, investigating, outcome, closed) and escalate to the NDIS Commission at any time. | Timeline; escalation records the Commission reference. | M |
| 9.5 | Quality | Work complaints in a register restricted to Compliance and Quality roles, with every open logged. | RBAC; access log; lifecycle drawer; linked incident; outcome; acknowledgement within 2 business days tracked. | L |
| 9.6 | Driver | Receive compliments the same day and see them count toward my quality record. | Routing to driver and lead; quality record. | S |

## Epic 10 · Claims, invoicing and reconciliation

| # | Persona | Story | AC | Size |
|---|---|---|---|---|
| 10.1 | Finance | Validate each completed trip (verified pickup, drop-off, agreement on the date, price limits) before any line is generated. | Validation rules; failures become exceptions. | L |
| 10.2 | Finance | Generate one line per NDIS support item (transport support, non-labour travel, support-worker time) from trip evidence. | Item chosen by vehicle actually dispatched; km and MMM recorded; held to price limits. | L |
| 10.3 | Finance | Issue by pathway: invoice to plan manager (API), claim via PRODA (bulk), invoice to participant (self-managed). | Three pathways; batch files; status per claim. | XL |
| 10.4 | Finance | Ingest remittances from plan managers, PRODA and the bank feed and match them to claims. | Matching; short or missing lines become exceptions; nothing posts to accounting until reconciled. | L |
| 10.5 | Finance | Resolve exceptions: rejected claim (regenerate and resubmit), short remittance (credit note or dispute), unsigned agreement, over budget, duplicate trip. | Typed exceptions with owner and SLA; actions per type. | L |
| 10.6 | Finance | Auto-chase issued claims older than 14 days and chase manually from the record. | Daily job; chase history on the timeline. | S |
| 10.7 | Coordinator | Export invoice bundles per plan manager (CSV, PDF), open past exports and see line items. | Bundles by period and plan manager; drill-in; sent by API. | M |
| 10.8 | Participant | See every receipt as NDIS lines with the total to my plan and no charge to me. | Receipt per trip; claim status. | S |
| 10.9 | Finance | Post reconciled claims to the accounting platform. | Xero (or equivalent) integration; idempotent. | M |

## Epic 11 · Pricing and driver remuneration

| # | Persona | Story | AC | Size |
|---|---|---|---|---|
| 11.1 | Finance | Maintain an effective-dated pricing book (support items, rates, price limits) with history attached to the claims it priced. | Versioning; effective dates; no hard-coded rates. | L |
| 11.2 | Finance | Set the contractor share (78% of transport support) and pass-through rules (tolls and parking at cost) and see a worked example. | Rule table; per-job pay computed from the claim; employed drivers hourly under the award. | M |
| 11.3 | Driver | See my pay per trip, why it is that amount, and a weekly payout. | Breakdown on offer and wrap-up; weekly statement; tolls and parking reimbursed. | M |
| 11.4 | Ops | Block gap fees and surcharges everywhere and never show fares to drivers. | Enforced in pricing and UI. | S |

## Epic 12 · Outcomes and evidence

| # | Persona | Story | AC | Size |
|---|---|---|---|---|
| 12.1 | Coordinator | See trips, on-time rate, average wait, missed pickups, cancellation rate, kilometres, attendance and most-visited places by plan goal for my caseload. | Monthly and quarterly; per participant drill-down. | M |
| 12.2 | Coordinator | Export a plan-review evidence pack per participant in the format the support needs assessment expects. | PDF and CSV; consented slice only. | M |
| 12.3 | Participant | See my own transport this plan year and export it for my review. | Card on Bookings; export to me and my coordinator. | S |
| 12.4 | Ops | Platform outcomes console with the same measures across all participants and providers. | Console; trend; complaints and satisfaction alongside. | M |

## Epic 13 · Platform, RBAC and integrations

| # | Persona | Story | AC | Size |
|---|---|---|---|---|
| 13.1 | Ops | Manage users, roles and scope; invite users; Compliance and Quality gate complaints and privacy logs. | RBAC with per-participant scope; invites expire. | M |
| 13.2 | Ops | Configure feature flags and business rules with effective dates. | Versioned config. | M |
| 13.3 | Ops | Find anything with a command palette across screens and records. | Search across participants, drivers, trips, incidents, complaints, claims. | S |
| 13.4 | Ops | Connect plan managers (API), NDIA PRODA, accounting and clinic calendars. | Integrations page; connection state; export-only fallback. | XL |
| 13.5 | Ops | Keep a full audit trail on every record. | Append-only events on all master records. | M |

---

## Build sizing

Counting the stories above by size (S 17, M 40, L 19, XL 5) at S 0.6, M 1.5, L 4, XL 7 engineer-weeks gives roughly **240 engineer-weeks** for the full product, before contingency. Two sensible cuts:

**MVP, a registered platform provider serving plan-managed and self-managed participants in one metro (Adelaide)**: Epics 1 to 6 and 8 to 10 minus PRODA, minus live ops map, minus recurring trips, minus tiers, minus accounting posting. About **130 engineer-weeks**: a team of four engineers for eight months, plus a designer and a product owner. Mandatory registration (audit, worker screening, incident and complaints systems) is inside this cut, not after it.

**Full product** adds agency-managed claiming via PRODA, live operations, recurring trips, employed-driver rostering, driver tiers, accounting and clinic integrations, outcomes exports and effective-dated versioning: the remaining **110 engineer-weeks**, about another eight months for the same team.

Non-engineering costs to carry alongside: NDIS registration audit (Practice Standards, Module 2A, complaints rules), key personnel suitability, insurance (public liability, vehicle, professional indemnity), a 24/7 ops desk from day one of trips, and worker screening for every driver.

## Business sizing frame

Every number here is a lever with an assumption stated next to it. Replace the assumptions with your own data as you get it.

Unit economics per trip (from the prototype's pricing book and remuneration rules):

- Average claim per trip: $40 (sedan $38.50, sensory-calm $45.10, WAV $52.20, mix weighted to sedans).
- Of that, transport support about $37, non-labour pass-through about $3.
- Contractor share 78% of transport support: $28.90. Pass-through to driver at cost: $3.
- MoveWell margin: 22% of transport support, about **$8.10 per trip** (20% of the claim).

Demand per active participant (assumption to validate against your caseload data):

- 2.4 trips per week, 48 weeks: about 115 trips a year.
- Claim value about $4,600 a year per active participant, MoveWell margin about **$930 a year per active participant**.

Scenarios:

| Scenario | Active participants | Trips a year | Gross claim value | MoveWell margin |
|---|---|---|---|---|
| Adelaide metro launch, year 1 | 600 | 69,000 | $2.8M | $0.56M |
| Adelaide metro established, year 3 | 2,500 | 288,000 | $11.5M | $2.3M |
| Three capitals | 8,000 | 920,000 | $36.8M | $7.4M |
| National, 5% of transport-funded participants | 25,000 | 2.9M | $115M | $23M |

Market ceiling frame: 774,456 active NDIS participants (March 2026). The share with Core transport or a recurring transport allowance is not published in one place; the working assumption is 55 to 65 percent, so about 450,000 people, of whom a smaller share cannot use public transport and use paid transport regularly. The national scenario above assumes 5 percent of that pool, which is ambitious but not the ceiling.

Costs that scale with trips: ops desk (about $1.20 per trip at scale), payment and claiming (about $0.40), insurance (about $0.60), support and quality (about $0.50). Costs that do not: engineering, registration and audit, management. At the year-3 scenario the trip-scaled costs are about $0.8M against $2.3M margin.

Levers that change the answer most: trips per participant per week, the contractor share (each point is about 1.2 percent of margin), the WAV and sensory-calm mix (higher claims, same share), and whether employed drivers on fleet vehicles are used for Complex-tier work (higher margin per trip, higher fixed cost).

## What to do with this

1. Import the stories into your backlog tool as epics and stories; the prototype screens are the visual spec.
2. Replace the assumptions in the business frame with caseload data from a coordinator partner (trips per week is the one that matters most).
3. Decide the MVP cut with the compliance lead, since mandatory registration fixes part of the scope for you.
