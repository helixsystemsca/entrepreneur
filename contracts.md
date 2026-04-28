# Contracts.md

## Purpose

Defines strict system contracts so all agents (Cursor, Claude, ChatGPT) operate consistently without breaking architecture.

---

## Core Principles

### 1. Raw Data is Immutable

* `raw_records` is append-only
* Never update or delete raw data
* All transformations happen downstream

---

### 2. Recomputability First

* All derived layers must be rebuildable from raw data
* No critical logic lives only in the database
* Business logic must exist in code (version controlled)

---

### 3. Separation of Concerns

| Layer         | Responsibility                  |
| ------------- | ------------------------------- |
| Raw           | Store source truth              |
| Normalized    | Clean + structured              |
| Entities      | Deduplicated real-world objects |
| Metrics       | Computed signals                |
| Opportunities | User-facing insights            |

---

### 4. No Cross-Layer Leakage

* Normalized cannot modify raw
* Entities cannot directly depend on raw payload shape
* Insights cannot mutate entity data

---

### 5. Idempotent Jobs

All jobs must:

* Be safe to re-run
* Avoid duplicate inserts
* Use deterministic logic where possible

---

### 6. Source Traceability

Every entity must be traceable back to:

* One or more raw records
* A known source
* A timestamp

---

### 7. Schema Stability

* Core tables must not change frequently
* New features → new tables, not destructive edits

---

## Non-Negotiables

* No business logic inside SQL triggers
* No direct writes to `business_entities` without pipeline
* No scraping without grid assignment
* No scoring without confidence

---

## Definition of Done

A feature is complete when:

* It respects all contracts
* It is recomputable
* It does not break existing pipelines
* It includes logging + traceability

---
