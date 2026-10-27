# TEST_BLUEPRINT.md

Full test-scenario blueprint for BizCatchup — covers the Go backend (`scanner/`) and the Flutter client (`biz-scan-flutter/bizcatchup_flutter/`). Organized by layer (Backend API / Frontend UI), then by feature. Check items off as tests are written.

**Baseline coverage at time of writing:**
- Backend: only 3 test files exist (`config/parse_test.go`, `pkg/db/teams/teams_test.go`, `pkg/endpoints/billing/revenuecat_test.go`) — all pure-logic, no HTTP-handler-level tests.
- Frontend: zero tests, no `test/` directory.

---

## BACKEND API — Go (`scanner/`)

### Auth & Middleware
- [ ] Firebase auth middleware: valid token passes
- [ ] Firebase auth middleware: expired token → 401
- [ ] Firebase auth middleware: malformed token → 401
- [ ] Firebase auth middleware: missing `Authorization` header → 401
- [ ] Firebase auth middleware: token for a deleted/nonexistent user → 401/403
- [ ] Admin middleware: valid admin email passes
- [ ] Admin middleware: non-admin authenticated user hits admin route → 403
- [ ] Admin middleware: token claims missing email field
- [ ] `Authentication()` basic-auth no-op: regression test proving any colon-containing credential currently passes (documents known gap)
- [ ] Unauthenticated devops/fix-* routes: anonymous request to `/team/:teamID/fix-count`
- [ ] Unauthenticated devops/fix-* routes: anonymous request to `/users/:userID/fix-team`
- [ ] Unauthenticated devops/fix-* routes: anonymous request to `/empty-teams-data`
- [ ] Unauthenticated devops/fix-* routes: anonymous request to `/business-cards/groups` (FixGroupType)
- [ ] Unauthenticated devops/fix-* routes: anonymous request to `/devops/*` invite endpoints
- [ ] Unauthenticated devops/fix-* routes: anonymous request to `/bulkProcessProgress/:requestID`
- [ ] Firebase init failure at startup: v1/v2 routes 404 instead of 500
- [ ] Firebase init failure at startup: `/health` and `/status` still respond

### Business Cards — Scan (v1 & v2)
- [ ] Happy path: 1-image scan
- [ ] Happy path: 2-image (front/back) scan
- [ ] Missing/corrupt image upload
- [ ] Unsupported image format
- [ ] Oversized image
- [ ] Zero images provided
- [ ] More than 2 images provided (`CombineImages` error path)
- [ ] Azure OCR returns non-202 initial response
- [ ] Azure OCR polling never reaches `succeeded` within 10 retries → timeout surfaced
- [ ] Azure OCR returns partial fields (verify no panic on type assertions)
- [ ] Gemini returns empty candidates/parts → graceful degrade, no nil-pointer panic
- [ ] Gemini returns malformed JSON → unmarshal error handled, no panic
- [ ] Phone/email/website regex validators: valid formats
- [ ] Phone/email/website regex validators: invalid formats
- [ ] Phone/email/website regex validators: empty strings
- [ ] Phone/email/website regex validators: international/unicode phone formats
- [ ] Phone/email/website regex validators: multiple values in one field
- [ ] QR scan: valid QR from hihello
- [ ] QR scan: valid QR from popl
- [ ] QR scan: valid QR from linq
- [ ] QR scan: valid QR from generic provider
- [ ] QR scan: malformed QR payload
- [ ] QR scan: unsupported provider name
- [ ] QR scan: empty QR data
- [ ] Scan limit (v2): under daily/total limit → success
- [ ] Scan limit (v2): exactly at limit → blocked with `ErrScanLimitReached`
- [ ] Scan limit (v2): unlimited (zero = unlimited) → always allowed
- [ ] **Race**: N concurrent scans from same team with 1 slot remaining → exactly 1 succeeds via Firestore transaction
- [ ] Fire-and-forget post-response goroutine: assert eventual side effect (group/label count) without blocking response
- [ ] Fire-and-forget post-response goroutine: failure doesn't crash process or corrupt shared state
- [ ] Import (CSV): valid file
- [ ] Import (XLSX): valid file
- [ ] Import: missing headers
- [ ] Import: extra/unknown columns
- [ ] Import: empty file
- [ ] Import: corrupt file with correct extension
- [ ] Import: huge file (row-count stress)
- [ ] Manual create: all fields present
- [ ] Manual create: only required-equivalent fields present
- [ ] Manual create: duplicate detection by email
- [ ] Manual create: duplicate detection by phone
- [ ] Manual create: no duplicates
- [ ] Rescan: existing card ID
- [ ] Rescan: non-existent ID
- [ ] Rescan: card owned by a different team (authorization boundary)

