# Product Requirements

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
## Summary

### REQ-000 · approved · source: requirements

Product-owner-approved technology stack and lightweight delivery scope for a camera-first Indian calorie tracker beta targeting ~1,000 free, English-only users.

Delivery scope: lightweight; requirements version 1. Approved stack (not to be substituted): Backend FastAPI, Cloud AWS (ap-south-1 Mumbai), Database PostgreSQL, Frontend React Native with Expo (iOS + Android). Rationale given: FastAPI's async handling suits slow vision-model calls and cheap correction-logging writes; AWS Mumbai gives India data residency, upload speed, and one account covering compute/DB/storage; PostgreSQL handles structured relational data (users, targets, meals, items, catalogue, weights) plus full-text catalogue search; React Native/Expo gives one codebase for iOS+Android with camera, gallery and reminder primitives inside a three-month beta window. In-scope capabilities: camera/gallery meal capture, AI dish identification + calorie estimate, editable estimate (swap dish/change portion/add-remove items), save to daily log, home screen intake-vs-target, onboarding profile, derived daily calorie/macro targets, catalogue search + manual entry/edit, meal grouping (breakfast/lunch/dinner/snacks), body weight log, individual accounts, meal history by day, meal+photo deletion, hosted (non-custom-trained) AI vision recognition, approximate estimates with alternatives, no agreed numeric accuracy target, nutrition sourced from IFCT/USDA FoodData Central/Open Food Facts, Indian household portions (katori, roti, idli, etc.), Indian-first/global-best-effort food coverage, user-deletable meal photos, internet required for photo analysis, English-only UI, free beta with no in-app payments.

### EPIC-001 · approved · source: requirements:EPIC-001

Individual accounts (email/password or Google/Apple) with an onboarding flow that captures a profile and derives a configurable daily calorie/macro target, framed as a general wellness estimate.

US-001 (critical): email/password sign-up creates account + signs in + enters onboarding; duplicate email rejected with sign-in offered, no duplicate created; invalid email/password shows field-level errors; returning sign-in restores the user's own profile, targets and log (AC-001..AC-004). US-002 (high): Continue with Google/Apple creates or matches an account and routes new users into onboarding; a cancelled/failed provider flow leaves the user signed out with no account created and a message shown; Apple sign-in is omitted on Android where unsupported (AC-005..AC-007). US-003 (critical): onboarding collects height, current weight, age, activity level and goal (lose/maintain/gain) before the home screen is reached; out-of-range or blank required fields block progress with an explanation; confirming saves the profile and lands on the home screen with targets in place; onboarding is not repeated on a later sign-in on the same or another device (AC-008..AC-011). US-004 (critical): completed onboarding produces and displays a stored daily calorie target and separate protein/carb/fat targets in grams, shown with an explicit 'general wellness estimate, not medical advice' statement; because the calculation formula/activity multipliers were not agreed with the business, they must be implemented as documented and configurable without requiring an app release (AC-012..AC-014). US-005 (high): the profile screen shows current height/weight/age/activity/goal plus current targets; saving a changed value recalculates targets and the home screen compares today's intake against the new targets immediately, without rewriting previously logged days; signing out returns to the sign-in screen and revokes on-device access until re-authentication (AC-015..AC-018).

**Related:** US-001, US-002, US-003, US-004, US-005

- ⚠ Calorie/macro target calculation formula and activity multipliers are explicitly described as proposed but not agreed with the business (AC-014) -- needs confirmation before target accuracy can be relied on.

### EPIC-002 · approved · source: requirements:EPIC-002

Camera-first meal capture (camera or gallery) analysed by a hosted multimodal vision model into a dish list with approximate calories/macros, Indian-first, with defined handling for low confidence, no-food, offline and service-failure cases.

US-006 (critical): the primary capture action opens the camera in one step with no intermediate menu; OS camera-permission prompt is shown on first use, with a fallback to gallery/search if declined; a captured photo offers retake or submit (AC-019..AC-021). US-007 (high): a gallery option lets the user pick an existing image, shown with the same retake/submit options; photo-library permission is requested, with an explanation and return to capture screen if declined (AC-022..AC-023). US-008 (critical): submitting a photo while online returns one or more detected dishes, each with assumed portion, estimated calories/protein/carb/fat and a meal total; a progress indicator is shown with a cancel option that discards nothing unsaved; common Indian meals (thali, curry+roti, idli-sambar) are returned as Indian dish names with household portions, not generic ingredients; unconfident or non-Indian foods return a clearly-marked low-confidence best guess or an empty result prompting search/manual entry, never blocking logging; a photo with no recognisable food tells the user so and offers retake/search/manual (AC-024..AC-028). US-009 (critical): displayed estimates explicitly state they are approximate and may need correction; each detected dish shows alternative catalogue matches with their own calories, selectable instead; because no numeric accuracy target has been agreed, no accuracy percentage or margin of error is ever shown (AC-029..AC-031). US-010 (high): submitting with no connection tells the user analysis needs connectivity, keeps the photo, and offers retry or search/manual logging; a service error or timeout shows a non-technical message with retry, and the failure is recorded in backend logs; retrying while connected resubmits the same photo without re-capture (AC-032..AC-034).

**Related:** US-006, US-007, US-008, US-009, US-010

- ⚠ No numeric accuracy target (e.g. +/-15%) has been agreed for calorie estimates -- explicitly a deferred product decision per AC-031, not a defect, but still open.

### EPIC-003 · approved · source: requirements:EPIC-003

