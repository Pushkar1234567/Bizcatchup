# BizCatchUp – RevenueCat Paywall & Subscription Integration

> **Reference spec for implementation.** Captures the product + engineering requirements for integrating RevenueCat as the billing/subscription platform across the BizCatchUp mobile apps (Flutter frontend) and the Go backend (`scanner/`, module `github.com/NookPay/mould`).
>
> - **Document Version:** 1.1
> - **Last Updated:** April 30, 2026
> - **Owner:** Product Team — BizCatchUp
> - **Status:** Under Review

> ⚠️ **Source-doc note:** The backend "Architecture Overview" in the original spec lists **Trackier** as the payment/webhook component. That is a copy-paste error — the authoritative billing/webhook provider is **RevenueCat**. This doc uses RevenueCat throughout. Trackier remains only an attribution SDK (`trackier_sdk_flutter` / Apptrove) and is unrelated to billing.

---

## 1. Objective

Integrate **RevenueCat** as the primary billing and subscription management platform in the BizCatchUp mobile apps (iOS + Android). This replaces the previously planned **AppSumo** billing workflow (now discarded) and becomes the official paywall + subscription system going forward.

**Goal:** Enable in-app subscription purchasing, entitlement unlocks (e.g. "Pro Access"), and paywall display via RevenueCat, for a seamless purchase/manage experience.

RevenueCat provides:
- Subscription hosting (Apple App Store, Google Play)
- Cross-platform entitlement management
- Revenue analytics
- Webhooks for post-purchase event updates

---

## 2. Scope

### In Scope
- **Frontend** integration of the RevenueCat paywall UI in BizCatchUp.
- Subscription flow via the RevenueCat SDK:
  - Free → Pro upgrade
  - Monthly and annual options
  - Display current plan entitlements
- Paywall customization using the BizCatchUp Figma design (import or RevenueCat component editor).
- Product catalog setup: **Offerings → Products → Entitlements → link entitlement to product → paywall setup & embedding**.
- Display of plans and pricing tiers (Monthly & Annual).
- Frontend testing via the **Test Store** environment before production.
- Restore purchases, Terms, and Privacy links on the paywall UI.
- API hook placeholders from backend → RevenueCat (data sync).

### Out of Scope (this phase)
- Backend entitlement validation, event webhooks, subscription-state sync *(Phase 2 — but documented in §7 for context)*.
- Pricing/billing logic inside the BizCatchUp backend.
- Revenue tracking / analytics reporting logic.
- Deep CRM integrations, paywall A/B testing (Phase 2).
- Cross-platform entitlement unification (future enterprise version).

---

## 3. Pricing Tiers

| Plan | Regular | Limited-time offer |
|------|---------|--------------------|
| **Free** | $0 | — |
| **Pro** | $15/month | **$5/month** |
| **Pro (annual)** | $180/year | **$50/year** |
| **Team** (flat, up to 5 members) | $75/month | **$15/month** |
| **Team (annual)** | $900/year | **$150/year** |
| **Enterprise** | Contact Us | — |

---

## 4. Developer Setup Flow (RevenueCat Dashboard)

1. **Create a New Project** in RevenueCat for BizCatchUp *(done)*.
2. **Configure Product Catalog:**
   - Create **Offerings** (e.g. `default_offering` → "Main subscription plans").
   - Create **Products** (monthly and annual Pro subscriptions, Team, etc.).
   - Create **Entitlements** (e.g. `Pro Access`).
   - **Link** entitlement ↔ products.
3. **Create & Edit Paywall:**
   - Option 1: RevenueCat native component editor.
   - Option 2: Import the BizCatchUp Figma paywall layout.
4. **Configure pricing** per §3.
5. **Test** via the Test Store environment.
6. **Deploy** the paywall into the user-facing app flow.

---

## 5. User Flow (Purchase)

1. User reaches a limit or taps **"Upgrade to Pro."**
2. RevenueCat **paywall** screen appears.
3. User views plan options (Monthly / Annual).
4. User chooses a plan → taps **"Continue."**
5. Native store purchase dialog appears (App Store / Play Store).
6. On successful purchase:
   - Entitlement switches to **"Pro Access."**
   - Pro-only features unlock (scan limits removed, CRM sync, team features).
7. On reinstall, **"Restore Purchases"** revalidates the entitlement.

> **UI reference:** Lovable prototype — *"Bizcatchup x Revenuecat"*. Navigate the UI as a user would to see the included updates.

---

## 6. Functional Requirements (Frontend)

