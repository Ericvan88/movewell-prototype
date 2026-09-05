# MoveWell: top 10 priorities to round out the prototype

Prepared 5 September 2026 from a full audit of the prototype (every flow, every
clickable element) and a review of the current NDIS market and regulatory position.
The goal of this round is a prototype complete enough to write user stories against and
to size the business, not to polish visuals.

## What the market review changed

1. **MoveWell is a "platform provider" and mandatory registration started 1 July 2026.**
   The NDIS Commission now requires platform providers (apps or websites that connect
   participants with workers and process NDIS-funded payments) to register: independent
   audit against the Practice Standards, key personnel suitability, worker screening for
   every worker on the platform, 24-hour reportable incidents, and an accessible
   complaints system. Higher-risk supports follow from 1 July 2027. Incident and
   complaints management therefore move from "nice to have" to licence to operate.
2. **Pricing is confirmed.** The 2026-27 price limit for Activity Based Transport
   (04_590_0125_6_1) is $1.00 per km nationally, effective 1 July 2026, with no
   remote loading on the per-km item. The prototype's claim model is aligned.
3. **The caregiver channel is the contested ground.** Uber's own survey found 84 percent
   of NDIS participants rely on a carer or family member to arrange travel, and Uber
   Caregiver now offers book-on-behalf, three-way chat and 90-day scheduling. It does not
   offer NDIS claiming, accessibility profiles, trained or screened drivers, verified
   pickup or incident management. Those are MoveWell's differentiators, and the Supporter
   app that carries them currently has a dead primary button.
4. **Plan reform rewards evidence.** Support needs assessments start April 2027,
   foundational supports move outside the NDIS by January 2028, and Thriving Kids begins
   October 2026 for under-9s. Transport providers that can hand participants clean
   evidence of need and outcomes (trips, purpose, on-time, km) will be easier to keep in
   plans. Some children's transport may leave the scheme.
5. **Scale of the pool.** 774,456 active participants at March 2026 and $12.4 billion
   paid to providers in that quarter. Transport levels remain Level 1 about $69 per
   fortnight, Level 2 about $103, Level 3 about $133, alongside Core-funded
   activity-based transport.

## The top 10

Ordered by value for user stories and business sizing. "Correct" items fix what a
reviewer would trip over today; "complete" items add what is missing.