The editable estimate screen lets the user correct dish, portion and item list before saving; both the AI's original guess and the user's final version are persisted to measure recognition accuracy in the field.

US-011 (critical): a wrong dish can be swapped from the suggested alternatives or via catalogue search; both the original detected dish and the chosen replacement are recorded on save for accuracy analysis (AC-035..AC-037). US-012 (critical): quantity/portion unit changes recalculate item and meal totals immediately; Indian household units (katori, roti, idli, piece, glass) are offered alongside grams/millilitres for relevant dishes; zero or non-numeric quantities are rejected, keeping the previous portion (AC-038..AC-040). US-013 (critical): missing items can be added from the catalogue with a portion, wrong items can be removed, with totals updating each time; removing every item blocks save and prompts to add an item or discard (AC-041..AC-043). US-014 (critical): saving requires confirming a meal slot (breakfast/lunch/dinner/snacks) and date, pre-selected by time of day but overridable; the meal, its items, portions, calories/macros and photo are written to the log; the home screen reflects the new entry without a manual refresh (AC-044..AC-047). US-015 (medium): discarding removes the estimate with no log entry and no retained photo; attempting to leave after edits without saving prompts a discard confirmation (AC-048..AC-049). US-016 (high): on save, the backend stores the original AI-estimated items/portions/total alongside the user-confirmed items/portions/total; an unedited photo-derived meal is flagged 'accepted without correction' so acceptance and correction rates can be distinguished; the stored correction data is queryable for per-dish correction rate and calorie delta without needing a dedicated in-app analytics screen (AC-050..AC-052).

**Related:** US-011, US-012, US-013, US-014, US-015, US-016

### EPIC-004 · approved · source: requirements:EPIC-004

Non-photo logging paths -- catalogue search and manual food entry -- plus the ability to edit anything already in the log, including items that originated from a photo.

US-017 (critical): typing 2+ characters lists matching catalogue foods (name + default-portion calories), updating live; Indian dish names (e.g. dal tadka, masala dosa, paneer butter masala) return matching entries; selecting a result with a quantity/portion adds it to the current estimate or directly to a chosen meal slot; an empty result offers the manual-entry path (AC-053..AC-056). US-018 (high): manual entry requires a name, portion description and calorie value, with optional macros; missing name or calories blocks save with an indication of what's missing; previously entered manual foods are offered again on later search and stay private to the creating account (AC-057..AC-059). US-019 (high): opening any logged meal (today or a past day) allows changing an item's food, quantity, portion unit or meal slot, or removing a single item, with the day's totals recalculated; editing a photo-derived meal keeps the attached photo and leaves the original AI estimate record intact for accuracy analysis (AC-060..AC-062).

**Related:** US-017, US-018, US-019

### EPIC-005 · approved · source: requirements:EPIC-005

Home screen shows today's intake grouped by meal slot against calorie/macro targets; users can browse history day-by-day and delete a logged meal along with its photo.

US-020 (critical): the home screen shows today's total calories consumed, the calorie target, and the remaining/exceeded amount; protein/carb/fat consumed are each shown in grams against their targets; a day with nothing logged shows zero totals and prompts the first meal; exceeding the target is shown factually with no judgemental or medical framing (AC-063..AC-066). US-021 (high): breakfast, lunch, dinner and snacks are each shown with their items and a calorie subtotal, including empty groups which still offer an add action; tapping a group or entry opens its items, portions, calories, macros and photo if present (AC-067..AC-069). US-022 (high): navigating to a previous date shows that day's meals grouped by slot with totals against the target in force at the time; forward/back navigation updates the view in place; a day with nothing logged shows an empty state that still allows adding an entry; additions/edits on a past day are recorded against that date, not today (AC-070..AC-073). US-023 (high): deleting a logged meal removes it and recalculates the day's totals immediately; if a photo was attached it is deleted from backend storage and no longer served; the delete confirmation states both the meal and its photo will be removed, with a cancel option (AC-074..AC-076).

**Related:** US-020, US-021, US-022, US-023

### EPIC-006 · approved · source: requirements:EPIC-006

Users can log body weight over time (date-stamped) and browse their weight history, with an optional link back into profile/target recalculation.

US-024 (high): entering a weight saves it against today's date by default, with an option to choose a different date; an out-of-range or non-numeric value is rejected with an explanation and nothing is saved; saving a second entry for a date already recorded updates that date's entry instead of duplicating; saving a new current weight offers to update the profile weight and, if accepted, recalculates calorie/macro targets (AC-077..AC-080). US-025 (medium): recorded weights are listed most-recent-first with date and value; having no entries beyond onboarding shows an empty state prompting the first entry; selecting an entry allows editing its value or deleting it, with the list updating on save (AC-081..AC-083).

**Related:** US-024, US-025

### EPIC-007 · approved · source: requirements:EPIC-007

A curated nutrition catalogue built from IFCT, USDA FoodData Central and Open Food Facts covers Indian home/restaurant dishes with household portion units, and tracks source/licence traceability.

