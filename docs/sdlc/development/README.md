# Development

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
### DEV-PLAN-001 · approved · source: plan

Approved 7-sprint delivery plan (version 1), each sprint capacity 20 points, sequencing the full product backlog from account/onboarding through beta release conditions.

Sprint 1: Account creation, onboarding profile capture and daily target derivation. Sprint 2: Indian food catalogue, profile editing, camera and gallery photo capture. Sprint 3: AI dish recognition from photos, household portion units and catalogue search. Sprint 4: Estimate review screen -- approximate labelling, alternatives, error handling, dish swap, portion adjust, manual entry. Sprint 5: Meal saving, item add/remove, discard, correction feedback capture and catalogue source traceability. Sprint 6: Home screen with intake vs targets, meal grouping, history browsing, editing and deletion. Sprint 7: Weight log, beta release conditions -- free access, English-only, privacy controls and wellness disclaimers.

**Related:** EPIC-001, EPIC-002, EPIC-003, EPIC-004, EPIC-005, EPIC-006, EPIC-007, EPIC-008

- ⚠ The input gives sprint goals and a separate flat backlog of stories/tasks, but does not state which specific backlog items were assigned to which sprint -- that mapping could not be reconstructed without guessing.
- ⚠ No completion, in-progress, or blocked status is reported for any sprint or backlog item, so it cannot be confirmed how much of this plan has actually been executed.

### DEV-EPIC-001 · approved · source: plan:EPIC-001

Planned backlog for account creation, OAuth sign-in, onboarding and target derivation/editing.

US-001 (5 pts, backend-agent): users table/auth schema (backend-agent), POST /auth/signup (backend-agent), POST /auth/login (backend-agent), mobile sign-up/sign-in screens (frontend-agent). US-002 (5 pts, integration-agent): POST /auth/oauth (integration-agent), Google Sign-In SDK integration (integration-agent), Apple Sign-In on iOS (integration-agent), platform-conditional sign-in UI (frontend-agent). US-003 (5 pts, frontend-agent): user_profiles table/migration (backend-agent), POST /profile (backend-agent), onboarding wizard screens (frontend-agent), post-onboarding navigation logic (frontend-agent). US-004 (3 pts, backend-agent): user_targets table/migration (backend-agent), configurable target calculation (backend-agent), target display with wellness disclaimer (frontend-agent). US-005 (3 pts, frontend-agent): GET/PUT /profile (backend-agent), profile view/edit screen (frontend-agent), sign-out flow (frontend-agent).

**Related:** US-001, US-002, US-003, US-004, US-005

- ⚠ No implementation status (done/in-progress/blocked) reported for any task in this epic.

### DEV-EPIC-002 · approved · source: plan:EPIC-002

Planned backlog for camera/gallery capture and AI dish recognition.

US-006 (5 pts, frontend-agent): Expo Camera module/permissions, camera capture screen, wiring capture output to analysis flow (all frontend-agent). US-007 (3 pts, frontend-agent): Expo Image Picker integration, reuse of capture preview for gallery images (frontend-agent). US-008 (8 pts, integration-agent): S3 photo upload pipeline (devops-agent), vision recognition adapter (integration-agent), POST /meals/analyze (backend-agent), analysis results screen (frontend-agent). US-009 (3 pts, frontend-agent): alternative dish matches returned by the analysis endpoint (backend-agent), approximate-estimate labelling (frontend-agent), alternative dish picker UI (frontend-agent). US-010 (3 pts, frontend-agent): connectivity check before submission, timeout/error handling (frontend-agent), analysis-failure logging on the backend (backend-agent).

**Related:** US-006, US-007, US-008, US-009, US-010

- ⚠ No implementation status reported for any task in this epic.

### DEV-EPIC-003 · approved · source: plan:EPIC-003

Planned backlog for the estimate review/correction screen and meal save with accuracy-feedback capture.

US-011 (5 pts, frontend-agent): swap-from-alternatives flow, search-from-item flow (frontend-agent), tracking original/replacement dish IDs (backend-agent). US-012 (5 pts, frontend-agent): portion selector component, real-time recalculation, portion input validation (all frontend-agent). US-013 (3 pts, frontend-agent): add-item and remove-item actions, preventing an empty-meal save (frontend-agent). US-014 (5 pts, backend-agent): meals/meal_items tables and migration, POST /meals (backend-agent), save-meal screen with slot/date selection (frontend-agent), persisting/displaying the photo with the saved meal (backend-agent). US-015 (1 pt, frontend-agent): discard action, unsaved-changes confirmation (frontend-agent). US-016 (5 pts, backend-agent): storing the original estimate alongside the confirmed meal, tracking accepted-vs-corrected state, correction-data query capability (all backend-agent).

