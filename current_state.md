# Current_State.md

## Purpose

Provide Claude with full system context for deep design and iteration.

---

## System Overview

We are building:
A scalable market intelligence engine that identifies entrepreneurial opportunities using structured data pipelines.

---

## Current Status

* Architecture defined
* Schema drafted
* Pipeline phases planned
* No production data yet

---

## Key Design Questions (Claude Focus)

### 1. Entity Resolution Strategy

* How to improve matching accuracy over time?
* Should we introduce ML later or stay rule-based?

---

### 2. Scoring System Design

We need:

* Transparent scoring
* Reliable confidence weighting
* Protection against misleading signals

Questions:

* How should weights evolve?
* How do we prevent bias toward dense cities?

---

### 3. Data Freshness Model

* How do we track staleness?
* Should scores decay over time?

---

### 4. Opportunity Types

We want to detect:

* Underserved markets
* Oversaturated markets
* High-risk/high-reward zones
* Unknown (data-poor) zones

---

### 5. Expansion Strategy

* Best way to expand geographically?
* When to prioritize new regions vs deeper data?

---

## Constraints

* Must remain recomputable
* Must avoid tight coupling
* Must scale to millions of records

---

## Next Design Goals

Claude should:

1. Refine entity resolution logic
2. Improve scoring model robustness
3. Propose metric standardization
4. Suggest long-term evolution paths

---

## Vision

This system should become:
A decision engine that reduces uncertainty for entrepreneurs.

Not just data → but **confidence-backed insight**

---
