# Product Requirements Document — Physical Assets Marketplace

## Summary

A two-sided marketplace to buy, sell, and bid on physical assets such as vending machines, ATM machines, kiosks, and related equipment. The platform supports listing creation, auction (bidding) and fixed-price sales, secure payments with escrow, logistics coordination (pickup/shipping/installation), asset verification and inspection, compliance/KYC for regulated assets (especially ATMs), and dispute resolution. The initial MVP targets used vending machines and non-cash-handling kiosks; ATMs and heavily regulated assets are flagged for controlled rollout with additional compliance requirements.

---

## Goals (What & Why)

* Launch a trustworthy, low-friction marketplace for buying and selling physical assets to unlock liquidity for asset owners and provide buyers with vetted inventory.
* Provide features needed for high-value, hard-to-ship physical goods: bidding, escrow, logistics coordination, inspection, and fraud prevention.
* Achieve a safe, scalable foundation that allows adding new asset categories (ATMs, arcades, laundry machines) and monetization channels (listing fees, success fees, premium listings, logistics referrals).

## Success metrics (KPIs)

* GMV (Gross Merchandise Value) — \$ per month; target: \$X in first 6 months (set during roadmap planning).
* Conversion rate: % of listings that result in sale within 90 days.
* Time-to-first-sale for a listing (median days).
* Buyer satisfaction score (NPS/CSAT) and seller satisfaction.
* Percentage of transactions using escrow and successfully completed without disputes.
* Number of verified/inspected listings.
* Repeat buyer/seller rate.

---

## Users & Personas

1. **Independent Owner (Seller)**

   * Owns a small number of vending machines or kiosks; wants to liquidate or upgrade.
   * Needs simple listing flow, clear pricing, shipping/installation help, and low fees.

2. **Operator / Small Chain (Seller & Buyer)**

   * Operates 10–200 units; buys to expand and sells retired units.
   * Needs bulk listing tools, inventory import, offers/auctions, and logistics coordination.

3. **Reseller / Refurbisher (Buyer)**

   * Buys used machines to refurbish and resell.
   * Needs robust filtering by condition, location, and repair history; wants inspection reports.

4. **Business Buyer (Buyer)**

   * Cafes, offices, property managers looking for turnkey installations.
   * Needs delivery and installation services, warranty/maintenance options, and financing/leasing info.

5. **Platform Admin / Support**

   * Monitors listings, disputes, KYC, payments, and marketplace health.

---

## Key Use Cases & User Journeys

### Use Case A — Simple Fixed-Price Sale (Seller)

1. Seller creates an account and verifies identity.
2. Seller lists a vending machine with photos, serial number, condition, location, and asking price.
3. Platform offers optional inspection service scheduling.
4. Listing goes live; buyer purchases using Buy Now.
5. Buyer pays; funds go to escrow. Seller receives shipping label or schedules pickup.
6. Asset delivered or collected; buyer inspects. Upon confirmation or after a time window, escrow releases funds to seller.

**Acceptance criteria:** Listing published, escrow held, shipping scheduled, funds released after confirmation.

### Use Case B — Auction / Bidding (Buyer & Seller)

1. Seller lists a machine as an auction with reserve price and start/end times.
2. Buyers place bids; system enforces bid increments and auto-extend on last-minute bids.
3. Winning bidder pays into escrow within a payment window.
4. Logistics arranged and asset transferred; funds released on successful delivery or after grace period.

**Acceptance criteria:** Bids recorded, auction integrity maintained, payment/escrow flows work, dispute path exists.

### Use Case C — ATM (Regulated) Sale (High Trust)

1. Seller/Buyer triggers enhanced KYC and regulatory checks.
2. Seller provides cash-handling history, service contracts, and bank/processor handoffs.
3. Platform requires escrow + certified inspection + legal transfer templates.
4. Final transfer includes decommissioning/removal of sensitive data and re-certification if needed.

**Acceptance criteria:** KYC passed, documentation attached, escrow and legal templates used, transfer documented.

---

## Product Scope — MVP vs Roadmap

### MVP (must-have to launch quickly)

* Account creation & basic KYC for sellers and buyers (email, phone, ID upload)
* Create/edit listings: title, category, make/model, serial, condition, photos, location, quantity, price type (fixed or auction), reserve price, shipping options
* Search & browse with filters: location radius, category, condition, price, auction vs buy-now
* Bidding engine: support sealed/open auctions, bid increments, max-bid proxy bidding, auto-extend
* Payment integration + escrow (support major cards + ACH); escrow release rules
* Messaging between buyer & seller + seller response SLA tracking
* Logistics scheduling integration (carrier API or partner flow) and print labels for shippable items; pickup coordination for large assets
* Inspection scheduling (3rd party or partner network) and simple inspection report upload
* Admin dashboard: transactions, disputes, KYC queue, listings moderation
* Basic fees: listing fee (optional) and success fee
* Email notifications and critical transactional webhooks