| ID | Requirement | Type | Description |
|----|-------------|------|-------------|
| FR-01 | Integrate RevenueCat SDK (iOS + Android) | Integration | Add SDK initialization within the BizCatchUp client. |
| FR-02 | Display RevenueCat paywall in-app | UI | Show paywall (monthly & annual pricing) before checkout. |
| FR-03 | Enable subscription purchase flow | Interaction | User subscribes via the native store flow managed by RevenueCat. |
| FR-04 | Allow restoring previous purchases | UI | "Restore Purchases" reinstates unlocked entitlements. |
| FR-05 | Show Terms & Privacy links | UI | Link to hosted policies below the paywall. |
| FR-06 | Dynamically fetch paywall details | Integration | Load paywall content from the RevenueCat dashboard. |
| FR-07 | Update UI on subscription activation | Functional | Unlock Pro-only features (CRM sync, analytics, unlimited scans). |
| FR-08 | Handle cancellation / expired state gracefully | Functional | Show downgrade prompt or return to free-tier UI. |
| FR-09 | Testing via test environment | QA | Complete frontend QA with test products before production. |

### Non-Functional Requirements

| ID | Requirement | Area | Target |
|----|-------------|------|--------|
| NFR-01 | Paywall load time | Performance | < 2 s on average network conditions |
| NFR-02 | SDK stability | Reliability | Paywall must not crash the app on load or transaction |
| NFR-03 | UI consistency | UX | Follows BizCatchUp brand theme & typography |
| NFR-04 | Data privacy | Security | No payment data stored locally; handled via native stores only |
| NFR-05 | Resilience | Reliability | Retry mechanism if network fails during paywall load |

---

## 7. Backend Integration (Phase 2 — Go / `scanner/`)

RevenueCat is the **authoritative source** for subscription data. The Go backend mirrors state into **Firestore** for fast, user-centric queries. The backend:
- receives webhook events,
- validates authenticity (Bearer token),
- updates subscription state,
- serves as the source of truth for user *access* within BizCatchUp.

### Data Flow
1. User initiates purchase on mobile (iOS/Android).
2. Payment processed by RevenueCat + platform (Apple/Google).
3. RevenueCat webhook fires with the subscription event.
4. Go backend receives the webhook, validates the Bearer token.
5. Backend extracts user ID, plan, status, duration.
6. Backend writes/updates the user's Firestore document.

### 7.1 Webhook Endpoint

```
POST /api/webhooks/revenuecat
```

**Responsibilities**
- Validate Bearer token from RevenueCat.
- Parse webhook payload (JSON).
- Extract subscription metadata (user ID, plan, status, duration).
- Async (non-blocking) write to Firestore, then respond `200` immediately.

**Request signature**

```
Authorization: Bearer <REVENUECAT_WEBHOOK_SECRET>
```

**Payload example**

```json
{
  "event": {
    "type": "INITIAL_PURCHASE",
    "app_user_id": "<firebase-uid>",
    "product_id": "plan_100",
    "expiration_at_ms": 1640000000000
  }
}
```

> **Wiring note:** In `scanner/`, HTTP routes live in `internal/routes/` (versioned) and per-domain handlers in `pkg/endpoints/`. Add a `revenuecat` (or `billing`) webhook handler under `pkg/endpoints/` and register the route in `internal/routes/`. The `app_user_id` is the **Firebase UID**, which the frontend passes as the RevenueCat `appUserID`.

### 7.2 Bearer Token Validation
1. Extract token from `Authorization` header.
2. Compare against `REVENUECAT_WEBHOOK_SECRET` (env var).
3. Return `401 Unauthorized` on mismatch; return `200 OK` after a successful enqueue/write.

### 7.3 Firestore Schema

**Collection:** `users` — **Document ID:** Firebase UID

| Field | Type | Description |
|-------|------|-------------|
| `plan` | String | Product ID from RevenueCat (e.g. `"plan_100"`) |
| `price` | Number | Subscription price (from RevenueCat metadata) |
| `status` | String | `"active"`, `"expired"`, `"cancelled"` |
| `expiresAt` | Timestamp | Expiration timestamp (from RevenueCat) |
| `updatedAt` | Timestamp | When the record was last synced |

### 7.4 Supported Event Types

| Event Type | Action |
|-----------|--------|
| `INITIAL_PURCHASE` | Create new subscription document with `"active"` status |
| `RENEWAL` | Update expiration timestamp, keep `"active"` |
| `EXPIRATION` | Update status to `"expired"` |
| `CANCELLATION` | Update status to `"cancelled"` |

### 7.5 Configuration

**Environment variable (required):**
```
REVENUECAT_WEBHOOK_SECRET=<bearer-token-from-dashboard>
```

