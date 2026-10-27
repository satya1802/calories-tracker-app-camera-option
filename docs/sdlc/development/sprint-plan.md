# Sprint Plan

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start sprints -->
## Sprint 1: Sprint 1

Account creation, onboarding profile capture and daily target derivation

Capacity: 20 points · Committed: 18

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-001 | Story | Create an account with email and password | 5 | backend-agent | — |
| ↳ US-001-T1 | Task | Create users table and auth schema | — | backend-agent | — |
| ↳ US-001-T2 | Task | Implement POST /auth/signup endpoint | — | backend-agent | — |
| ↳ US-001-T3 | Task | Implement POST /auth/login endpoint | — | backend-agent | — |
| ↳ US-001-T4 | Task | Build mobile sign-up and sign-in screens | — | frontend-agent | — |
| US-002 | Story | Sign in with Google or Apple | 5 | integration-agent | US-001 |
| ↳ US-002-T1 | Task | Implement POST /auth/oauth backend endpoint | — | integration-agent | — |
| ↳ US-002-T2 | Task | Integrate Google Sign-In SDK in mobile app | — | integration-agent | — |
| ↳ US-002-T3 | Task | Integrate Apple Sign-In on iOS | — | integration-agent | — |
| ↳ US-002-T4 | Task | Platform-conditional sign-in UI | — | frontend-agent | — |
| US-003 | Story | Capture my profile during onboarding | 5 | frontend-agent | US-001 |
| ↳ US-003-T1 | Task | Create user_profiles table and migration | — | backend-agent | — |
| ↳ US-003-T2 | Task | Implement POST /profile endpoint | — | backend-agent | — |
| ↳ US-003-T3 | Task | Build onboarding wizard screens | — | frontend-agent | — |
| ↳ US-003-T4 | Task | Post-onboarding navigation logic | — | frontend-agent | — |
| US-004 | Story | Get a derived daily calorie and macro target | 3 | backend-agent | US-003 |
| ↳ US-004-T1 | Task | Create user_targets table and migration | — | backend-agent | — |
| ↳ US-004-T2 | Task | Implement configurable target calculation | — | backend-agent | — |
| ↳ US-004-T3 | Task | Display targets with wellness disclaimer on mobile | — | frontend-agent | — |

## Sprint 2: Sprint 2

Indian food catalogue, profile editing, camera and gallery photo capture

Capacity: 20 points · Committed: 19

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-005 | Story | View and update my profile and targets | 3 | frontend-agent | US-003, US-004 |
| ↳ US-005-T1 | Task | Implement GET /profile and PUT /profile endpoints | — | backend-agent | — |
| ↳ US-005-T2 | Task | Build profile view and edit screen | — | frontend-agent | — |
| ↳ US-005-T3 | Task | Implement sign-out flow | — | frontend-agent | — |
| US-006 | Story | Photograph a meal with the camera | 5 | frontend-agent | US-001 |
| ↳ US-006-T1 | Task | Set up Expo Camera module and permissions | — | frontend-agent | — |
| ↳ US-006-T2 | Task | Build camera capture screen | — | frontend-agent | — |
| ↳ US-006-T3 | Task | Wire capture output to analysis flow | — | frontend-agent | — |
| US-007 | Story | Choose an existing photo from the gallery | 3 | frontend-agent | US-006 |
| ↳ US-007-T1 | Task | Integrate Expo Image Picker for gallery | — | frontend-agent | — |
| ↳ US-007-T2 | Task | Reuse capture preview for gallery images | — | frontend-agent | — |
| US-026 | Story | Find Indian home and restaurant dishes in the catalogue | 8 | backend-agent | — |
| ↳ US-026-T1 | Task | Design foods and food_aliases schema | — | backend-agent | — |
| ↳ US-026-T2 | Task | Build import pipeline for IFCT data | — | backend-agent | — |
| ↳ US-026-T3 | Task | Build import pipeline for USDA and Open Food Facts | — | backend-agent | — |
| ↳ US-026-T4 | Task | Curate launch Indian dish catalogue | — | backend-agent | — |

## Sprint 3: Sprint 3

AI dish recognition from photos, household portion units and catalogue search

Capacity: 20 points · Committed: 16

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-008 | Story | Get a dish list with calories and macros from the photo | 8 | integration-agent | US-006, US-026 |
| ↳ US-008-T1 | Task | Set up S3 photo upload pipeline | — | devops-agent | — |
| ↳ US-008-T2 | Task | Implement vision recognition adapter | — | integration-agent | — |
| ↳ US-008-T3 | Task | Implement POST /meals/analyze endpoint | — | backend-agent | — |
| ↳ US-008-T4 | Task | Build analysis results screen on mobile | — | frontend-agent | — |
| US-017 | Story | Search the food catalogue and add a food | 5 | backend-agent | US-026 |
| ↳ US-017-T1 | Task | Implement GET /catalogue/search endpoint | — | backend-agent | — |
| ↳ US-017-T2 | Task | Build mobile search screen | — | frontend-agent | — |
| ↳ US-017-T3 | Task | Add portion selection and add-to-meal flow | — | frontend-agent | — |
| ↳ US-017-T4 | Task | Handle empty search results | — | frontend-agent | — |
| US-027 | Story | Use Indian household portion units | 3 | backend-agent | US-026 |
| ↳ US-027-T1 | Task | Create portion_units table and migration | — | backend-agent | — |
| ↳ US-027-T2 | Task | Curate household unit mappings for launch catalogue | — | backend-agent | — |
| ↳ US-027-T3 | Task | Expose portion units via catalogue API | — | backend-agent | — |

