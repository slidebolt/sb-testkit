# Git Workflow for sb-testkit

This repository contains the Slidebolt Testkit, providing utilities for integration and E2E testing of Slidebolt services and plugins.

## Dependencies
- **Internal:**
  - `sb-domain`: Shared domain models.
  - `sb-messenger-sdk`: Shared messaging interfaces.
  - `sb-script`: Scripting engine (for testing automations).
  - `sb-storage-sdk`: Shared storage interfaces.
  - `sb-storage-server`: Storage implementation for test environments.
  - `sb-virtual`: Virtual device provider for testing.
- **External:** 
  - Standard Go library and NATS.

## Build Process
- **Type:** Pure Go Library (Test Module).
- **Consumption:** Imported as a module dependency in other projects' test files (`_test.go`).
- **Artifacts:** No standalone binary or executable is produced.
- **Validation:** 
  - Validated through unit tests (if any).
  - Validated by its consumers during their respective integration/E2E test cycles.

## Pre-requisites & Publishing
As a testing utility, `sb-testkit` must be updated whenever any of the core SDKs or implementation services are changed.

**Before publishing:**
1. Determine current tag: `git tag | sort -V | tail -n 1`
2. Ensure it compiles correctly within its own context.

**Publishing Order:**
1. Ensure all internal dependencies are tagged and pushed.
2. Update `sb-testkit/go.mod` to reference the latest tags.
3. Determine next semantic version for `sb-testkit` (e.g., `v1.0.4`).
4. Commit and push the changes to `main`.
5. Tag the repository: `git tag v1.0.4`.
6. Push the tag: `git push origin main v1.0.4`.

## Update Workflow & Verification
1. **Modify:** Update testing utilities in `testenv.go` or `spy.go`.
2. **Verify Local:**
   - Run `go mod tidy`.
   - Run `go build ./...` to ensure no compilation errors.
3. **Commit:** Ensure the commit message clearly describes the testkit change.
4. **Tag & Push:** (Follow the Publishing Order above).