### 1. Correct: make every record its own person (persona convergence)
Every list in the prototype opens the demo record regardless of what was clicked:
the coordinator caseload opens Maya for Theo, Iris, Jordan and Priya (and "Refer for OT
assessment" refers Maya); the driver radar, dispatch and offer screens all pre-trip
"Maya P." for jobs that are not hers, with an 11:00 am job opening a 2:15 pm pickup;
Allied Health shows Maya's assessment content and four "Maya" captions when Henry is
the referral; the supporter sign-up finishes inside Maya's rider app and Lena's sign-up
lands as Deb. Fix by carrying a real participant, trip and driver record through each
flow. This is the foundation for user stories: without it there is no data model to
write them against.

### 2. Complete: the Supporter app as a real product
"Book a ride for Maya" and "Book a ride for Sam" do nothing, Sam has no detail screen,
and there is no message feed. Wire booking on behalf (reusing the rider steps with the
supported person's profile applied), add Sam's screen with his narrower consent scope,
and add the "Maya has arrived safely at Hydrotherapy · 10:32 am" feed. This is the
direct answer to Uber Caregiver and the channel 84 percent of participants use.

### 3. Complete: incident management, end to end
Regulatory under mandatory registration (Practice Standards Module 2A, 24-hour
reportable incidents). Today: one worked incident in Admin, a dead "Report an incident"
in the Driver app, and a dead SOS button on the in-trip screen. Build driver intake
(SOS and report), the admin lifecycle (record, classify, immediate safety actions,
notify, escalate, corrective actions, evidence, closure, Commission report), and a
"Record incident" action from any trip in Admin.

### 4. Complete: complaints and feedback
Also regulatory. Rider wizard: complaint or compliment, anonymous or named, add an
advocate or support person, attach evidence, get a reference number and status updates,
with the NDIS Commission escalation path. Admin: a complaints queue restricted by role.

### 5. Correct: the driver-side money model
The Driver app shows the participant's whole claim total as the driver's earnings
($52.20 "you earned" equals the WAV claim; the sedan job is priced at the WAV figure;
radar cards show bare fares). Define driver remuneration properly: contractor per-trip
payout derived from the claim with MoveWell's margin, employed drivers on rostered
hours. This is the unit economics of the business and cannot be sized until it exists.
Also decide the position on "take rate 18 percent", "private pay 8 percent" and "surge
nudge" copy in Admin: keep as internal metrics or reword.

### 6. Complete: finance pipeline in Admin (roadmap Phase 3)
Claim vs invoice vs reconciliation as separate workflows: trip validation, line
generation, invoice issue for plan-managed and self-managed, NDIA claim submission for
agency-managed, remittance, reconciliation, credit note and resubmission. Include
invoice drill-in (past exports and claims rows are currently inert), a plan-manager
touchpoint, and the exception types from Phase 4 folded in (rejected claim, unsigned
agreement, over budget, duplicate). This is what sizes revenue timing and cash cycle.

### 7. Complete: participant transport profile and driver brief
Finish the driver's pre-trip brief with badge chips (non-verbal, wheelchair, 2:1
support), a risk level and how the person prefers to be addressed. Keep plan-level
data (NDIS number, plan dates, primary contact, risk detail) in the Admin and
Coordinator records only, preserving the privacy stance that drivers never see plan
details. Make the rider's accessibility profile editable ("Edit" is dead) and fill
the Allied Health assessment (chips are static, so requirements never change).

### 8. Complete: notifications and transport alerts
No app has an inbox. Add a notifications feed to the rider and supporter apps, seeded
with driver running late, trip cancelled, participant collected and not collected,
funding almost exhausted, consent expiring, and service agreement expired, with the
matching admin and coordinator alerts already on their dashboards linking through.
In-app messaging stays deferred.

### 9. Correct: make lists behave like lists
Filters and search are painted on but inert across Admin (participants, drivers, trip
search), config toggles do not flip, "Invite user" and "Invite team member" are labels,
recurring trips, past exports, claims cards, compliance rows, integrations and
timesheets have no drill-in, and rider booking history only opens one trip (and shows
the wrong receipt). Wire filters, search and drawers consistently, and remove the
duplicated 120-line logic block (with its stale retail fare arrays) from the four
files that carry it.

### 10. Complete: outcomes and evidence for plan reviews
Extend both outcomes screens with trips this month, on-time percentage, average wait,
missed pickups, cancellation rate, kilometres travelled and most-visited locations, and
add a participant-facing "evidence for my plan review" export. Ties directly to the
2027 support needs assessments and to the claim-unit evidence already captured.

## Deferred, deliberately
Guided story mode (best done once the flows above are real), in-app messaging,
effective-dated versioning (roadmap Phase 5), Thriving Kids and foundational-supports
routing (watch the October 2026 rollout).

## Sources
- DAAR, 04_590_0125_6_1 price and details 2026-27: https://daar.com.au/resources/ndis/ndis-pricing-guide/04_590_0125_6_1
- Carevo, NDIS transport funding guide 2026: https://carevo.com.au/blog/ndis-transport-funding-complete-guide
- NDIS Commission, mandatory registration: https://www.ndiscommission.gov.au/about-us/ndis-commission-reform-hub/mandatory-registration
- NDIS Commission, regulatory reform roadmap February 2026: https://www.ndiscommission.gov.au/sites/default/files/2026-02/Reg-Reform-Roadmap-Feb-2026-PDF.pdf
- Skystaff, platform provider registration 2026: https://skystaff.com.au/ndis-consulting/platform-provider-registration/
- NDIS Commission, incident management: https://www.ndiscommission.gov.au/rules-and-standards/reportable-incidents-and-incident-management/incident-management
- Uber newsroom, Uber Caregiver: https://www.uber.com/en-AU/newsroom/caregiver
- NDIS Growth, NDIS statistics 2026: https://ndisgrowth.com.au/ndis-statistics/
- Centre of Hope, NDIS reforms 2026 timeline: https://centreofhope.com.au/ndis-reforms-2026/
- Centre of Hope, transport funding levels 2026: https://centreofhope.com.au/ndis-transport-funding-explained-2026/
