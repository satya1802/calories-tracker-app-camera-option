# Data Model

<!-- sdlc:auto:start entities -->
### users

| Field | Type | PK | FK | Nullable |
|---|---|---|---|---|
| id | uuid | True | — | False |
| email | varchar | False | — | True |
| password_hash | varchar | False | — | True |
| auth_provider | varchar | False | — | False |
| provider_subject | varchar | False | — | True |
| onboarding_complete | boolean | False | — | False |
| created_at | timestamptz | False | — | False |

### user_profiles

| Field | Type | PK | FK | Nullable |
|---|---|---|---|---|
| id | uuid | True | — | False |
| user_id | uuid | False | users.id | False |
| height_cm | numeric | False | — | False |
| weight_kg | numeric | False | — | False |
| age | int | False | — | False |
| activity_level | varchar | False | — | False |
| goal | varchar | False | — | False |
| updated_at | timestamptz | False | — | False |

### user_targets

| Field | Type | PK | FK | Nullable |
|---|---|---|---|---|
| id | uuid | True | — | False |
| user_id | uuid | False | users.id | False |
| calorie_target | int | False | — | False |
| protein_g | int | False | — | False |
| carb_g | int | False | — | False |
| fat_g | int | False | — | False |
| formula_version | varchar | False | — | False |
| effective_from | timestamptz | False | — | False |

### foods

| Field | Type | PK | FK | Nullable |
|---|---|---|---|---|
| id | uuid | True | — | False |
| name | varchar | False | — | False |
| owner_user_id | uuid | False | users.id | True |
| source | varchar | False | — | False |
| calories_per_100g | numeric | False | — | False |
| protein_per_100g | numeric | False | — | False |
| carb_per_100g | numeric | False | — | False |
| fat_per_100g | numeric | False | — | False |
| search_vector | tsvector | False | — | True |
| imported_at | timestamptz | False | — | True |

### food_aliases

| Field | Type | PK | FK | Nullable |
|---|---|---|---|---|
| id | uuid | True | — | False |
| food_id | uuid | False | foods.id | False |
| alias | varchar | False | — | False |

### portion_units

| Field | Type | PK | FK | Nullable |
|---|---|---|---|---|
| id | uuid | True | — | False |
| food_id | uuid | False | foods.id | False |
| unit_name | varchar | False | — | False |
| gram_equivalent | numeric | False | — | False |
| is_default | boolean | False | — | False |

### meals

| Field | Type | PK | FK | Nullable |
|---|---|---|---|---|
| id | uuid | True | — | False |
| user_id | uuid | False | users.id | False |
| meal_slot | varchar | False | — | False |
| log_date | date | False | — | False |
| origin | varchar | False | — | False |
| photo_key | varchar | False | — | True |
| total_calories | int | False | — | False |
| total_protein_g | int | False | — | False |
| total_carb_g | int | False | — | False |
| total_fat_g | int | False | — | False |
| created_at | timestamptz | False | — | False |

### meal_items

| Field | Type | PK | FK | Nullable |
|---|---|---|---|---|
| id | uuid | True | — | False |
| meal_id | uuid | False | meals.id | False |
| food_id | uuid | False | foods.id | True |
| display_name | varchar | False | — | False |
| quantity | numeric | False | — | False |
| unit_name | varchar | False | — | False |
| grams | numeric | False | — | False |
| calories | int | False | — | False |
| protein_g | int | False | — | False |
| carb_g | int | False | — | False |
| fat_g | int | False | — | False |

### photo_estimates

| Field | Type | PK | FK | Nullable |
|---|---|---|---|---|
| id | uuid | True | — | False |
| user_id | uuid | False | users.id | False |
| meal_id | uuid | False | meals.id | True |
| model_name | varchar | False | — | False |
| original_items_json | jsonb | False | — | False |
| estimated_total_calories | int | False | — | False |
| confidence | varchar | False | — | True |
| accepted_without_edit | boolean | False | — | False |
| created_at | timestamptz | False | — | False |

### weight_entries

| Field | Type | PK | FK | Nullable |
|---|---|---|---|---|
| id | uuid | True | — | False |
| user_id | uuid | False | users.id | False |
| entry_date | date | False | — | False |
| weight_kg | numeric | False | — | False |
<!-- sdlc:auto:end entities -->

<!-- sdlc:auto:start relationships -->
| Source | Target | Type |
|---|---|---|
| users | user_profiles | one-to-one |
| users | user_targets | one-to-many |
| users | meals | one-to-many |
| users | weight_entries | one-to-many |
| users | foods | one-to-many |
| meals | meal_items | one-to-many |
| foods | portion_units | one-to-many |
| foods | food_aliases | one-to-many |
| foods | meal_items | one-to-many |
| meals | photo_estimates | one-to-one |
<!-- sdlc:auto:end relationships -->

<!-- sdlc:auto:start er-diagram -->
```mermaid
erDiagram
  users {
    uuid id PK
    varchar email
    varchar password_hash
    varchar auth_provider
    varchar provider_subject
    boolean onboarding_complete
    timestamptz created_at
  }
  user_profiles {
    uuid id PK
    uuid user_id FK
    numeric height_cm
    numeric weight_kg
    int age
    varchar activity_level
    varchar goal
    timestamptz updated_at
  }
  user_targets {
    uuid id PK
    uuid user_id FK
    int calorie_target
    int protein_g
    int carb_g
    int fat_g
    varchar formula_version
    timestamptz effective_from
  }
  foods {
    uuid id PK
    varchar name
    uuid owner_user_id FK
    varchar source
    numeric calories_per_100g
    numeric protein_per_100g
    numeric carb_per_100g
    numeric fat_per_100g
    tsvector search_vector
    timestamptz imported_at
  }
  food_aliases {
    uuid id PK
    uuid food_id FK
    varchar alias
  }
  portion_units {
    uuid id PK
    uuid food_id FK
    varchar unit_name
    numeric gram_equivalent
    boolean is_default
  }
  meals {
    uuid id PK
    uuid user_id FK
    varchar meal_slot
    date log_date
    varchar origin
    varchar photo_key
    int total_calories
    int total_protein_g
    int total_carb_g
    int total_fat_g
    timestamptz created_at
  }
  meal_items {
    uuid id PK
    uuid meal_id FK
    uuid food_id FK
    varchar display_name
    numeric quantity
    varchar unit_name
    numeric grams
    int calories
    int protein_g
    int carb_g
    int fat_g
  }
  photo_estimates {
    uuid id PK
    uuid user_id FK
    uuid meal_id FK
    varchar model_name
    jsonb original_items_json
    int estimated_total_calories
    varchar confidence
    boolean accepted_without_edit
    timestamptz created_at
  }
  weight_entries {
    uuid id PK
    uuid user_id FK
    date entry_date
    numeric weight_kg
  }
  users ||--|| user_profiles : "one-to-one"
  users ||--o{ user_targets : "one-to-many"
  users ||--o{ meals : "one-to-many"
  users ||--o{ weight_entries : "one-to-many"
  users ||--o{ foods : "one-to-many"
  meals ||--o{ meal_items : "one-to-many"
  foods ||--o{ portion_units : "one-to-many"
  foods ||--o{ food_aliases : "one-to-many"
  foods ||--o{ meal_items : "one-to-many"
  meals ||--|| photo_estimates : "one-to-one"
```
<!-- sdlc:auto:end er-diagram -->