US-026 (critical): the launch catalogue covers common Indian home and restaurant dishes (thali components, curries, breads, rice dishes, regional items) each with calories and protein/carb/fat for at least one defined portion; alternate names/spellings of the same dish resolve to one catalogue entry; a global/international food not in the catalogue returns the closest available match or an empty result with manual entry as a fallback, accepted as best-effort for v1 (AC-084..AC-086). US-027 (high): dishes normally served in a household unit offer relevant units (e.g. 1 katori, 1 roti, 1 idli, 1 piece, 1 glass) with gram equivalents in the portion selector; selecting a unit/quantity calculates calories/macros from the stored gram equivalent; foods with no meaningful household unit default to grams or millilitres (AC-087..AC-089). US-028 (medium): each catalogue entry records its source (IFCT, USDA FoodData Central, Open Food Facts, or internally curated) and import date; a later correction to a catalogue value applies only to future logging, leaving past saved calorie values unchanged; required attribution for sourced data must be shown in-app and the licence review recorded before release (AC-090..AC-092).

**Related:** US-026, US-027, US-028

- ⚠ Licence review of IFCT/USDA FoodData Central/Open Food Facts terms and the required in-app attribution (AC-092) is not confirmed as complete in any input provided -- needs sign-off before launch.

### EPIC-008 · approved · source: requirements:EPIC-008

Cross-cutting beta release conditions: fully free with no payments, English-only on both platforms, India-hosted/account-scoped user data, and explicit non-medical wellness positioning.

US-029 (high): no feature is gated and no paywall, upgrade prompt or daily scan limit is shown to any signed-in beta user across photo logging, search, manual entry, log, history and weight log; the submitted App Store/Play Store build contains no in-app purchase or billing integration (AC-093..AC-094). US-030 (high): the same feature set is available on iOS and Android from one cross-platform codebase; the UI stays in English regardless of device language; the hosted backend is expected to serve the ~1,000-user beta load without degradation, with broader scale work explicitly deferred (AC-095..AC-097). US-031 (critical): uploaded meal photos are stored in the managed India-region cloud backend, retrievable only by the owning authenticated account; every log, photo, weight entry and profile is scoped to its owner and cross-account access is denied; deleting a log entry removes its photo from storage so it is no longer served; first camera use shows a notice that photos are uploaded for analysis, stored with the log, and deletable (AC-098..AC-101). US-032 (medium): derived targets are first shown with a statement that the app is a general wellness tool, not medical or clinical advice; no diagnosis, clinical interpretation or medical recommendation appears anywhere estimates, macros, targets or weight are shown; the disclaimer remains accessible from profile/settings after its first showing (AC-102..AC-104).

**Related:** US-029, US-030, US-031, US-032
<!-- sdlc:auto:end narrative -->

<!-- sdlc:auto:start summary -->
**Requirements version:** v1  
**Delivery scope:** lightweight  
**Approved:** 2026-10-05

**Capabilities in scope:** Meal photo capture from camera or gallery, Dish identification and calorie estimate from the photo, Editable estimate screen: swap dish, change portion, add or remove items, Save a confirmed meal into today's food log, Today's intake versus calorie and macro target on the home screen, Onboarding profile: height, weight, age, activity level and goal, Derived daily calorie and protein/carb/fat targets, Food catalogue search and add with a chosen portion, Manual food entry and editing of any previously logged item, Meals grouped as breakfast, lunch, dinner and snacks, Body weight entries over time, Individual user account and personal profile, Meal history browsing by day, Deleting a logged meal and its photo, Dish recognition by a hosted AI vision service, not a custom-trained model, Estimates always shown as approximate, with alternative dishes to pick from, No agreed accuracy target (e.g. ±15%) for calorie estimates, Nutrition values curated from IFCT, USDA FoodData Central and Open Food Facts, Indian household portions: katori, roti, idli and similar, Indian home and restaurant food first; global foods best-effort, Meal photos kept with the log entry and deletable by the user, Internet connection required to analyse a photo, English-only app at launch, Free during beta, with no in-app payments

**Approved technology stack:**

| Layer | Choice | Rationale |
|---|---|---|
| backend | FastAPI | The heart of your app is a call out to a hosted vision model, then mapping its answer onto your own Indian catalogue with katori and roti portions. That is data work, and Python is where the AI and food-data tooling lives. FastAPI handles the slow part well: a photo waiting several seconds on the model does not block other users. It also keeps your feedback loop cheap — recording what the model guessed versus what the user corrected is just another table write. |
| cloud | AWS | You asked for hosting in an India region, and AWS Mumbai (ap-south-1) gives you that for both the database and the meal photos, which matters for upload speed on Indian mobile networks and for keeping user data in-country. It covers all three things this app needs in one account: managed PostgreSQL, S3 for photos users can delete, and somewhere to run the FastAPI service. At 1,000 beta users the bill is small, and adding freemium scan limits and subscriptions later changes nothing about the hosting. |
| database | PostgreSQL | This matches the assumption already made. Everything you track is structured and related: a user, their goal, meals, items in each meal, portions and weight history, plus the catalogue curated from IFCT, USDA and Open Food Facts. PostgreSQL powers text search for catalogue logging without a separate search service, keeps today's calorie and macro totals correct, and gives you a clean record of every correction — the evidence you need to judge whether photo accuracy is good enough to scale. |
| frontend | React | Your product is camera-first and mobile-only, and React in its mobile form (React Native with Expo) is exactly what your analyst assumed. One codebase gives you both iOS and Android inside the three-month beta window instead of building the same screens twice, and Expo covers camera capture, photo library access and local meal reminders. The photo-review screen — swap the dish, adjust the portion, add items — is ordinary form work in React, which is where most of your build effort will go. |
<!-- sdlc:auto:end summary -->

<!-- sdlc:auto:start epics -->
## EPIC-001: Account, Onboarding Profile and Daily Targets

Individual self-serve accounts and the onboarding profile that derives each user's daily calorie and macronutrient targets.

