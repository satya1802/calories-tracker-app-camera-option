# Traceability Matrix

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start legend -->
Built from recorded links, not written by a model: requirement key → plan item (`source_stable_key`) → development ticket (`stable_key`) → the ticket's test steps → the last live deployment that started after the work finished. **AC tests** counts the story's acceptance criteria that have a test case, and those whose test cases all passed in the latest finished E2E run.
<!-- sdlc:auto:end legend -->

<!-- sdlc:auto:start matrix -->
| Requirement | Epic | Title | Plan items | Sprint | Design | Code | Commits | Ticket | Tests | AC tests | Deployed |
|---|---|---|---|---|---|---|---|---|---|---|---|
| US-001 | EPIC-001 | Create an account with email and password | US-001, US-001-T1, US-001-T2, US-001-T3, US-001-T4 | 1 | POST /auth/login, POST /auth/signup, api, db, mobile_app, users | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-002 | EPIC-001 | Sign in with Google or Apple | US-002, US-002-T1, US-002-T2, US-002-T3, US-002-T4 | 1 | POST /auth/oauth, api, mobile_app, users | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-003 | EPIC-001 | Capture my profile during onboarding | US-003, US-003-T1, US-003-T2, US-003-T3, US-003-T4 | 1 | POST /profile, api, db, mobile_app, user_profiles | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-004 | EPIC-001 | Get a derived daily calorie and macro target | US-004, US-004-T1, US-004-T2, US-004-T3 | 1 | POST /profile, api, db, mobile_app, user_profiles, user_targets | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-005 | EPIC-001 | View and update my profile and targets | US-005, US-005-T1, US-005-T2, US-005-T3 | 2 | GET /profile, PUT /profile, api, mobile_app, user_profiles, user_targets | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-006 | EPIC-002 | Photograph a meal with the camera | US-006, US-006-T1, US-006-T2, US-006-T3 | 2 | mobile_app | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-007 | EPIC-002 | Choose an existing photo from the gallery | US-007, US-007-T1, US-007-T2 | 2 | mobile_app | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-008 | EPIC-002 | Get a dish list with calories and macros from the photo | US-008, US-008-T1, US-008-T2, US-008-T3, US-008-T4 | 3 | POST /meals/analyze, api, db, foods, mobile_app, photo_estimates, photo_store, vision_integration | — | — | not started | not run | 0/5 tested · 0/5 passing | — |
| US-009 | EPIC-002 | See estimates as approximate with alternative dishes | US-009, US-009-T1, US-009-T2, US-009-T3 | 4 | POST /meals/analyze, api, foods, mobile_app | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-010 | EPIC-002 | Handle loss of connectivity or analysis failure | US-010, US-010-T1, US-010-T2, US-010-T3 | 4 | POST /meals/analyze, api, mobile_app, vision_integration | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-011 | EPIC-003 | Swap a detected dish for a different one | US-011, US-011-T1, US-011-T2, US-011-T3 | 4 | GET /catalogue/search, api, catalogue_service, foods, meal_items, mobile_app | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-012 | EPIC-003 | Adjust the portion of an item | US-012, US-012-T1, US-012-T2, US-012-T3 | 4 | catalogue_service, foods, mobile_app, portion_units | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-013 | EPIC-003 | Add or remove items in the estimate | US-013, US-013-T1, US-013-T2, US-013-T3 | 5 | meal_items, mobile_app | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-014 | EPIC-003 | Save the confirmed meal into today's log | US-014, US-014-T1, US-014-T2, US-014-T3, US-014-T4 | 5 | POST /meals, api, db, meal_items, meals, mobile_app, photo_estimates, photo_store | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-015 | EPIC-003 | Discard an estimate without logging it | US-015, US-015-T1, US-015-T2 | 5 | mobile_app | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-016 | EPIC-003 | Capture corrections as accuracy feedback | US-016, US-016-T1, US-016-T2, US-016-T3 | 5 | POST /meals, api, db, meal_items, meals, photo_estimates | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-017 | EPIC-004 | Search the food catalogue and add a food | US-017, US-017-T1, US-017-T2, US-017-T3, US-017-T4 | 3 | GET /catalogue/search, api, catalogue_service, food_aliases, foods, mobile_app, portion_units | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-018 | EPIC-004 | Enter a food manually | US-018, US-018-T1, US-018-T2, US-018-T3 | 4 | POST /foods/manual, api, catalogue_service, db, foods, mobile_app | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-019 | EPIC-004 | Edit any previously logged item | US-019, US-019-T1, US-019-T2, US-019-T3 | 6 | PUT /meals/{id}, api, meal_items, meals, mobile_app, photo_estimates | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-020 | EPIC-005 | See today's intake against my calorie and macro targets | US-020, US-020-T1, US-020-T2, US-020-T3, US-020-T4 | 6 | GET /home, api, meal_items, meals, mobile_app, user_targets | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-021 | EPIC-005 | See today's meals grouped by breakfast, lunch, dinner and snacks | US-021, US-021-T1, US-021-T2, US-021-T3 | 6 | GET /home, api, meal_items, meals, mobile_app | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-022 | EPIC-005 | Browse my meal history by day | US-022, US-022-T1, US-022-T2, US-022-T3 | 6 | GET /meals, api, meal_items, meals, mobile_app, user_targets | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-023 | EPIC-005 | Delete a logged meal and its photo | US-023, US-023-T1, US-023-T2, US-023-T3 | 6 | DELETE /meals/{id}, api, meals, mobile_app, photo_store | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-024 | EPIC-006 | Record my body weight | US-024, US-024-T1, US-024-T2, US-024-T3, US-024-T4 | 7 | POST /weights, api, db, mobile_app, user_profiles, user_targets, weight_entries | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-025 | EPIC-006 | View my weight entries over time | US-025, US-025-T1, US-025-T2, US-025-T3 | 7 | GET /weights, api, mobile_app, weight_entries | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-026 | EPIC-007 | Find Indian home and restaurant dishes in the catalogue | US-026, US-026-T1, US-026-T2, US-026-T3, US-026-T4 | 2 | catalogue_service, db, food_aliases, foods | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-027 | EPIC-007 | Use Indian household portion units | US-027, US-027-T1, US-027-T2, US-027-T3 | 3 | catalogue_service, db, foods, portion_units | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-028 | EPIC-007 | Trace nutrition values to their source | US-028, US-028-T1, US-028-T2, US-028-T3 | 5 | catalogue_service, db, foods, mobile_app | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-029 | EPIC-008 | Use every feature free during the beta | US-029, US-029-T1, US-029-T2 | 7 | mobile_app | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-030 | EPIC-008 | Use the app in English on iOS and Android | US-030, US-030-T1, US-030-T2, US-030-T3 | 7 | api, mobile_app | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-031 | EPIC-008 | Keep my meal photos and log data under my control | US-031, US-031-T1, US-031-T2, US-031-T3, US-031-T4 | 7 | api, db, meals, mobile_app, photo_store | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-032 | EPIC-008 | Understand that the app is a wellness tool, not medical advice | US-032, US-032-T1, US-032-T2, US-032-T3 | 7 | mobile_app | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
<!-- sdlc:auto:end matrix -->