### Business Cards — CRUD/List/Export
- [ ] List: pagination page 0
- [ ] List: pagination last page
- [ ] List: pagination beyond range
- [ ] List: empty result set
- [ ] List: search query matching
- [ ] List: search query non-matching
- [ ] List: filter combinations (group/label/favorite/status)
- [ ] Get: existing ID
- [ ] Get: non-existent ID
- [ ] Get: ID belonging to another team
- [ ] Update: partial update
- [ ] Update: full update
- [ ] Update: malformed nested `Addresses`/`image_url` shapes (string vs array)
- [ ] Bulk group/label associate: empty array
- [ ] Bulk group/label associate: single item
- [ ] Bulk group/label associate: large batch
- [ ] Bulk group/label associate: mix of valid/invalid card IDs
- [ ] Bulk group/label associate: malformed `Operation` payload rejected
- [ ] Delete (bulk): delete existing
- [ ] Delete (bulk): delete already-deleted
- [ ] Delete (bulk): delete IDs from another team
- [ ] Delete (bulk): 3 sequential async goroutines don't race — final counts correct regardless of ordering
- [ ] Download export: xlsx happy path
- [ ] Download export: csv happy path
- [ ] Download export: pdf happy path
- [ ] Download export: unsupported `:type` value
- [ ] Download export: zero cards to export
- [ ] Download export: very large export (memory/streaming)
- [ ] Lead capture (public): valid submission
- [ ] Lead capture (public): missing required-ish fields
- [ ] Lead capture (public): spam/garbage payload
- [ ] Lead capture (public): duplicate submission
- [ ] devops.go unbounded fan-out: large collection backfill resource behavior
- [ ] devops.go unbounded fan-out: DB error mid-fan-out doesn't deadlock/panic

### Digital Business Cards
- [ ] Create: happy path with image
- [ ] Create: happy path without image
- [ ] Create: multipart upload fails partway (no orphaned Storage file, or documented)
- [ ] Update: existing card
- [ ] Update: non-existent card
- [ ] Update: nested `ConnectFields`/`QRCodeSetting` structures
- [ ] Get by share_id: valid
- [ ] Get by share_id: invalid/nonexistent
- [ ] Get by share_id: deleted card
- [ ] Get by share_id: expired/deactivated card (if state exists)
- [ ] Generate AI description: Gemini returns valid text
- [ ] Generate AI description: Gemini errors/times out
- [ ] Generate AI description: empty input fields
- [ ] Delete: existing
- [ ] Delete: already-deleted
- [ ] Delete: by non-owner

### Teams
- [ ] Invite within member limit
- [ ] Invite exceeding `MemberLimit()` → `memberAllowanceError`
- [ ] Invite duplicate email (already member)
- [ ] Invite duplicate email (already invited)
- [ ] Accept invite: valid code
- [ ] Accept invite: expired/used code
- [ ] Accept invite: code for wrong user/email
- [ ] Cancel invite: pending invitation
- [ ] Cancel invite: already-accepted invitation
- [ ] Resend invite: pending invitation
- [ ] Change ownership: valid transfer
- [ ] Change ownership: transfer to non-member
- [ ] Change ownership: transfer to self
- [ ] Remove member / change role / leave team: last-owner-leaves edge case
- [ ] Remove member / change role / leave team: remove self
- [ ] Remove member / change role / leave team: remove non-member
- [ ] Remove member / change role / leave team: invalid role value
- [ ] **Race**: admin manual `UpdatePlan` vs RevenueCat webhook writing same `team-plan` doc simultaneously
- [ ] SubscriptionType: free/pro/team/enterprise happy paths
- [ ] SubscriptionType: empty string fails closed
- [ ] SubscriptionType: unknown/garbage value fails closed (HTTP-level, gated endpoint)
- [ ] devops invite variants: same invite scenarios, flagged unauthenticated