Assumptions carried from the confirmed understanding:
- Accounts are individual, with email/password plus Google and Apple sign-in. There is no guest/anonymous mode in v1.
- The app is delivered as a cross-platform mobile app (React Native / Expo) for iOS and Android. No web app in v1.
- Backend is a managed cloud service (Postgres plus object storage) hosted in an India region.
- The app is positioned as a general wellness tool, not a medical device, and gives no clinical or medical advice.
- The specific formula used to derive calorie and macro targets (e.g. Mifflin-St Jeor plus an activity multiplier) was not agreed in the conversation and is proposed, not confirmed.

### US-001: Create an account with email and password

**Priority:** critical

> As a new user, I want to create an individual account with my email address and a password, so that my food log and profile are saved to me and available every time I open the app.

| ID | Given | When | Then |
|---|---|---|---|
| AC-001 | I am on the sign-up screen and have entered a valid email address and a password meeting the stated rules | I submit the sign-up form | an account is created for me, I am signed in, and I am taken into onboarding |
| AC-002 | I enter an email address that already has an account | I submit the sign-up form | the app tells me the email is already registered and offers me the sign-in path instead, and no duplicate account is created |
| AC-003 | I enter an invalid email format or a password that fails the stated rules | I submit the sign-up form | the app shows a field-level message explaining what is wrong and does not submit |
| AC-004 | I have an account and have signed out | I sign in with the correct email and password | I am returned to my own profile, targets and food log |

### US-002: Sign in with Google or Apple

**Priority:** high

> As a new or returning user, I want to sign up and sign in using my Google or Apple account, so that I do not have to create and remember another password.

| ID | Given | When | Then |
|---|---|---|---|
| AC-005 | I am on the sign-up or sign-in screen | I choose Continue with Google or Continue with Apple and complete the provider flow successfully | an account is created or matched for me, I am signed in, and new users are taken into onboarding |
| AC-006 | I cancel or fail the Google or Apple provider flow | I am returned to the app | I remain signed out, no account is created, and the app shows a message that sign-in was not completed |
| AC-007 | the app is running on Android where Apple sign-in may not be available | I open the sign-in screen | only the sign-in options supported on that platform are offered |

### US-003: Capture my profile during onboarding

**Priority:** critical

> As a newly registered user, I want to enter my height, weight, age, activity level and goal, so that the app can work out a daily calorie and macro target that fits me.

| ID | Given | When | Then |
|---|---|---|---|
| AC-008 | I have just created an account | onboarding starts | I am asked for height, current weight, age, activity level and my goal (lose, maintain or gain weight) before I reach the home screen |
| AC-009 | I am on an onboarding step | I enter a value outside a sensible range or leave a required field blank | the app blocks me from continuing and explains what is required |
| AC-010 | I have completed every onboarding step | I confirm | my profile is saved to my account and I am taken to the home screen with targets in place |
| AC-011 | I have completed onboarding before | I sign in again on the same or another device | onboarding is not repeated and my saved profile is used |

### US-004: Get a derived daily calorie and macro target

**Priority:** critical

> As a user who has completed onboarding, I want the app to calculate my daily calorie target and protein, carbohydrate and fat targets from my profile, so that I have a concrete number to track my intake against.

| ID | Given | When | Then |
|---|---|---|---|
| AC-012 | I have supplied height, weight, age, activity level and goal | onboarding completes | the app stores and displays a daily calorie target and separate protein, carbohydrate and fat targets in grams |
| AC-013 | my derived targets are shown | I view them | the app states that they are a general wellness estimate and not medical advice |
| AC-014 | the calculation method has not been agreed with the business | targets are produced | the implemented formula and activity multipliers are documented and configurable so they can be changed without an app release |

### US-005: View and update my profile and targets

**Priority:** high

> As a existing user, I want to review and change my profile details, so that my targets stay accurate as my weight, activity or goal changes.

| ID | Given | When | Then |
|---|---|---|---|
| AC-015 | I am signed in | I open my profile | I see my current height, weight, age, activity level, goal and my current calorie and macro targets |
| AC-016 | I am viewing my profile | I change any profile value and save | my targets are recalculated and the home screen immediately compares today's intake against the new targets |
| AC-017 | I have changed my targets today | I view previous days in history | those days still show the intake that was logged, and the app does not retrospectively rewrite past log entries |
| AC-018 | I am signed in | I choose to sign out | I am returned to the sign-in screen and my data is no longer accessible on the device without signing in again |

## EPIC-002: Meal Photo Capture and AI Dish Recognition

The camera-first core: the user photographs a meal and a hosted AI vision service identifies the dishes and estimates calories and macros.

Assumptions carried from the confirmed understanding:
- Recognition uses a hosted multimodal vision model (GPT-4o / Gemini class) prompted to identify dishes and estimate portions and mapped onto the app's nutrition catalogue. It is not a custom-trained model.
- No accuracy target (for example plus or minus 15 percent) has been agreed for calorie estimates. Estimates are presented as approximate. Agreeing a numeric accuracy target later would materially change the recognition approach.
- An internet connection is required to analyse a photo.
- Indian home and restaurant food is the priority; global foods are best-effort at launch.

### US-006: Photograph a meal with the camera

**Priority:** critical

> As a user about to eat, I want to take a photo of my meal from inside the app, so that I can log it without typing anything.