## Sprint 4: Sprint 4

Estimate review screen: approximate labelling, alternatives, error handling, dish swap, portion adjust, manual entry

Capacity: 20 points · Committed: 19

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-009 | Story | See estimates as approximate with alternative dishes | 3 | frontend-agent | US-008 |
| ↳ US-009-T1 | Task | Return alternative dish matches from analysis endpoint | — | backend-agent | — |
| ↳ US-009-T2 | Task | Add approximate-estimate labelling to results screen | — | frontend-agent | — |
| ↳ US-009-T3 | Task | Build alternative dish picker UI | — | frontend-agent | — |
| US-010 | Story | Handle loss of connectivity or analysis failure | 3 | frontend-agent | US-008 |
| ↳ US-010-T1 | Task | Add connectivity check before photo submission | — | frontend-agent | — |
| ↳ US-010-T2 | Task | Handle analysis timeout and service errors | — | frontend-agent | — |
| ↳ US-010-T3 | Task | Record analysis failures in backend logs | — | backend-agent | — |
| US-011 | Story | Swap a detected dish for a different one | 5 | frontend-agent | US-008, US-026 |
| ↳ US-011-T1 | Task | Implement swap from alternatives list | — | frontend-agent | — |
| ↳ US-011-T2 | Task | Add search-from-item flow for swap | — | frontend-agent | — |
| ↳ US-011-T3 | Task | Track original and replacement dish IDs | — | backend-agent | — |
| US-012 | Story | Adjust the portion of an item | 5 | frontend-agent | US-008, US-027 |
| ↳ US-012-T1 | Task | Build portion selector component | — | frontend-agent | — |
| ↳ US-012-T2 | Task | Implement real-time recalculation on portion change | — | frontend-agent | — |
| ↳ US-012-T3 | Task | Validate portion input | — | frontend-agent | — |
| US-018 | Story | Enter a food manually | 3 | backend-agent | US-001 |
| ↳ US-018-T1 | Task | Implement POST /foods/manual endpoint | — | backend-agent | — |
| ↳ US-018-T2 | Task | Build manual entry form on mobile | — | frontend-agent | — |
| ↳ US-018-T3 | Task | Include user's manual foods in search results | — | backend-agent | — |

## Sprint 5: Sprint 5

Meal saving, item add/remove, discard, correction feedback capture and catalogue source traceability

Capacity: 20 points · Committed: 17

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-013 | Story | Add or remove items in the estimate | 3 | frontend-agent | US-008, US-017 |
| ↳ US-013-T1 | Task | Implement add-item action on estimate screen | — | frontend-agent | — |
| ↳ US-013-T2 | Task | Implement remove-item action on estimate screen | — | frontend-agent | — |
| ↳ US-013-T3 | Task | Prevent saving an empty meal | — | frontend-agent | — |
| US-014 | Story | Save the confirmed meal into today's log | 5 | backend-agent | US-008, US-011, US-012 |
| ↳ US-014-T1 | Task | Create meals and meal_items tables and migration | — | backend-agent | — |
| ↳ US-014-T2 | Task | Implement POST /meals endpoint | — | backend-agent | — |
| ↳ US-014-T3 | Task | Build save-meal screen with slot and date selection | — | frontend-agent | — |
| ↳ US-014-T4 | Task | Persist and display photo with saved meal | — | backend-agent | — |
| US-015 | Story | Discard an estimate without logging it | 1 | frontend-agent | US-008 |
| ↳ US-015-T1 | Task | Implement discard action on estimate screen | — | frontend-agent | — |
| ↳ US-015-T2 | Task | Add unsaved-changes confirmation | — | frontend-agent | — |
| US-016 | Story | Capture corrections as accuracy feedback | 5 | backend-agent | US-014, US-011 |
| ↳ US-016-T1 | Task | Store original estimate alongside confirmed meal | — | backend-agent | — |
| ↳ US-016-T2 | Task | Track accepted-vs-corrected state | — | backend-agent | — |
| ↳ US-016-T3 | Task | Create correction-data query capability | — | backend-agent | — |
| US-028 | Story | Trace nutrition values to their source | 3 | backend-agent | US-026 |
| ↳ US-028-T1 | Task | Add source tracking fields to foods table | — | backend-agent | — |
| ↳ US-028-T2 | Task | Ensure corrections are prospective only | — | backend-agent | — |
| ↳ US-028-T3 | Task | Display source attribution in-app | — | frontend-agent | — |

## Sprint 6: Sprint 6