**Related:** US-011, US-012, US-013, US-014, US-015, US-016

- ⚠ No implementation status reported for any task in this epic.

### DEV-EPIC-004 · approved · source: plan:EPIC-004

Planned backlog for catalogue search, manual entry and editing of logged items.

US-017 (5 pts, backend-agent): GET /catalogue/search (backend-agent), mobile search screen, portion-selection/add-to-meal flow, empty-result handling (frontend-agent). US-018 (3 pts, backend-agent): POST /foods/manual (backend-agent), manual entry form (frontend-agent), inclusion of the user's manual foods in search results (backend-agent). US-019 (3 pts, frontend-agent): PUT /meals/{id} (backend-agent), edit-meal screen, single-item deletion from a meal (frontend-agent).

**Related:** US-017, US-018, US-019

- ⚠ No implementation status reported for any task in this epic.

### DEV-EPIC-005 · approved · source: plan:EPIC-005

Planned backlog for the home screen, meal grouping, history browsing, and meal/photo deletion.

US-020 (5 pts, frontend-agent): GET /home (backend-agent), home screen calorie display, macro breakdown display, empty-day state (frontend-agent). US-021 (3 pts, frontend-agent): GET /home enhanced to group by slot (backend-agent), meal group sections, tap-through to entry detail (frontend-agent). US-022 (5 pts, frontend-agent): GET /meals date filtering (backend-agent), history date navigation screen, empty-day/add-to-past-date handling (frontend-agent). US-023 (3 pts, backend-agent): DELETE /meals/{id} (backend-agent), delete confirmation UI (frontend-agent), S3 photo deletion verification (devops-agent).

**Related:** US-020, US-021, US-022, US-023

- ⚠ No implementation status reported for any task in this epic.

### DEV-EPIC-006 · approved · source: plan:EPIC-006

Planned backlog for the body weight log.

US-024 (5 pts, frontend-agent): weight_entries table/migration, POST /weights (backend-agent), weight entry form, profile-weight-update offer on save (frontend-agent). US-025 (3 pts, frontend-agent): GET /weights (backend-agent), weight log list screen, edit/delete for weight entries (frontend-agent).

**Related:** US-024, US-025

- ⚠ No implementation status reported for any task in this epic.

### DEV-EPIC-007 · approved · source: plan:EPIC-007

Planned backlog for building and curating the nutrition catalogue and Indian food coverage.

US-026 (8 pts, backend-agent): foods/food_aliases schema design, IFCT import pipeline, USDA/Open Food Facts import pipeline, curation of the launch Indian dish catalogue (all backend-agent). US-027 (3 pts, backend-agent): portion_units table/migration, household unit mapping curation, exposing portion units via the catalogue API (all backend-agent). US-028 (3 pts, backend-agent): source-tracking fields on foods table, ensuring corrections are prospective-only (backend-agent), in-app source attribution display (frontend-agent).

**Related:** US-026, US-027, US-028

- ⚠ No implementation status reported for any task in this epic.
- ⚠ No record confirming the licence review mentioned in AC-092 was actually carried out as part of this backlog work.

### DEV-EPIC-008 · approved · source: plan:EPIC-008

Planned backlog for beta release conditions: free access, English-only, privacy/data scoping, and wellness disclaimers.

US-029 (2 pts, qa-agent): audit of all screens for feature gating (qa-agent), verification of no billing integration in the build (devops-agent). US-030 (2 pts, qa-agent): cross-platform feature-parity verification (qa-agent), forcing English locale regardless of device language (frontend-agent), basic load verification for 1,000 users (devops-agent). US-031 (5 pts, security-agent): per-user S3 access policies, per-user data scoping across all API endpoints, photo-deletion-from-storage verification (all security-agent), first-use camera privacy notice (frontend-agent). US-032 (2 pts, frontend-agent): wellness disclaimer at target display, audit of all screens for clinical language (qa-agent), making the disclaimer accessible from profile/settings (frontend-agent).

**Related:** US-029, US-030, US-031, US-032

- ⚠ No implementation status reported for any task in this epic.
- ⚠ No record of the qa-agent audits (feature-gating, clinical-language) actually being run or their results.
<!-- sdlc:auto:end narrative -->