| ID | Given | When | Then |
|---|---|---|---|
| AC-019 | I am signed in and on the home screen | I tap the primary capture action | the camera opens within one step, with no intermediate menu |
| AC-020 | the app has not yet been granted camera permission | I tap the capture action | the operating system permission prompt is shown, and if I decline the app explains that photo logging needs the camera and offers the gallery and search paths instead |
| AC-021 | the camera is open | I take a photo | I see the captured photo with options to retake or to submit it for analysis |

### US-007: Choose an existing photo from the gallery

**Priority:** high

> As a user who already photographed a meal, I want to pick a photo from my device gallery instead of taking a new one, so that I can log a meal after the fact.

| ID | Given | When | Then |
|---|---|---|---|
| AC-022 | I am on the capture screen | I choose the gallery option and select an image | the selected image is shown with the same retake/submit options as a camera capture and can be submitted for analysis |
| AC-023 | the app has not been granted photo library permission | I choose the gallery option | the permission prompt is shown and, if declined, the app explains the limitation and returns me to the capture screen |

### US-008: Get a dish list with calories and macros from the photo

**Priority:** critical

> As a user who has submitted a meal photo, I want the app to identify the dishes in the photo and estimate calories, protein, carbohydrate and fat, so that I can log the meal without looking anything up.

| ID | Given | When | Then |
|---|---|---|---|
| AC-024 | I submit a meal photo while connected to the internet | analysis completes | I am shown a list of one or more detected dishes, each with an assumed portion, estimated calories and estimated protein, carbohydrate and fat, plus a total for the meal |
| AC-025 | analysis is in progress | I am waiting | the app shows a progress indicator and lets me cancel and return without saving anything |
| AC-026 | I photograph a common Indian meal such as a thali, a curry with roti, or idli with sambar | analysis completes | the detected dishes are expressed as Indian dish names from the app catalogue with Indian household portions rather than generic ingredient names |
| AC-027 | the photo contains a food the service cannot confidently identify, including non-Indian foods handled on a best-effort basis | analysis completes | the app returns its best guess clearly marked as low confidence, or returns an empty result with a prompt to add items by search or manually, and never blocks me from logging |
| AC-028 | the photo contains no recognisable food at all | analysis completes | the app tells me no food was detected and offers to retake the photo or log by search or manual entry |

### US-009: See estimates as approximate with alternative dishes

**Priority:** critical

> As a user reviewing a photo result, I want the result to be clearly labelled as an estimate and to offer alternative dish matches, so that I am not misled into trusting a number that may be wrong.

| ID | Given | When | Then |
|---|---|---|---|
| AC-029 | a photo analysis result is displayed | I look at the calorie and macro figures | the screen states explicitly that the values are an approximate estimate from the photo and should be corrected if wrong |
| AC-030 | a detected dish is displayed | I open that dish | I see a short list of alternative catalogue dishes the system considered, each with its own calorie value, that I can select instead |
| AC-031 | no numeric accuracy target has been agreed for the product | estimates are presented anywhere in the app | no accuracy claim, percentage or margin of error is shown to the user |

### US-010: Handle loss of connectivity or analysis failure

**Priority:** high

> As a user with a poor or absent connection, I want clear behaviour when a photo cannot be analysed, so that I do not lose the photo or my ability to log the meal.

| ID | Given | When | Then |
|---|---|---|---|
| AC-032 | I have no internet connection | I submit a photo for analysis | the app tells me that photo analysis needs a connection, keeps the captured photo, and offers to retry or to log the meal by search or manual entry |
| AC-033 | the hosted recognition service returns an error or times out | I am waiting for a result | the app shows a non-technical failure message with a retry action, and the failure is recorded in backend logs for diagnosis |
| AC-034 | an analysis has failed | I tap retry while connected | the same photo is resubmitted without my having to take it again |

## EPIC-003: Review, Correct and Save the Meal

The editable estimate screen, which is both the correction path for the user and the feedback loop for measuring recognition accuracy in the field.

Assumptions carried from the confirmed understanding:
- Every photo result is editable before it is saved; nothing is logged automatically.
- Corrections are the mechanism by which accuracy is measured, since scale work is deferred until photo-estimation accuracy is proven. Capturing the original estimate alongside the corrected version is therefore required.
- Meals are grouped as breakfast, lunch, dinner and snacks.

### US-011: Swap a detected dish for a different one

**Priority:** critical

> As a user whose meal was misidentified, I want to replace a detected dish with the correct one, so that my log reflects what I actually ate.

| ID | Given | When | Then |
|---|---|---|---|
| AC-035 | an estimate lists a dish that is wrong | I open that item and pick one of the suggested alternatives | the item is replaced and its calories and macros, and the meal total, update immediately |
| AC-036 | none of the suggested alternatives is correct | I choose to search the catalogue from the item | I can select any catalogue food and it replaces the detected item |
| AC-037 | I have swapped a dish | I save the meal | the original detected dish and the dish I chose are both recorded against the entry for accuracy analysis |

### US-012: Adjust the portion of an item

**Priority:** critical

> As a user whose portion was estimated wrongly, I want to change the quantity or portion size of any item in the estimate, so that the calorie figure matches what I actually ate.

| ID | Given | When | Then |
|---|---|---|---|
| AC-038 | an item in the estimate has an assumed portion | I change the quantity or select a different portion unit offered for that food | the item's calories and macros and the meal total recalculate immediately and visibly |
| AC-039 | an Indian dish is in the estimate | I open the portion selector | household units relevant to that dish (such as katori, roti, idli, piece, glass) are offered alongside grams or millilitres |
| AC-040 | I enter a quantity of zero or a non-numeric value | I confirm the portion | the app rejects the value with an explanatory message and keeps the previous portion |