### Billing / RevenueCat Webhook
- [ ] Valid bearer + valid event body → 200, team plan updated
- [ ] Missing bearer → 401/403
- [ ] Wrong bearer → 401/403
- [ ] Missing `event.Type` → 400
- [ ] Missing `event.AppUserID` → 400
- [ ] Event for unknown team → 200 "ignored", no write
- [ ] Unknown event type → 200 "ignored"
- [ ] Superseded expiration: EXPIRATION/REFUND for already-superseded product is ignored
- [ ] Superseded expiration: doesn't downgrade a currently-active newer plan
- [ ] Async Firestore write failure: webhook still returns 200 (documented contract)
- [ ] Async Firestore write failure: failure at least logged
- [ ] Duplicate webhook delivery: idempotent, no double-apply
- [ ] Out-of-order delivery: older event after newer event doesn't regress state

### Wallet
- [ ] Apple Wallet: all required fields present → success
- [ ] Apple Wallet: each required field (Name/Company/Title/Email) individually missing → 400
- [ ] Apple Wallet: optional fields (Phone/QRCodeURL) omitted → still succeeds
- [ ] Apple Wallet: async pass-generation goroutine response semantics (sent before/after generation)
- [ ] Apple Wallet: generation fails after response already sent
- [ ] Google Wallet JSON: valid team/card
- [ ] Google Wallet JSON: missing card
- [ ] Wallet cleanup goroutines respect shutdown signal, no temp-file leak

### Labels & Groups
- [ ] Create label/group: valid name
- [ ] Create label/group: empty name
- [ ] Create label/group: duplicate name within same team
- [ ] Create label/group: name collision across teams is independent
- [ ] Rename: valid rename
- [ ] Rename: rename to already-existing name
- [ ] Rename: rename non-existent label/group
- [ ] Delete: cascades to remove refs from all associated cards
- [ ] Delete: label/group referenced by many cards (bulk update path)
- [ ] Delete: non-existent label/group

### Integrations / OAuth / Contacts Sync
- [ ] OAuth create/redirect: valid provider redirect with code
- [ ] OAuth create/redirect: invalid/expired code
- [ ] OAuth create/redirect: `fetchToken` exchange failure
- [ ] OAuth create/redirect: unsupported provider name
- [ ] Delete OAuth app: existing integration
- [ ] Delete OAuth app: already-deleted
- [ ] Get/create contacts: single contact create
- [ ] Get/create contacts: update existing contact
- [ ] Get/create contacts: malformed contact payload
- [ ] Bulk contacts: empty batch
- [ ] Bulk contacts: small batch
- [ ] Bulk contacts: large batch respects `maxConcurrent` semaphore
- [ ] Bulk contacts: one bad contact doesn't abort rest of batch
- [ ] Bulk contacts: **race** on `sync.Map progressStore` — concurrent poll reads during in-flight writes
- [ ] Bulk contacts: progress polling before job starts
- [ ] Bulk contacts: progress polling mid-job
- [ ] Bulk contacts: progress polling after completion
- [ ] Bulk contacts: progress polling after failure
- [ ] Bulk contacts: progressStore memory-leak check across many jobs
- [ ] Each provider (hubspot/zoho/salesforce/google-contacts): auth token expired mid-sync
- [ ] Each provider: rate-limited response
- [ ] Each provider: malformed contact data returned

### Workflows
- [ ] Create/update/delete: valid config
- [ ] Create/update/delete: invalid `IntegrationName`
- [ ] Create/update/delete: empty `Filter.Groups`
- [ ] Create/update/delete: workflow referencing deleted group/label
- [ ] Execution: card matching filter triggers integration push
- [ ] Execution: card not matching filter does nothing
- [ ] Execution: integration call fails mid-execution

### Feedback & App Version
- [ ] Feedback: empty email
- [ ] Feedback: malformed email
- [ ] Feedback: empty feedback string
- [ ] Feedback: extremely long feedback string
- [ ] Feedback: HTML/script injection in feedback text (stored-XSS check, public unauth endpoint)
- [ ] App version: valid version int
- [ ] App version: zero value (flagged gap — `binding:"required"` on int rejects 0)
- [ ] App version: negative version
- [ ] App version: non-numeric input

### Config / Startup
- [ ] Missing `.env` file → app starts with soft warning
- [ ] Missing Azure DI credentials → fatal startup
- [ ] Missing `ZEPTOMAIL_API_KEY` → fatal startup
- [ ] Missing `GEMINI_API_KEY` → fatal startup
- [ ] Missing/invalid `GOOGLE_APPLICATION_CREDENTIALS` → fatal startup
- [ ] Missing `RevenueCatConfig.WebhookSecret` → not fatal at startup, 500 at request time
- [ ] Viper zero/false value vs unset value (known silent-skip behavior) documented
- [ ] Typesense dead-code path excluded or flagged

