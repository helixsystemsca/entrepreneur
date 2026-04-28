# Integration.md

## Purpose

Execution plan for Cursor to build the system in phases.

---

# Phase 1 — Core Infrastructure

### Goals

* Create database schema
* Setup Supabase connection
* Create migration system

### Tasks

* Implement all tables from `schema.md`
* Add indexes for performance
* Setup environment config

---

# Phase 2 — OSM Ingestion

### Goals

* Build first data pipeline

### Tasks

* Implement grid system
* Write OSM pull function
* Store results in `raw_records`

### Constraints

* Must assign each record to a grid
* Must include hashing to prevent duplicates

---

# Phase 3 — Normalization Pipeline

### Goals

* Convert raw → structured

### Tasks

* Normalize names
* Extract categories
* Clean phone/address fields

---

# Phase 4 — Entity Resolution

### Goals

* Deduplicate businesses

### Tasks

* Implement similarity scoring:

  * name similarity
  * geo distance
  * category match

* Merge into `business_entities`

* Link via `entity_sources`

---

# Phase 5 — Job System

### Goals

* Automate ingestion + processing

### Tasks

* Implement job queue (DB-driven)
* Add worker loop
* Support retries + failures

---

# Phase 6 — Playwright Integration

### Goals

* Add dynamic data sources

### Tasks

* Create modular scraper framework
* Assign scraping per grid cell
* Respect rate limits

---

# Phase 7 — Metrics Engine

### Goals

* Compute market signals

### Tasks

* Business density
* Category saturation
* Population ratios

---

# Phase 8 — Opportunity Engine

### Goals

* Generate insights

### Tasks

* Compute opportunity scores
* Store explanations
* Add confidence weighting

---

# Phase 9 — Optimization

### Goals

* Scale safely

### Tasks

* Add caching
* Optimize queries
* Batch processing

---

## Cursor Rules

* Do NOT redesign schema unless critical
* Do NOT mix layers
* Keep functions modular
* Log everything

---