### US-013: Add or remove items in the estimate

**Priority:** critical

> As a user whose photo missed or invented a dish, I want to add a missing item or delete an item that is not mine, so that the saved meal is complete and accurate.

| ID | Given | When | Then |
|---|---|---|---|
| AC-041 | the estimate is missing a dish that was on my plate | I use the add-item action and pick a food from the catalogue with a portion | the item is added to the estimate and the meal total updates |
| AC-042 | the estimate contains an item I did not eat | I remove that item | it disappears from the list and the meal total updates |
| AC-043 | I remove every item from the estimate | I attempt to save | the app prevents saving an empty meal and tells me to add at least one item or discard |

### US-014: Save the confirmed meal into today's log

**Priority:** critical

> As a user who has reviewed the estimate, I want to save the meal against a meal slot and date, so that it counts towards my daily intake.

| ID | Given | When | Then |
|---|---|---|---|
| AC-044 | I have a non-empty estimate on screen | I choose to save | I select or confirm breakfast, lunch, dinner or snacks and the date, and the meal is written to my log with its items, portions, calories and macros |
| AC-045 | I save a meal from a photo | the save completes | the photo is stored with the log entry and is visible when I open that entry later |
| AC-046 | I save a meal | I am returned to the home screen | today's totals and the relevant meal group reflect the new entry without my having to refresh |
| AC-047 | the meal slot is not chosen explicitly | the save screen opens | a slot is pre-selected based on the time of day and I can override it |

### US-015: Discard an estimate without logging it

**Priority:** medium

> As a user who photographed something by mistake, I want to abandon the estimate, so that nothing unwanted ends up in my log.

| ID | Given | When | Then |
|---|---|---|---|
| AC-048 | I am on the estimate screen | I choose to discard and confirm | no log entry is created, the photo is not retained against any entry, and I return to the home screen |
| AC-049 | I have made edits to the estimate | I attempt to leave the screen without saving | the app asks me to confirm that I want to discard my changes |

### US-016: Capture corrections as accuracy feedback

**Priority:** high

> As a product owner running the beta, I want every difference between the original AI estimate and the saved meal to be recorded, so that we can measure photo-estimation accuracy in the field before investing in scale.

| ID | Given | When | Then |
|---|---|---|---|
| AC-050 | a meal originating from a photo is saved | the entry is written | the backend stores the original estimated items, portions and calorie total alongside the user-confirmed items, portions and calorie total |
| AC-051 | a photo-derived meal is saved with no edits at all | the entry is written | it is recorded as accepted without correction, so acceptance rate can be distinguished from correction rate |
| AC-052 | correction data has been collected | the product owner needs to review accuracy | the stored data can be queried to report per-dish correction rate and calorie delta, without requiring an in-app analytics screen in this version |

## EPIC-004: Catalogue Search, Manual Entry and Editing

The two non-photo logging paths, and the ability to correct anything already in the log.

Assumptions carried from the confirmed understanding:
- Nutrition values are curated into the app's own catalogue from IFCT Indian food composition tables, USDA FoodData Central and Open Food Facts.
- Users cannot contribute foods to the shared catalogue in v1; a manually entered food is personal to the user who created it.
- Cached catalogue search and manual logging may work offline, but offline support is not a hard requirement for this version.

### US-017: Search the food catalogue and add a food

**Priority:** critical

> As a user logging without a photo, I want to search the catalogue by name and add a food with a chosen portion, so that I can log something quickly or correct a photo result.

| ID | Given | When | Then |
|---|---|---|---|
| AC-053 | I am on the search screen | I type at least two characters | matching catalogue foods are listed with their name and calories for the default portion, updating as I type |
| AC-054 | I search for an Indian dish by its common name (for example dal tadka, masala dosa, paneer butter masala) | results are returned | the matching Indian catalogue entries appear in the results |
| AC-055 | I select a food from the results | I choose a quantity and portion unit and confirm | the item is added with calories and macros calculated for that portion, either to the current estimate or directly to a chosen meal slot |
| AC-056 | my search returns nothing | the empty result is shown | the app offers me the manual entry path instead |

### US-018: Enter a food manually

**Priority:** high

> As a user whose food is not in the catalogue, I want to type in a food name and its calories and macros, so that I can still log it accurately.

| ID | Given | When | Then |
|---|---|---|---|
| AC-057 | I choose manual entry | I provide a name, a portion description and a calorie value, with optional protein, carbohydrate and fat | the item is added to the meal and counts towards my daily totals |
| AC-058 | I omit the name or the calorie value | I try to save the manual entry | the app blocks the save and indicates the missing required fields |
| AC-059 | I have created a manual food before | I search for it later | my own previously entered foods are offered to me so I do not have to retype them, and they remain private to my account |

### US-019: Edit any previously logged item

**Priority:** high

> As a user who logged something wrongly, I want to change the item, portion or meal slot of anything already in my log, so that my history is correct.

| ID | Given | When | Then |
|---|---|---|---|
| AC-060 | I open a logged meal from today or an earlier day | I change an item's food, quantity, portion unit or meal slot and save | the entry and the totals for the day it belongs to are recalculated and shown correctly |
| AC-061 | I open a logged meal | I remove a single item from it | that item is deleted, the remaining items stay, and the day's totals update |
| AC-062 | I edit a meal that originated from a photo | I save the edit | the attached photo remains with the entry and the original AI estimate record is left intact for accuracy analysis |

## EPIC-005: Daily Food Log, Home Screen and History

