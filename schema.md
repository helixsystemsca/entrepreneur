# Schema.md

## Purpose

Defines the core database structure for a scalable, recomputable market intelligence system.

---

## 1. Locations

```sql
locations (
  id uuid primary key,
  type text,
  name text,
  parent_id uuid,

  lat float,
  lon float,
  bounds jsonb,

  population int,
  metadata jsonb,

  created_at timestamp
)
```

---

## 2. Grid Cells

```sql
grid_cells (
  id uuid primary key,
  location_id uuid,

  bounds jsonb,
  centroid geometry,

  priority_score float,
  status text,

  last_processed_at timestamp
)
```

---

## 3. Raw Records (Immutable)

```sql
raw_records (
  id uuid primary key,
  source text,
  external_id text,

  grid_id uuid,
  location_id uuid,

  payload jsonb,
  fetched_at timestamp,

  hash text
)
```

---

## 4. Normalized Places

```sql
normalized_places (
  id uuid primary key,
  raw_id uuid,

  name text,
  name_normalized text,

  category text,

  lat float,
  lon float,

  address text,
  phone text,
  website text,

  extracted_at timestamp
)
```

---

## 5. Business Entities

```sql
business_entities (
  id uuid primary key,

  canonical_name text,
  category_primary text,

  lat float,
  lon float,
  location_id uuid,

  address text,
  phone text,
  website text,

  confidence_score float,
  data_completeness float,

  first_seen_at timestamp,
  last_verified_at timestamp,

  created_at timestamp,
  updated_at timestamp
)
```

---

## 6. Entity Sources

```sql
entity_sources (
  id uuid primary key,
  entity_id uuid,
  raw_id uuid,

  source text,
  trust_weight float,

  matched_at timestamp
)
```

---

## 7. Metrics (Flexible Layer)

```sql
metrics (
  id uuid primary key,

  entity_id uuid,
  location_id uuid,
  category text,

  metric_name text,
  metric_value float,

  calculated_at timestamp
)
```

---

## 8. Opportunities

```sql
opportunities (
  id uuid primary key,

  location_id uuid,
  category text,

  score float,
  confidence float,

  summary text,

  calculated_at timestamp
)
```

---

## 9. Opportunity Factors (Explainability)

```sql
opportunity_factors (
  id uuid primary key,
  opportunity_id uuid,

  factor_name text,
  factor_value float,
  weight float
)
```

---

## 10. Jobs (Scheduler Backbone)

```sql
jobs (
  id uuid primary key,

  type text,
  target_id uuid,
  source text,

  priority float,

  status text,

  scheduled_at timestamp,
  completed_at timestamp
)
```

---

## Design Notes

* All tables must include indexes on:

  * `location_id`
  * `category`
  * `created_at`

* Avoid foreign key constraints early if they slow ingestion

* Add them later once pipelines stabilize

---
