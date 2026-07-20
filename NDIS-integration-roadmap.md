# MoveWell: NDIS transport compliance and billing integration roadmap

This roadmap folds two research inputs into the MoveWell prototype:

- `ndis_transport_provider_report.md` (2025-26 PAPL pricing, support lines, caps,
  claiming rules).
- `transport_build_carryover_insights.md` (operating structure, roles, workflow, and
  data-model lessons from earlier NDIS platform work).

**Important:** these reports are design inputs, not current pricing authority. Rules
(support-item mappings, per-km rates, caps, loadings) must be **configurable and
effective-dated**, never hardcoded. The core reframe is that NDIS transport is a
**compliance-driven billing and workflow system**, not a rideshare fare app.

## Conflict analysis (prototype as reviewed)

Already aligned: money framed as an estimated claim (not a retail fare), "no money
handled in the car", drivers never see fares, claims built from trip evidence,
plan-management type captured, a support number referenced, consent separated from
clinical data.

Direct conflicts that had to change:

1. **Fixed per-tier fares** treated the $1.00/km as a retail fare (an audit risk per the
   report). Fixed in Phase 1: money is now a derived, decomposed claim; the tier signals
   vehicle capability, not price.
2. **One support item for everything** (`04_590_0125_6_1`). Phase 1 introduces multiple
   engines: Activity based transport, Specialised transport (WAV / sensory-calm), and
   provider travel non-labour (`01_799_0117_8_1`). Support-worker time noted for
   accompanied trips.
3. **Claim-only model** ignores recurring-allowance / externally-paid and self-managed
   participants. Phase 1 makes plan-managed wording correct; the funding-source branch is
   Phase 2.

## Decisions locked

- Fare model: **reframe as a derived, decomposed claim estimate** (totals preserved).
- Finance capability **folds into the Admin Portal** (no separate persona).
- Build order below; Phase 1 is implemented, Phases 2-5 are planned.

## Phases

### Phase 1 (done): booking and claim mechanics
- `RiderApp.dc.html`: tier = capability + a service-basis tag; Review and Receipt show a
  **decomposed** estimate (transport support + non-labour travel, each with its NDIS
  support item), a km / MMM-metro evidence line, plan-managed wording, and a no-gap-fee
  note. Totals unchanged.
- `CoordinatorWorkspace.dc.html`, `AdminPortal.dc.html`: invoice-export and
  claims-monitor notes reflect invoice separation, gap-fee blocking, and price-limit
  holds.

### Phase 2 (done): service agreements and funding profiles
- **Service agreement** as an onboarding gate: a step in the coordinator Add-participant
  wizard (billing method from plan, pass-through consent for tolls/parking/contribution,
  cancellation and no-show policy, e-signature vs in-person) and an acknowledgement step
  in the mobile sign-up; transport activates once the agreement is signed.
- **Participant funding profile**: a Funding profile and agreement card in the
  Coordinator participant detail, and funding-pathway lines on the Admin participant
  register showing the variations (Core budget claim to plan manager, NDIA claim,
  recurring Level allowance externally paid). Booking-time budget check is described on
  the card. Deepening the recurring Level 1/2/3 amounts and the full pre-booking gate
  remains for a later pass.

### Phase 3: finance in the Admin Portal (claim vs invoice vs reconciliation)
- Rework Admin **Claims monitor** into a pipeline that separates trip validation ->
  financial line generation -> invoice issue (plan-managed / self) vs claim submission
  (NDIA / myplace / PRODA) -> remittance ingestion -> reconciliation -> credit note /
  resubmission.
- Build out **Pricing and line items** (effective-dated support-item mappings and per-km
  rates), invoice decomposition, gap-fee / above-price-limit controls, and a plan-manager
  touchpoint. External actors: PRODA / myplace, accounting platform, bank.

### Phase 4: first-class exceptions
- Admin **Exceptions** module with structured types (trip delivered but not billable,
  wrong support item, missing or unsigned agreement, claim rejected, participant over
  budget, duplicate trip, worker or qualification mismatch, toll or parking dispute,
  no-show or cancellation outside policy), each with owner, SLA, status, and audit notes.
  Wire the existing ops attention queue and rejected-claim rows into it.

### Phase 5: governance and single source of truth
- Effective-dated **version history** for pricing books, service agreements, support-item
  mappings, and funding arrangements (shown under Admin configuration).
- Capture full trip data (km, MMM remoteness, tolls, parking, participant-in-vehicle,
  service classification).
- Linked master records (participant, funding profile, agreement, pricing/support map,
  booking, shift, invoice line, claim line, exception, audit log) as the single source of
  truth, with import/export as integration boundaries rather than the architecture.

## Roles to represent over the phases

Coordinator/scheduler, operations lead, driver/support worker, finance/accounts,
plan-manager counterpart, participant/nominee, internal approver, compliance/quality.
Most are present; finance and the plan-manager touchpoint arrive in Phase 3.