The daily view of intake against target, grouped by meal, and the ability to browse and clean up past days.

Assumptions carried from the confirmed understanding:
- Meal photos are stored with the log entry in object storage in an India region and are deleted when the user deletes the entry.
- Daily and weekly trend charts described in the confirmed understanding are not part of the Lightweight MVP capability set and are deferred to a later version; this version provides day-by-day browsing of logged meals and weight entries instead.

### US-020: See today's intake against my calorie and macro targets

**Priority:** critical

> As a user tracking a goal, I want the home screen to show what I have eaten today versus my targets, so that I know how much I have left for the day.

| ID | Given | When | Then |
|---|---|---|---|
| AC-063 | I am signed in and open the app | the home screen loads | I see today's total calories consumed, my daily calorie target and the remaining or exceeded amount |
| AC-064 | the home screen is displayed | I look at macros | protein, carbohydrate and fat consumed today are each shown in grams against their respective targets |
| AC-065 | I have logged nothing today | the home screen loads | totals show zero against my targets and the screen prompts me to log my first meal |
| AC-066 | I have exceeded my calorie target | the home screen loads | the overage is shown factually without any judgemental or medical framing |

### US-021: See today's meals grouped by breakfast, lunch, dinner and snacks

**Priority:** high

> As a user reviewing my day, I want my logged items organised into the four meal groups, so that I can see the shape of my day and find an entry quickly.

| ID | Given | When | Then |
|---|---|---|---|
| AC-067 | I have logged items today | I view the home screen | breakfast, lunch, dinner and snacks are each shown with their items and a calorie subtotal |
| AC-068 | a meal group has no entries | I view the home screen | the group is still shown with an add action so I can log into it directly |
| AC-069 | I tap a meal group or an entry within it | the entry opens | I see its items, portions, calories, macros and the meal photo if one exists |

### US-022: Browse my meal history by day

**Priority:** high

> As a returning user, I want to look back at what I logged on previous days, so that I can review my eating over time.

| ID | Given | When | Then |
|---|---|---|---|
| AC-070 | I have logged meals on previous days | I navigate to a previous date | that day's meals, grouped by meal slot, with calorie and macro totals against the target in force are displayed |
| AC-071 | I am viewing a past day | I move forward or back a day | the view updates to the adjacent day without leaving the history screen |
| AC-072 | I select a date on which I logged nothing | the day loads | an empty state is shown for that day and I can still add an entry to it |
| AC-073 | I am viewing a past day | I add or edit an entry there | the entry is recorded against that date, not today |

### US-023: Delete a logged meal and its photo

**Priority:** high

> As a user, I want to delete a meal from my log along with the photo attached to it, so that I can remove mistakes and control what images of my food are stored.

| ID | Given | When | Then |
|---|---|---|---|
| AC-074 | I open a logged meal | I choose delete and confirm | the entry is removed from my log and the day's totals recalculate immediately |
| AC-075 | the deleted meal had a photo attached | the deletion completes | the stored photo is deleted from backend storage and is no longer retrievable in the app |
| AC-076 | I choose delete | the confirmation appears | it states that the meal and its photo will be removed and gives me the option to cancel |

## EPIC-006: Body Weight Log

Recording body weight over time, so the user can see weight alongside the calorie goal it supports.

Assumptions carried from the confirmed understanding:
- Weight trend charts are deferred with the rest of the trends capability; this version records and lists weight entries over time.
- Weight is a user-entered value; wearable and health-platform sync (Apple Health, Google Fit) is explicitly out of scope for v1.

### US-024: Record my body weight

**Priority:** high

> As a user working towards a weight goal, I want to log my weight with a date, so that I can see how it moves over time.

| ID | Given | When | Then |
|---|---|---|---|
| AC-077 | I am signed in | I enter a weight value and confirm | the entry is saved against today's date by default, with the option to choose a different date |
| AC-078 | I enter a weight outside a sensible range or a non-numeric value | I confirm | the app rejects the entry with an explanatory message and saves nothing |
| AC-079 | I already have a weight entry for the chosen date | I save a new one for the same date | the app updates that date's entry rather than creating a duplicate |
| AC-080 | I record a new current weight | the entry is saved | the app offers to update my profile weight and, if I accept, recalculates my calorie and macro targets |

### US-025: View my weight entries over time

**Priority:** medium

> As a user tracking my weight, I want to see my recorded weights in date order, so that I can tell whether I am moving towards my goal.

| ID | Given | When | Then |
|---|---|---|---|
| AC-081 | I have recorded more than one weight entry | I open the weight log | my entries are listed in date order, most recent first, each showing the date and value |
| AC-082 | I have recorded no weight entries beyond onboarding | I open the weight log | an empty state is shown prompting me to record my first weight |
| AC-083 | I am viewing the weight log | I select an entry | I can edit its value or delete it, and the list updates on save |

## EPIC-007: Nutrition Catalogue and Indian Food Coverage

The curated food catalogue that both photo recognition and search depend on.

Assumptions carried from the confirmed understanding:
- The catalogue is built from IFCT Indian food composition tables, USDA FoodData Central and Open Food Facts, curated into the app's own data model. Licence terms of those sources must be reviewed before launch.
- Indian home and restaurant food is the launch priority; global foods are best-effort and improved later.
- Household portions such as katori, roti and idli are first-class portion units, not free text.
- Barcode scanning against packaged-food data is explicitly out of scope for v1 even though Open Food Facts is a source.

### US-026: Find Indian home and restaurant dishes in the catalogue