**RevenueCat dashboard setup:**
1. Log into RevenueCat → **Project Settings → Webhooks**.
2. Create a webhook endpoint: `https://<backend-domain>/api/webhooks/revenuecat`.
3. Generate a Bearer token → copy to `REVENUECAT_WEBHOOK_SECRET`.
4. Enable all subscription event types (`INITIAL_PURCHASE`, `RENEWAL`, `EXPIRATION`, `CANCELLATION`).

### 7.6 Error Handling

| Code | Scenario | Action |
|------|----------|--------|
| `200` | Valid webhook | Firestore write enqueued; respond immediately |
| `401` | Invalid bearer token | Log security event; do not process |
| `400` | Malformed JSON payload | Log error; return `400` |
| `500` | Firestore write failure | Log error; return `500` (RevenueCat will retry) |

**Async processing:** the handler validates the token, enqueues the write (async task queue / goroutine), returns `200 OK` immediately, and processes the write in the background (log + retry on failure).

### 7.7 Backend Query — "does the user have an active subscription?"
1. Query `users` collection by user ID.
2. Check `status == "active"`.
3. Validate `expiresAt > now()`.

---

## 8. Integration Points

### 8.1 Frontend (Flutter)
- Use the RevenueCat SDK for the purchase flow.
- Pass the **Firebase UID** as the RevenueCat `appUserID` (this is the key that links webhook events to the Firestore `users/<uid>` doc).
- On success, verify the subscription in Firestore (mirrored data) before unlocking Pro features.

> **Codebase note:** RevenueCat setup currently has a stubbed hook — `initRevenueCat()` in `bizcatchup_flutter/lib/main.dart` is a no-op placeholder, and `lib/constants/revenuecat.dart` holds the setup keys (`androidSetupKey` / `iosSetupKey`). Implementation starts by filling in `initRevenueCat()` and wiring the paywall trigger points. RevenueCat is **native-only** — guard/skip it on web with `kIsWeb` (mirroring the analytics-SDK pattern already used for AppsFlyer/Trackier).

### 8.2 Backend
- Webhook handler + validation + Firestore mirror (see §7).

---

## 9. Success Metrics
- Paywall load success rate: **≥ 99%**
- Free → Pro conversion rate: **≥ 8%**
- Crash-free sessions during paywall flow: **≥ 99.5%**
- Purchase success rate (no UI errors): **≥ 98%**
- User satisfaction (NPS after purchase): **> 40**

---

## 10. Dependencies
- RevenueCat SDK (iOS, Android)
- App Store / Google Play in-app purchase setup
- API layer for entitlement sync (backend, Phase 2)
- Accurate Terms & Privacy URLs
- Test subscriptions enabled in sandbox environments

---

## 11. Risks & Mitigation

| Risk | Impact | Mitigation |
|------|--------|-----------|
| Paywall UI fails to load | Medium | Fallback screen + retry logic |
| Subscription not reflecting instantly | High | Cache entitlement locally until backend syncs |
| Pricing mismatch across stores | Medium | Keep App Store / Play Store configs consistent |
| SDK breaking with app updates | Medium | Version-control the SDK & regression test |
| Design inconsistency post-import | Low | Validate after Figma import; run UI QA |

---

## 12. Testing & Validation

### Local backend testing (webhooks)
Use ngrok (or similar) to expose the local backend:
```bash
ngrok http 9876   # scanner backend port
```
Configure the RevenueCat webhook URL to `https://<ngrok-id>.ngrok.io/api/webhooks/revenuecat`.

### Validation checklist
- [ ] Bearer token validation rejects invalid tokens (`401`).
- [ ] Valid webhook creates/updates the Firestore document.
- [ ] User ID extracted correctly (Firebase UID as document ID).
- [ ] Subscription status transitions work correctly.
- [ ] Expiration timestamps are parsed and stored correctly.

### Frontend QA
- [ ] Complete purchase flow via the **Test Store** with test products before production.

---

## 13. Monitoring & Logging

**Metrics:** webhook request count (by event type); authorization failures; Firestore write success/failure rates; end-to-end latency (RevenueCat event → Firestore write).

**Alerts:** high rate of `401`s (potential security issue); Firestore write error rate > 5%; no webhook events received in 24h.

---

## 14. Next Steps
1. Finalize Figma design import or confirm component-based paywall design.
2. Integrate the RevenueCat SDK in the Flutter frontend (start at `initRevenueCat()` in `main.dart`).
3. Connect paywall trigger points in the app flow (e.g. scan-limit reached, "Upgrade to Pro").
4. Conduct test purchases via the Test Store.
5. Backend integration of webhook + entitlement validation (Phase 2).
6. Roll out to beta users for subscription testing.