### Graceful Shutdown / Concurrency
- [ ] SIGTERM/SIGINT mid-request: in-flight requests complete
- [ ] SIGTERM/SIGINT mid-request: new requests rejected
- [ ] SIGTERM/SIGINT mid-request: `GRACEFUL_TIMEOUT` forces exit on hung goroutines
- [ ] Cron heartbeat respects context cancellation on shutdown
- [ ] Process killed immediately after response sent, before async goroutine completes — no corrupted partial state

### Network / External API Dropout
- [ ] Firestore unavailable/timeout on read
- [ ] Firestore unavailable/timeout on write
- [ ] Firestore unavailable/timeout on transaction
- [ ] Firebase Storage unavailable during upload
- [ ] Firebase Storage unavailable during download
- [ ] Azure OCR unreachable/DNS failure/TLS error
- [ ] Azure OCR slow response near 60s timeout boundary
- [ ] Gemini API unreachable
- [ ] Gemini API rate-limited (429)
- [ ] Gemini API auth failure (bad/expired key)
- [ ] ZeptoMail unreachable
- [ ] ZeptoMail rejects with 4xx (bad template ID)
- [ ] ZeptoMail rejects with 5xx
- [ ] Firebase Auth token verification service unreachable
- [ ] Partial mid-operation failure (OCR succeeds, Gemini fails) — no half-written card record

---

## FRONTEND UI — Flutter (`bizcatchup_flutter/`)

### Authentication
- [ ] Google sign-in: fresh sign-in
- [ ] Google sign-in: sign-in while anonymous (link vs replace)
- [ ] Google sign-in: `provider-already-linked` conflict → proceed (destructive, wipes guest data)
- [ ] Google sign-in: `provider-already-linked` conflict → cancel
- [ ] Google sign-in: `credential-already-in-use` conflict
- [ ] Google sign-in: user cancels sign-in
- [ ] Google sign-in: network failure mid-sign-in
- [ ] Google sign-in: Play Services unavailable
- [ ] Apple sign-in: availability check on unsupported device/OS
- [ ] Apple sign-in: nonce/hash validation
- [ ] Apple sign-in: `SignInWithAppleAuthorizationException` cancel code suppressed
- [ ] Apple sign-in: other exception codes surfaced
- [ ] Apple sign-in: link vs fresh sign-in
- [ ] Apple sign-in: network failure mid-flow
- [ ] Anonymous sign-in: fresh install happy path
- [ ] Anonymous sign-in: later linking to Google/Apple
- [ ] Anonymous sign-in: network failure
- [ ] Email/password: wrong password
- [ ] Email/password: invalid email format
- [ ] Email/password: user-not-found
- [ ] Email/password: email-already-in-use
- [ ] Email/password: network-request-failed
- [ ] Error mapper: table-driven test of every Firebase error code through `ErrorText.localizeError`
- [ ] Error mapper: table-driven test of platform error codes through `ErrorText.localizePlatformError`
- [ ] Sign-out: clears local session tokens
- [ ] Sign-out: clears analytics identity
- [ ] Sign-out: doesn't crash if already signed out
- [ ] Single-device session: second device sign-in invalidates first device's session
- [ ] Single-device session: network error during validation treated as valid (documented leniency)
- [ ] Single-device session: app resume triggers re-validation via lifecycle observer

### Camera / Scanning
- [ ] Web: file picker happy path
- [ ] Web: user cancels picker
- [ ] Android (ML Kit): 1-page scan
- [ ] Android (ML Kit): 2-page scan
- [ ] Android (ML Kit): gallery import
- [ ] Android (ML Kit): user cancels scanner
- [ ] Android (ML Kit): `result.images.isEmpty` silent failure handled internally
- [ ] iOS: camera permission granted → scan proceeds
- [ ] iOS: camera permission denied → silent early return
- [ ] iOS: two-sided scan, both sides succeed
- [ ] iOS: two-sided scan, first succeeds/second fails
- [ ] iOS: `PlatformException` "cancelled" → toast shown
- [ ] iOS: other exception → generic error toast
- [ ] Post-scan: network dropout between capture and upload