Home screen with intake vs targets, meal grouping, history browsing, editing and deletion

Capacity: 20 points · Committed: 19

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-019 | Story | Edit any previously logged item | 3 | frontend-agent | US-014 |
| ↳ US-019-T1 | Task | Implement PUT /meals/{id} endpoint | — | backend-agent | — |
| ↳ US-019-T2 | Task | Build edit-meal screen | — | frontend-agent | — |
| ↳ US-019-T3 | Task | Allow single-item deletion from meal | — | frontend-agent | — |
| US-020 | Story | See today's intake against my calorie and macro targets | 5 | frontend-agent | US-004, US-014 |
| ↳ US-020-T1 | Task | Implement GET /home endpoint | — | backend-agent | — |
| ↳ US-020-T2 | Task | Build home screen calorie display | — | frontend-agent | — |
| ↳ US-020-T3 | Task | Add macro breakdown display | — | frontend-agent | — |
| ↳ US-020-T4 | Task | Handle empty-day state | — | frontend-agent | — |
| US-021 | Story | See today's meals grouped by breakfast, lunch, dinner and snacks | 3 | frontend-agent | US-014 |
| ↳ US-021-T1 | Task | Enhance GET /home to return meals grouped by slot | — | backend-agent | — |
| ↳ US-021-T2 | Task | Build meal group sections on home screen | — | frontend-agent | — |
| ↳ US-021-T3 | Task | Implement tap-through to entry detail | — | frontend-agent | — |
| US-022 | Story | Browse my meal history by day | 5 | frontend-agent | US-014 |
| ↳ US-022-T1 | Task | Enhance GET /meals to support date filtering | — | backend-agent | — |
| ↳ US-022-T2 | Task | Build history date navigation screen | — | frontend-agent | — |
| ↳ US-022-T3 | Task | Handle empty-day and add-to-past-date | — | frontend-agent | — |
| US-023 | Story | Delete a logged meal and its photo | 3 | backend-agent | US-014 |
| ↳ US-023-T1 | Task | Implement DELETE /meals/{id} endpoint | — | backend-agent | — |
| ↳ US-023-T2 | Task | Build delete confirmation UI | — | frontend-agent | — |
| ↳ US-023-T3 | Task | Verify S3 photo deletion | — | devops-agent | — |

## Sprint 7: Sprint 7

Weight log, beta release conditions: free access, English-only, privacy controls and wellness disclaimers

Capacity: 20 points · Committed: 19

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-024 | Story | Record my body weight | 5 | frontend-agent | US-001, US-003 |
| ↳ US-024-T1 | Task | Create weight_entries table and migration | — | backend-agent | — |
| ↳ US-024-T2 | Task | Implement POST /weights endpoint | — | backend-agent | — |
| ↳ US-024-T3 | Task | Build weight entry form on mobile | — | frontend-agent | — |
| ↳ US-024-T4 | Task | Offer profile weight update on save | — | frontend-agent | — |
| US-025 | Story | View my weight entries over time | 3 | frontend-agent | US-024 |
| ↳ US-025-T1 | Task | Implement GET /weights endpoint | — | backend-agent | — |
| ↳ US-025-T2 | Task | Build weight log list screen | — | frontend-agent | — |
| ↳ US-025-T3 | Task | Add edit and delete for weight entries | — | frontend-agent | — |
| US-029 | Story | Use every feature free during the beta | 2 | qa-agent | US-008, US-017, US-020 |
| ↳ US-029-T1 | Task | Audit all screens for feature gating | — | qa-agent | — |
| ↳ US-029-T2 | Task | Verify no billing integration in build | — | devops-agent | — |
| US-030 | Story | Use the app in English on iOS and Android | 2 | qa-agent | US-001 |
| ↳ US-030-T1 | Task | Verify cross-platform feature parity | — | qa-agent | — |
| ↳ US-030-T2 | Task | Force English locale regardless of device language | — | frontend-agent | — |
| ↳ US-030-T3 | Task | Basic load verification for 1,000 users | — | devops-agent | — |
| US-031 | Story | Keep my meal photos and log data under my control | 5 | security-agent | US-014, US-023 |
| ↳ US-031-T1 | Task | Configure S3 access policies per user | — | security-agent | — |
| ↳ US-031-T2 | Task | Enforce per-user data scoping in all API endpoints | — | security-agent | — |
| ↳ US-031-T3 | Task | Verify photo deletion from storage | — | security-agent | — |
| ↳ US-031-T4 | Task | Add first-use camera privacy notice | — | frontend-agent | — |
| US-032 | Story | Understand that the app is a wellness tool, not medical advice | 2 | frontend-agent | US-004 |
| ↳ US-032-T1 | Task | Add wellness disclaimer at target display | — | frontend-agent | — |
| ↳ US-032-T2 | Task | Audit all screens for clinical language | — | qa-agent | — |
| ↳ US-032-T3 | Task | Make disclaimer accessible from profile/settings | — | frontend-agent | — |

## Unscheduled

_Nothing unscheduled._
<!-- sdlc:auto:end sprints -->
