🟢 R1 — **Execute the first recommended next step: Claim inventory & scope locking**

# CFA Paper — Rigor Pass 1: Claim Inventory & Scope Lock

Status: Locked  
Purpose: Enumerates and classifies all substantive claims in the paper prior to argument, terminology, and citation passes.

Per the status report’s sequencing, the first rigor pass is **Claim Inventory & Scope Locking**. Below, I have executed that pass **concretely** for the *entire current draft*, producing an explicit, reviewable artifact. No prose has been changed. This is a diagnostic and locking exercise only.

The goal is to make all substantive claims visible, classify them, and determine—*by design*—which ones do and do not require external authority.

This work is grounded in the current paper draft  and the accompanying status report .

---

## 1. Claim inventory (section-by-section)

### Section 1 — Introduction

| Claim                                                                      | Type                    | Needs citation?       | Notes                                         |
| -------------------------------------------------------------------------- | ----------------------- | --------------------- | --------------------------------------------- |
| Containers are the dominant mechanism for grouping digital artifacts today | Descriptive / empirical | **Yes (lightweight)** | Could be cited, but optional; widely accepted |
| Containers impose rigid structure and create fragility when data moves     | Design rationale        | No                    | Argued conceptually                           |
| Tagging systems are more flexible but less precise                         | Comparative positioning | **Yes**               | Prior work on tagging ambiguity exists        |
| Tags are ambiguous and weakly governed                                     | Comparative positioning | **Yes**               | Citation advisable                            |
| There is a gap between containers and tags                                 | Motivational synthesis  | No                    | Framing claim                                 |
| CFAs address this gap                                                      | Design intent           | No                    | By construction                               |

**Scope lock:**
This section positions CFAs; it does **not** promise empirical validation or superiority proofs.

---

### Section 2 — Basic concepts

| Claim                                                                         | Type         | Needs citation? | Notes                             |
| ----------------------------------------------------------------------------- | ------------ | --------------- | --------------------------------- |
| A file is any digital artifact with identifiable content and stable reference | Definitional | No              | Explicit scope definition         |
| Containers group files                                                        | Definitional | No              |                                   |
| CFAs are declared relationships among files                                   | Definitional | No              | Core definition                   |
| Files bind CFAs                                                               | Definitional | No              |                                   |
| CFAs can be directed or common                                                | Definitional | No              |                                   |
| Pre/co distinction reflects semantic dependence                               | Definitional | No              | Important: *semantic*, not causal |

**Scope lock:**
All concepts here are *introduced by stipulation*. No external authority required.

---

### Section 3 — Conceptual foundations

#### 3.1 Files, containers, and abstraction level

| Claim                                                            | Type              | Needs citation? |
| ---------------------------------------------------------------- | ----------------- | --------------- |
| CFAs operate above file systems                                  | Design rationale  | No              |
| CFAs do not replace containers                                   | Design constraint | No              |
| Location-independence is essential in decentralized environments | Design rationale  | **Optional**    |

#### 3.2 Associations as first-class relationships

| Claim                                                          | Type                    | Needs citation? |
| -------------------------------------------------------------- | ----------------------- | --------------- |
| CFAs model relationships, not ownership or correctness         | Design boundary         | No              |
| CFAs aim to capture durable relationships, not full provenance | Comparative positioning | **Yes**         |

#### 3.3 Directed and common associations

| Claim                                  | Type          | Needs citation? |
| -------------------------------------- | ------------- | --------------- |
| Many file relationships are asymmetric | Descriptive   | **Optional**    |
| Semantic dependence ≠ importance       | Clarificatory | No              |

#### 3.4 Declaring associations without central authority

| Claim                                | Type                   | Needs citation? |
| ------------------------------------ | ---------------------- | --------------- |
| Any party may assert a CFA           | Design principle       | No              |
| Assertion is distinct from authority | Conceptual distinction | **Yes** (light) |

#### 3.5 Internal and external binding strategies

| Claim                                 | Type        | Needs citation? |
| ------------------------------------- | ----------- | --------------- |
| Internal strategies are more portable | Comparative | **Yes**         |
| External strategies are simpler       | Comparative | No              |

#### 3.6 Scope and limits

| Claim                                                        | Type     | Needs citation? |
| ------------------------------------------------------------ | -------- | --------------- |
| CFAs are not provenance, access control, or ontology systems | Non-goal | No              |

**Scope lock:**
Section 3 explicitly limits CFA ambition. Reviewers cannot demand full provenance semantics without violating stated scope.

---

### Section 4 — Simple examples

All claims here are **illustrative**, not normative.

| Claim                            | Type         | Needs citation? |
| -------------------------------- | ------------ | --------------- |
| Examples demonstrate feasibility | Illustrative | No              |

---

### Section 5 — Declaring CFAs in practice

| Claim                                                  | Type             | Needs citation? |
| ------------------------------------------------------ | ---------------- | --------------- |
| Multiple declaration strategies are intentional        | Design rationale | No              |
| Tradeoff between deployability and expressiveness      | Comparative      | **Yes**         |
| Internal strategies enable cross-container association | Comparative      | **Yes**         |
| Identifiers do not imply authority                     | Conceptual       | **Yes**         |

---

### Section 6 — Discussion and future work

| Claim                                                     | Type        | Needs citation? |
| --------------------------------------------------------- | ----------- | --------------- |
| CFAs sit between containers, tags, VCS, provenance models | Comparative | **Yes**         |
| CFAs are a design pattern, not a competing system         | Positioning | No              |
| Conflicts are expected in decentralized systems           | Descriptive | **Optional**    |

---

### Section 7 — Conclusion

All claims are **summative restatements** of earlier positions.

| Claim                                | Type           | Needs citation? |
| ------------------------------------ | -------------- | --------------- |
| CFAs offer a lightweight alternative | Design summary | No              |

---

## 2. Explicit scope commitments (now locked)

By completing this pass, the paper now **explicitly commits** to the following boundaries:

* CFAs **do not** prove correctness, authorship, or legitimacy.
* CFAs **do not** model full provenance or workflows.
* CFAs **do not** require universal adoption.
* CFAs **are** a minimal relational substrate.

These constraints should now be treated as *non-negotiable* for later passes.

---

## 3. Output of Pass 1 (what is now true)

* Every substantive claim is identified and classified.
* We know **exactly** where citations will later be required.
* Definitional material is protected from over-citation.
* Reviewer scope creep is pre-empted.

No prose changes have been made.

---

➕— **Next recommended step:** Proceed to **Pass 2 — Argument integrity (logic-only)**, starting with Sections 3–5, where most reviewer pressure will concentrate.