**Priority:** critical

> As a user in India, I want the catalogue to contain the dishes I actually eat, so that both photo results and search give me a correct match.

| ID | Given | When | Then |
|---|---|---|---|
| AC-084 | the launch catalogue is loaded | a reviewer searches for common Indian home and restaurant dishes across the agreed launch list (including thali components, curries, breads, rice dishes and regional items) | each dish is present with calories and protein, carbohydrate and fat values for at least one defined portion |
| AC-085 | a dish is known by more than one name or spelling | a user searches by a common alternative name | the same catalogue entry is returned |
| AC-086 | a global or international food is requested | it is not in the curated catalogue | the app returns the closest available match or an empty result with the manual entry path, and this best-effort limitation is accepted for v1 |

### US-027: Use Indian household portion units

**Priority:** high

> As a user describing how much I ate, I want to use everyday units like katori, roti and idli, so that I do not have to guess weights in grams.

| ID | Given | When | Then |
|---|---|---|---|
| AC-087 | a catalogue dish normally served in a household unit | I open its portion selector | the relevant household units (for example 1 katori, 1 roti, 1 idli, 1 piece, 1 glass) are listed with their gram equivalents |
| AC-088 | I select a household unit and quantity | the item is added | calories and macros are calculated from the stored gram equivalent for that unit |
| AC-089 | a food has no meaningful household unit | I open its portion selector | grams or millilitres are offered as the default unit |

### US-028: Trace nutrition values to their source

**Priority:** medium

> As a product owner, I want each catalogue entry to record which source its values came from, so that we can honour licence terms and correct bad data found during the beta.

| ID | Given | When | Then |
|---|---|---|---|
| AC-090 | a catalogue entry has been curated | it is stored | it carries the source it was derived from (IFCT, USDA FoodData Central, Open Food Facts or internally curated) and the date it was imported |
| AC-091 | a nutrition value is found to be wrong during the beta | it is corrected in the catalogue | the correction applies to future logging without altering calorie values already saved on past log entries |
| AC-092 | the sources carry attribution or share-alike obligations | the app is prepared for release | the required attribution is shown within the app and the licence review is recorded |

## EPIC-008: Beta Release Conditions: Access, Language and Data Handling

The cross-cutting conditions of the beta release that the understanding fixed explicitly: free with no payments, English-only, connectivity-dependent, India-hosted data under user control, and non-medical positioning.

Assumptions carried from the confirmed understanding:
- Free during the beta with no in-app payments. A freemium model with daily free scan limits and subscription is the intended path after the MVP but is not built in this version.
- English-only UI at launch, despite the India-first food focus.
- Local meal-logging reminders were discussed as an assumption but are not part of the Lightweight MVP capability set and are not included in this version.
- Target scale is roughly 1,000 beta users; scale and performance work is deliberately deferred until photo-estimation accuracy is proven.

### US-029: Use every feature free during the beta

**Priority:** high

> As a beta user, I want full access with no payment and no scan limits, so that I can use the app freely while it is being proven.

| ID | Given | When | Then |
|---|---|---|---|
| AC-093 | I am a signed-in beta user | I use photo logging, search, manual entry, the daily log, history and the weight log | no feature is gated, no paywall or upgrade prompt is shown, and there is no daily limit on photo scans |
| AC-094 | the app is submitted to the App Store and Play Store | the build is reviewed | it contains no in-app purchase or billing integration |

### US-030: Use the app in English on iOS and Android

**Priority:** high

> As a user in India, I want a single English app available on both mobile platforms, so that I can install it on whichever phone I have.

| ID | Given | When | Then |
|---|---|---|---|
| AC-095 | the beta is released | a user installs it on a supported iOS device or a supported Android device | the same feature set is available on both, built from one cross-platform codebase |
| AC-096 | the device language is set to something other than English | the app opens | the interface is still presented in English, as agreed for launch |
| AC-097 | the beta scope is roughly 1,000 users | that load is applied | the hosted backend serves it without degradation, with broader scale work deferred as agreed |

### US-031: Keep my meal photos and log data under my control

**Priority:** critical

> As a user photographing my food, I want my photos and log stored privately and removable by me, so that I am comfortable using the camera to log meals.

| ID | Given | When | Then |
|---|---|---|---|
| AC-098 | I save a meal photo | it is uploaded | it is stored in the managed cloud backend in an India region and is retrievable only by my authenticated account |
| AC-099 | I am signed in | I view another user's data by any route in the app | access is denied; every log, photo, weight entry and profile is scoped to its owning account |
| AC-100 | I delete a log entry with a photo | the deletion completes | the image is removed from storage and is no longer served by the app |
| AC-101 | the beta is released | I first use the camera | the app states that meal photos are uploaded for analysis and stored with my log, and that I can delete them |

### US-032: Understand that the app is a wellness tool, not medical advice

**Priority:** medium

> As a user, I want the app to be clear about what its numbers mean, so that I do not treat estimates or targets as clinical guidance.

| ID | Given | When | Then |
|---|---|---|---|
| AC-102 | I complete onboarding and receive my derived targets | the targets are first shown | the app states that it is a general wellness tool and does not provide medical or clinical advice |
| AC-103 | I am using the app | I view calorie estimates, macros, targets or weight entries | no diagnosis, clinical interpretation or medical recommendation is presented anywhere |
| AC-104 | the disclaimer has been shown once at onboarding | I look for it again | it remains accessible from the profile or settings area |
<!-- sdlc:auto:end epics -->