### Post-MVP / Roadmap (phase 2 & 3)

* Advanced verification for ATMs and high-value assets (enhanced KYC, background checks)
* Bulk inventory import/export and CSV templates for operators
* Seller storefronts and branded pages
* Financing/leasing integration & partner referrals
* API for partners (ERP/inventory sync)
* Insurance and warranty marketplace
* Predictive pricing suggestions (based on condition, model, location)
* Local pickup marketplaces and third-party logistics (3PL) integrations
* International shipping rules, customs documentation
* Dynamic seller verification badges (verified, inspected, refurbished)

---

## Functional Requirements (detailed)

### Listings

* FR-101: Listings must capture structured metadata: category, subcategory, brand, model, serial number, year, odometer-equivalent (usage cycles), condition (New/Like New/Good/Fair/Poor), photos (min 4), video optional, location (lat/lon), estimated weight & dimensions, pickup/shipping options, required certifications for sale (e.g., ADA for kiosks).
* FR-102: Sellers can choose sale type: Fixed Price, Auction (timed), Make Offer (optional).
* FR-103: Support quantity >1 for multi-unit listings with per-unit price or bulk pricing tiers.

### Bidding & Auctions

* FR-201: Timed auctions with start/end datetime, reserve price, minimum increment, proxy bids, auto-extend if last-minute bid within X minutes.
* FR-202: Bid history viewable to buyers (masking bidder identities until auction completes).
* FR-203: Bidder must be verified and have a payment method; high-value auctions may require pre-authorization or deposit.

### Payments & Escrow

* FR-301: Integrate payment processor(s) supporting card and ACH; hold funds in escrow until release conditions met.
* FR-302: Support partial refunds, escrow disputes, and fee deductions.
* FR-303: Automatic release rules: buyer acceptance or timeout (e.g., 7 days after confirmed delivery).
* FR-304: Clear fee model shown at checkout: platform fee, shipping fee, tax, inspection fee.

### Logistics & Delivery

* FR-401: Shipping options shown on listing: buyer-arranged pickup, seller-arranged shipping, platform-partnered shipping.
* FR-402: For heavy items (weight/dimensions > threshold), require freight shipping flow with quote request.
* FR-403: Tracking integration and delivery confirmation required to release escrow.

### Inspections & Verification

* FR-501: Option to request inspection: schedule date/time, inspector uploads report with photos and pass/fail checklist.
* FR-502: Verification badges displayed for listings that passed inspection.

### Messaging & Offers

* FR-601: In-platform messaging with attachments and templates for common questions (payment, condition, pickup).
* FR-602: Offer flow for Make Offer: buyer submits offer, seller accepts/rejects/counteroffers; accepted offer triggers escrow payment.

### Admin & Moderation

* FR-701: Admin tools for reviewing KYC, suspending listings, refunding transactions, and resolving disputes.
* FR-702: Automated rules for flagging suspicious listings (mismatch pricing, duplicate serials, banned categories).

---

## Non-functional Requirements

* NFR-1: Availability: 99.9% uptime for core marketplace flows.
* NFR-2: Scalability: support growth to thousands of listings and concurrent auctions.
* NFR-3: Performance: listing pages load in <2s for typical catalogs.
* NFR-4: Security: encrypt PII in transit & at rest, PCI-DSS compliance for payment processing, CVV and card tokenization.
* NFR-5: Data retention & privacy per applicable laws (GDPR, CCPA) — implement user data export & deletion flows.

---

## Compliance, Legal & Regulatory

* ATMs & cash-handling equipment require additional compliance: bank/processor transfer forms, proof of decommissioning for cash cards, and possibly local regulations — include legal review and restricted sale workflows.
* Export controls: some kiosks or hardware with cryptographic modules may require licensing.
* Tax collection: collect and remit sales tax per jurisdiction or provide seller tax settings.
* Terms of Service & Acceptable Use: clearly disallow stolen goods and require serial number disclosure.

---

## Fraud Prevention & Risk Management

* Identity verification (ID OCR + selfie liveness) for sellers posting high-value items.
* Serial number cross-checks against stolen/blacklist databases (3rd party integration).
* Escrow to avoid chargeback risk; for high-risk transactions require escrow + deposit.
* Rate limits and bot detection on bidding/offer flows.
* Manual review queue for suspicious listings and flagged sellers.

