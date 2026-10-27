# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Workspace layout

`BizCatchup/` is a workspace folder (not itself a git repo) containing two **independent git repositories** for the same product — a business-networking app for creating, scanning, and sharing digital business cards:

- **`scanner/`** — Go backend (git branch: `stage`). Module `github.com/NookPay/mould`, builds to a binary named `mould`. Serves the REST API on port `9876`, deployed at `https://backend.bizcatchup.com`. **Has its own detailed `scanner/CLAUDE.md` — read it before working in this directory.**
- **`biz-scan-flutter/`** — Flutter client (git branch: `master`). Contains the actual Flutter project in the `bizcatchup_flutter/` subdirectory, plus a native iOS/macOS Xcode project in `bizcatchup/`.

The two are connected only over HTTP: the Flutter app's backend base URL is defined in `biz-scan-flutter/bizcatchup_flutter/lib/constants/api.dart` (`bizScanBaseURL = https://backend.bizcatchup.com`). There is no shared code or build between them — commit, build, and test each repo separately.

## Backend — `scanner/` (Go)

See `scanner/CLAUDE.md` for architecture. Quick reference (run from `scanner/`):

```bash
go run main.go                         # run locally (port 9876)
go build -o mould main.go              # build binary (or ./build.sh)
docker build -t bizcatchup-scanner .   # containerized build (needs libvips)
docker run -p 9876:9876 --env-file .env bizcatchup-scanner
```

- Entry point `main.go` → `cmd.RootCommand()` (Cobra). `cmd/bin.go` bootstraps all service managers concurrently, injects them into the global `pipeline/`, then starts the Gin HTTP server.
- HTTP routes live in `internal/routes/` (versioned `v1`/`v2`); per-domain handlers in `pkg/endpoints/` (businesscards, digitalcards, integrations, teams, users, wallet, workflows, billing, labels, feedback, appversion).
- Config is Viper + `.env` (`godotenv`); needs credentials for Firebase/Firestore, Gemini, Azure Document Intelligence OCR, ZeptoMail, and Typesense. CI/CD is Drone (`.drone.yml`) triggered on `stage`/`master`.

## Client — `biz-scan-flutter/bizcatchup_flutter/` (Flutter)

Package name `BizScanner`. **All Flutter commands must run from `biz-scan-flutter/bizcatchup_flutter/`**, not the repo root.

```bash
flutter pub get                        # install dependencies
flutter run                            # run on connected device/emulator
flutter build apk / ios / web          # build for a platform
flutter test                           # run all widget/unit tests
flutter test test/foo_test.dart        # run a single test file
flutter analyze                        # lint (analysis_options.yaml)
```

- Dart SDK constraint: `>=2.17.5 <=3.9.0`. Firebase config in `lib/firebase_options.dart` (regenerate with `flutterfire configure`).
- Entry point `lib/main.dart`. Feature code under `lib/` is grouped by feature area (`business_cards/`, `digital/`, `camera/`, `integrations/`, `teams/`, `workflows/`, `settings/`) rather than by layer; shared pieces in `base/`, `comon_widget/` (note spelling), `constants/`, `utils/`, `services/`.
- State/local storage: `provider` + `shared_preferences`. Card scanning uses Google ML Kit document scanner + `edge_detection`. Firebase provides auth (Google/Apple/email), Firestore, Storage, Messaging, App Check, Crashlytics, Analytics. Wallet passes via `apple_passkit` / `google_wallet`.
- Attribution/analytics SDKs live in `lib/services/` (all orchestrated through `analytics_service.dart`): **AppsFlyer** (`appsflyer_sdk`), **AppTrove** (`apptrove_sdk_flutter` — migrated from the older Trackier SDK), **Airbridge** (`airbridge_flutter_sdk`), and **Meta** (`facebook_app_events`). `session_service.dart` tracks app sessions. These are native-only; they're skipped on web.
- Billing/subscriptions: **RevenueCat** (`purchases_flutter` + `purchases_ui_flutter`) — `initRevenueCat()` in `main.dart`, paywall via `services/paywall_service.dart`, keys/entitlement in `constants/revenuecat.dart` (entitlement id `premium`). Native-only; requires `MainActivity` to extend `FlutterFragmentActivity`. See `REVENUECAT_INTEGRATION.md` for the full plan.
- Some dependencies are pinned to git forks and `dependency_overrides` exist (e.g. `intl`, `grpc`, `open_file_mac`) to keep iOS/Xcode 16 builds working — preserve these when touching `pubspec.yaml`.
- **Pointing the app at a local backend**: `lib/constants/api.dart` has `API.useLocalBackend` (default `false`, hitting the deployed `https://backend.bizcatchup.com`). To test against a local `scanner` run (`go run main.go`, port 9876), set it to `true` — `bizScanBaseURL` then resolves to `http://localhost:9876` on iOS/web, or `http://<_localBackendHost>:9876` on Android (physical device/emulator can't reach `localhost`, so `_localBackendHost` is hardcoded to the dev machine's LAN IP — update it via `ipconfig getifaddr en0` whenever that IP changes). **Always flip `useLocalBackend` back to `false` before building for release.**

## Working across both repos

When a change spans client and backend (e.g. a new endpoint), update the API contract in `scanner/pkg/endpoints/` and the corresponding Dart service/model in the Flutter app, and verify against `scanner/API_DOC.md`. Because they are separate repos on different branches, make and commit the changes in each repo independently.

## graphify

This project has a knowledge graph at graphify-out/ with god nodes, community structure, and cross-file relationships.

Rules:
- For codebase questions, first run `graphify query "<question>"` when graphify-out/graph.json exists. Use `graphify path "<A>" "<B>"` for relationships and `graphify explain "<concept>"` for focused concepts. These return a scoped subgraph, usually much smaller than GRAPH_REPORT.md or raw grep output.
- If graphify-out/wiki/index.md exists, use it for broad navigation instead of raw source browsing.
- Read graphify-out/GRAPH_REPORT.md only for broad architecture review or when query/path/explain do not surface enough context.
- After modifying code, run `graphify update .` to keep the graph current (AST-only, no API cost).