### Business Card List / Management
- [ ] List: loading state renders
- [ ] List: error state renders
- [ ] List: empty state renders (`EmptyListView`)
- [ ] List: populated state renders
- [ ] List: pagination scroll-to-load-more
- [ ] Search: query matches
- [ ] Search: query matches nothing
- [ ] Search: query cleared
- [ ] Filters: single filter applied
- [ ] Filters: combined filters (group + label + favorite)
- [ ] Filters: bottom sheet cancel vs apply
- [ ] Filters: range slider min/max/min==max
- [ ] Bulk ops: select all
- [ ] Bulk ops: select none
- [ ] Bulk ops: select then deselect
- [ ] Bulk ops: export each format
- [ ] Bulk ops: delete confirm accept
- [ ] Bulk ops: delete confirm cancel
- [ ] Bulk ops: group/label assign with mixed selection
- [ ] Count providers: concurrent async count updates race (`setTotalCardCount(Future<int>)`)
- [ ] Count providers: decrement guard against negative counts
- [ ] Contact export: valid contact
- [ ] Contact export: missing fields
- [ ] Contact export: device contacts permission denied
- [ ] Phone contacts sync: permission granted
- [ ] Phone contacts sync: permission denied
- [ ] Phone contacts sync: empty contact list
- [ ] Phone contacts sync: large contact list
- [ ] File download: each platform variant (io/web/stub)
- [ ] File download: interrupted download
- [ ] File download: disk full (mobile)

### Digital Business Cards
- [ ] Setup wizard: step-by-step happy path
- [ ] Setup wizard: back-navigation preserves state
- [ ] Setup wizard: incomplete required fields blocks progress
- [ ] Setup wizard: image upload failure mid-wizard
- [ ] Setup wizard: network dropout during save
- [ ] Card preview/share: valid share link renders
- [ ] Card preview/share: copy link / generate QR
- [ ] Card preview/share: revoked/deleted card via old link
- [ ] Subscription home banner: correct copy per tier
- [ ] Subscription home banner: hidden for premium users
- [ ] Subscription home banner: tap navigates to plan screen

### Teams
- [ ] MyTeamHomePage: loading state
- [ ] MyTeamHomePage: error state
- [ ] MyTeamHomePage: empty state
- [ ] MyTeamHomePage: live update via StreamBuilder when membership changes elsewhere
- [ ] Invite: send happy path
- [ ] Invite: at member limit blocked
- [ ] Invite: resend
- [ ] Invite: cancel pending
- [ ] Invite: accept via deep link
- [ ] Role change / remove member / leave team (including last-member-leaves)
- [ ] Change ownership
- [ ] `Team` model: `isPremium()`/`hasTeamAccess()`/`planLabel()` across all tiers incl. unknown/empty (fail-closed)

### RevenueCat / Paywall / Subscriptions
- [ ] `initRevenueCat()`: web no-op path
- [ ] `initRevenueCat()`: native init success
- [ ] `initRevenueCat()`: native init failure (bad key/network)
- [ ] `initRevenueCat()`: test-store vs platform key selection
- [ ] Paywall: generic offering presents
- [ ] Paywall: specific offering by ID with fallback to current
- [ ] Paywall: offering with empty packages → `PaywallResult.error`
- [ ] Purchase: successful purchase updates entitlement
- [ ] Purchase: cancelled purchase (`purchaseCancelledError`) handled correctly
- [ ] Purchase: payment pending state
- [ ] Purchase: attempted while offline
- [ ] Plan change: upgrade (immediate proration) happy path
- [ ] Plan change: downgrade (deferred) happy path
- [ ] Plan change: no existing `current.productId` → error path
- [ ] Plan change: network dropout mid-purchase
- [ ] Restore: Customer Center presents correctly
- [ ] Restore: decide/test explicit in-app "Restore Purchases" need
- [ ] Identity: concurrent purchase attempt while `identify()` in-flight — `_awaitIdentify()` guard blocks correctly
- [ ] Identity: logout releases identity correctly
- [ ] **Reconciliation race**: RevenueCat premium, Firestore webhook not yet landed → UI shows premium immediately
- [ ] **Reconciliation race**: Firestore premium, RevenueCat free (stale) → local view does NOT downgrade
- [ ] **Reconciliation race**: webhook arrives late with lapsed/expired status after a fresh purchase
- [ ] `planLoaded` false until first snapshot — spinner shows, no premature "free" flash