---

## Data Model (high-level)

* Users: id, name, email, phone, KYC\_status, verification\_docs\[], rating
* Listings: id, seller\_id, title, category, brand, model, serial, condition, photos\[], location{lat,lon,city,state,country}, dimensions, weight, price\_type, price, reserve\_price, quantity, shipping\_options, inspection\_status
* Auctions: id, listing\_id, start\_at, end\_at, bids\[], reserve\_price, status
* Orders: id, listing\_id, buyer\_id, seller\_id, payment\_status, escrow\_status, shipment\_id, inspection\_id, final\_status
* Inspections: id, listing\_id, inspector\_id, report, pass\_fail, photos\[]

---

## APIs & Integrations

* Payment provider (Stripe, Adyen, or similar) for cards and ACH; escrow logic managed by platform or payments partner.
* Identity verification (e.g., Onfido, Persona) for KYC/KYB.
* Shipping partners / freight quote APIs (UPS/FedEx/3PL marketplace partners) and local carriers for heavy freight.
* Inspection partners and scheduling (calendar + SMS reminders).
* Optional: valuation data sources / historical sales database for pricing suggestions.

---

## UX Notes & Wireframes (high-level)

* Listing creation wizard: Step 1: Basic info; Step 2: Photos & condition checklist; Step 3: Pricing & sale type; Step 4: Shipping & logistics; Step 5: Publish & pay listing fee (if any).
* Auction page: countdown timer, current top bid, bid entry with proxy bid option, bid history modal, countdown auto-extension banner.
* Checkout flow: show escrow details, fees breakdown, shipping & pickup choices, ability to schedule inspection/installation.
* Mobile-first design: many sellers will list from phones in the field; provide camera-first photo uploader and suggested photo checklist.

---

## Operations & Support

* Customer support SLA tiers: standard (48 hours) and expedited for high-value transactions.
* Dispute handling playbook: evidence collection, inspection verification, mediation window, partial refunds.
* Onboarding for commercial operators: CSV bulk import, dedicated onboarding manager.
* Partnerships: inspection network, freight brokers, refurbishment partners, insurance providers.

---

## Monetization & Business Model

* Listing fee (low) + success fee (percentage of sale).
* Premium featured listing placements and storefront subscriptions for high-volume sellers.
* Referral / commission on logistics, inspection, financing, and insurance partners.

---

## Analytics & Reporting

* Seller dashboard: active listings, pending offers, completed sales, revenue, fees paid.
* Buyer dashboard: saved searches, watched auctions, purchase history, support tickets.
* Admin reporting: GMV, disputes, fraud rate, inspection pass rate.

---

## Launch Plan & Milestones (example)

* Month 0: Product definition, partner outreach (inspections, logistics), and legal framework.
* Month 1–2: Build core MVP (Listings, Search, Payments+Escrow, Messaging, Basic Logistics).
* Month 3: Closed beta with 50 listings (vending machines & kiosks) and partner-inspection pilots.
* Month 4: Public launch in target region (single country/state) and marketing push.
* Month 6: Add auction features, bulk import, and expand to ATMs with compliance flow.

---

## Risks & Mitigations

* Risk: High fraud or stolen goods. Mitigation: mandatory serial capture, KYC, blacklist checks, and manual review for flagged items.
* Risk: Complex logistics for heavy/bulky assets. Mitigation: partner with freight brokers and provide clear shipping guidance and quotes.
* Risk: Regulatory complexity for ATMs. Mitigation: controlled rollout, legal templates, and account manager support.

---

## Open questions for stakeholders

1. Target launch geography and tax/legal jurisdiction(s).
2. GMV and adoption targets for first 6 and 12 months.
3. Appetite for subsidizing inspection and shipping in launch phase.
4. Which payment provider(s) do we prefer (platform-managed escrow vs payment-provider escrow)?
5. Risk tolerance for allowing non-verified sellers and high-value auctions.

---

## Next steps

* Confirm target launch market and top-priority asset categories.
* Validate with 5–10 sellers and 5–10 buyers to collect user requirements and pricing sensitivity.
* Finalize partner agreements for inspections, freight, and ID verification.
* Kick off engineering for MVP features and prepare beta onboarding.

---

*Appendix: Example Acceptance Criteria (for dev sprints)*

* Users can create a listing with at least 4 photos and location; duplication rejection for exact serial numbers.
* Auctions accept bids and enforce proxy bidding; winner notification and payment flow trigger.
* Escrow holds funds and releases on delivery confirmation or after configured timeout.
* Inspection upload attaches to listing and displays badge on listing page.