### Integrations
- [ ] OAuth connect: happy path per provider (Google/Outlook/CSV)
- [ ] OAuth connect: user cancels mid-flow
- [ ] OAuth connect: token exchange failure
- [ ] OAuth connect: already-connected provider reconnect
- [ ] CSV import: valid CSV
- [ ] CSV import: malformed CSV
- [ ] CSV import: empty CSV
- [ ] CSV import: huge CSV (UI responsiveness)
- [ ] Bulk contact push: progress UI reflects backend state at start/mid/complete/fail
- [ ] Bulk contact push: network dropout while polling

### Workflows
- [ ] Create/edit form: all fields valid
- [ ] Create/edit form: missing required integration selection
- [ ] Create/edit form: filter with no groups selected
- [ ] Run history: empty history
- [ ] Run history: populated history
- [ ] Run history: failed run surfaced correctly

### Analytics / Session Services
- [ ] Each fan-out service (AppsFlyer/Apptrove/Airbridge/Meta): assert side effects since exceptions are swallowed
- [ ] Apptrove: ATT prompt user grants
- [ ] Apptrove: ATT prompt user denies
- [ ] Apptrove: prompt already answered, not re-shown
- [ ] Airbridge: true no-op on iOS/web (no crash, no event sent)
- [ ] Identity sync dedupe: rapid repeated sync calls collapse into one
- [ ] Identity sync: re-fires after team change
- [ ] FCM token: obtained successfully
- [ ] FCM token: refresh mid-session
- [ ] FCM token: notification permission denied, token still obtainable per platform

### State Providers — Cross-cutting Races
- [ ] `LimitProvider`: teamConfig arrives before appConfig
- [ ] `LimitProvider`: teamConfig arrives after appConfig
- [ ] `LimitProvider`: listener init failure degrades to sane default (not crash)
- [ ] `TeamSettingsProvider`: concurrent local edit + incoming Firestore snapshot, no data loss/flicker
- [ ] `ModelTheme.setIsDark` no-op regression test (toggling has no visual effect)
- [ ] `BusinessCardSettings` not registered in `MultiProvider` — confirm dead code or reachable bug

### Local Storage / Persistence
- [ ] Fresh install: sane defaults for sort/theme/export-format/list-view
- [ ] Corrupted/unexpected value type stored under a SharedPreferences key
- [ ] Per-user vs per-team `save_to_contact_externally` keys don't collide on same device
- [ ] Storage cleared mid-session on another device vs local session state mismatch

### Network Dropout Scenarios (cross-cutting)
- [ ] Fully offline at launch: auth check shows correct state
- [ ] Fully offline at launch: team/plan load shows correct state
- [ ] Fully offline at launch: card list load shows correct state (not infinite spinner)
- [ ] Network drops mid-request: card scan upload
- [ ] Network drops mid-request: digital card save
- [ ] Network drops mid-request: invite send
- [ ] Network drops mid-request: purchase
- [ ] Network drops mid-request: OAuth token exchange
- [ ] Network restored after drop: pending listeners reconcile without duplicate/stale UI
- [ ] Slow network: scan upload timeout behavior
- [ ] Slow network: OCR wait timeout behavior
- [ ] Slow network: Gemini description generation timeout behavior

### Build Config (flagged, verify before automating)
- [ ] Confirm `useLocalBackend` flag behavior in `api.dart` before running frontend tests in CI (currently hardcoded to a LAN dev IP)

---

## CROSS-REPO CONTRACT TESTS
- [ ] Every `api.dart` route mapping matches current Go handler request/response shape
- [ ] `BulkAssociateGroupOrLabel` flexible `UnmarshalJSON` matches what Flutter service actually sends
- [ ] End-to-end: purchase on device → RevenueCat webhook → Firestore update → Flutter `TeamPlanProvider` reflects premium (realistic latency)
- [ ] End-to-end: webhook never arrives — Flutter still reflects correct state per reconciliation rules
- [ ] End-to-end: webhook arrives late with a superseded/expired event — no incorrect downgrade

---

## Known Gaps (blockers to "100%", not test items)
- Several devops/backfill routes and the no-op basic-auth middleware are real security gaps — decide fix-before-or-alongside-testing.
- Typesense is wired for config/init but never connected in `pipeline.go`/`cmd/bin.go` — dead code, exclude from coverage targets unless activated.
- `useLocalBackend` hardcoded true in `api.dart` will break CI-run frontend tests pointed at a real backend.
