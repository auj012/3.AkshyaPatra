# Akshaya Patra — Proof of Concept Requirements Document

| Field | Value |
|---|---|
| Product | Akshaya Patra — Food Discovery Engine |
| Document Type | Proof of Concept PRD |
| Status | POC Planning |
| Author | Ushasree Jakilinki |
| Version | 1.0 |
| Last Updated | August 2026 |

---

## 1. POC Summary

This proof of concept will validate the technical and product feasibility of Akshaya Patra's core food discovery workflow.

The POC will use:

- Real USDA Branded Foods product data.
- A staged pipeline that filters approximately 400,000 source records.
- An approximately 30,000-product cookie working dataset.
- Synthetic customer profiles.
- Synthetic current-week sales data.
- A deterministic, rule-based food-intelligence baseline.

The POC will test whether Akshaya Patra can:

1. Extract structured food intelligence from product records.
2. Apply standardized product labels.
3. Match products against confirmed customer constraints.
4. Exclude unsafe or unsuitable products.
5. Rank eligible products using current-week sales.
6. Explain why products were included, excluded, or marked uncertain.

---

## 2. POC Objective

Demonstrate an explainable end-to-end food discovery workflow that identifies product sensitivity signals, labels products, filters products against confirmed customer constraints, and ranks only eligible products.

---

## 3. POC Hypothesis

> Given a real product dataset, synthetic customer profiles, and synthetic current-week sales signals, Akshaya Patra can demonstrate an explainable end-to-end food discovery workflow that identifies relevant product sensitivities, labels products, filters products against confirmed customer constraints, and ranks eligible products.

---

## 4. POC Questions

The POC is designed to answer the following questions.

### Question 1 — Can the product pipeline process the available source data?

Can the approximately 400,000 USDA Branded Foods records be processed through staged cleanup and filtering to create a usable cookie dataset?

### Question 2 — Can deterministic food intelligence identify relevant signals?

Can rule-based processing derive useful allergen, sensitivity, dietary, and ingredient-related signals from the available product information?

### Question 3 — Can products be labeled consistently?

Can food intelligence be transformed into a standardized, queryable product label structure?

### Question 4 — Can confirmed user constraints be respected?

Can synthetic customer profiles be matched against product labels so that conflicting products are excluded?

### Question 5 — Can eligible products be ranked safely?

Can current-week sales influence ranking only after safety and suitability filtering has occurred?

### Question 6 — Is ML/NLP justified?

Does an ML/NLP candidate create enough measurable improvement over the rule-based baseline to justify additional complexity, cost, and reduced explainability?

---

## 5. Scope

### In Scope

- USDA Branded Foods source dataset.
- Approximately 400,000 source product records processed through staged cleanup.
- Approximately 30,000 cookie products used as the working dataset.
- Product and ingredient intelligence extraction.
- Rule-based allergen and sensitivity signal detection.
- Standardized product labeling.
- Structured product database or queryable product output.
- Synthetic customer profiles.
- Synthetic current-week sales data.
- Safe product eligibility filtering.
- Ranking of eligible products.
- Recommendation explanations.
- Rule-based baseline evaluation.
- Foundation for ML/NLP comparison.

### Out of Scope

- Full U.S. food product coverage.
- Product-market fit validation.
- Real customer behavior analysis.
- Real customer preference data.
- Real current-week sales data.
- Medical advice or medical diagnosis.
- A guarantee of individual medical safety.
- Retail purchasing, checkout, or inventory integration.
- Production-scale security, compliance, or deployment.
- A final decision to use ML/NLP.
- Claims of real-world recommendation effectiveness.

---

## 6. Data Strategy

### Product Data

| Attribute | POC Plan |
|---|---|
| Source | USDA Branded Foods |
| Data Type | Real product data |
| Source Scale | Approximately 400,000 records -https://fdc.nal.usda.gov/download-datasets Branded |
| Working Dataset | Approximately 30,000 cookie products |
| Purpose | Build and evaluate product-level food intelligence |
| Constraint | Product information may be incomplete, ambiguous, or inconsistent |

### Customer Data

| Attribute | POC Plan |
|---|---|
| Source | Generated profiles |
| Data Type | Synthetic |
| Purpose | Test matching, eligibility filtering, and recommendation workflows |
| Limitation | Does not represent real behavior, trust, adoption, or preferences |

A synthetic customer profile may include:

- Customer ID
- Confirmed allergens
- Confirmed sensitivities
- Dietary restrictions
- Dietary preferences
- Ingredient exclusions
- Other selected food criteria

### Current-Week Sales Data

| Attribute | POC Plan |
|---|---|
| Source | Generated weekly sales records |
| Data Type | Synthetic |
| Purpose | Test ranking among eligible products |
| Example Fields | Product_ID, Week, Units_Sold |
| Limitation | Does not represent real demand or shopping behavior |

---

## 7. Why Cookies?

Cookies are the bounded POC category because they are:

- Large enough to demonstrate the product concept.
- Small enough for local development and repeated testing.
- Rich enough in ingredient variation to test food-intelligence logic.
- Suitable for illustrating the full pipeline from raw data through recommendations.

The cookie dataset is a POC boundary. It is not the intended long-term scope of Akshaya Patra.

---

## 8. POC Product Flow

```text
USDA Branded Foods Dataset
      ↓
Staged Cleaning and Filtering
      ↓
Cookie Working Dataset
      ↓
Phase 1: Food Intelligence
      ↓
Phase 2: Product Labels
      ↓
Synthetic Customer Profile
      ↓
Safety / Suitability Filtering
      ↓
Synthetic Current-Week Sales
      ↓
Eligible Product Ranking
      ↓
Recommendation + Explanation
```

---

## 9. Phase 1 Requirements — Predict Sensitivities

### Objective

Create product-level food intelligence that identifies relevant allergen, sensitivity, dietary, and ingredient-related signals from available product information.

### Inputs

- Cookie product records.
- Product names.
- Ingredients.
- Available allergen statements.
- Other available product attributes.

### Outputs

Structured product-level sensitivity signals that can be consumed by downstream labeling and recommendation capabilities.

### Initial Approach

The POC will begin with deterministic, rule-based processing.

The rule-based approach should include:

- Ingredient dictionaries.
- Allergen dictionaries.
- Ingredient aliases and variants.
- Pattern matching.
- Explicit handling of uncertainty.
- Traceable logic for each detected signal.

### Functional Requirements

| ID | Requirement |
|---|---|
| P1-FR-01 | The system shall process product records in stages rather than loading the full source dataset into memory at once. |
| P1-FR-02 | The system shall identify product records relevant to the cookie category. |
| P1-FR-03 | The system shall extract available product names, ingredients, and allergen-related fields. |
| P1-FR-04 | The system shall apply deterministic rules to identify supported sensitivity or allergen signals. |
| P1-FR-05 | The system shall retain evidence or rule output that explains detected signals. |
| P1-FR-06 | The system shall identify records with missing, ambiguous, or insufficient information. |
| P1-FR-07 | The system shall produce structured output suitable for product labeling. |

### Evaluation Measures

- Precision
- Recall
- F1 score
- False-negative count
- Coverage
- Unknown or insufficient-data rate

---

## 10. Phase 2 Requirements — Label Products

### Objective

Transform Phase 1 product intelligence into standardized product labels that downstream filtering and ranking logic can query consistently.

### Example Output

| Product | Milk | Soy | Wheat | Peanut | Tree Nuts |
|---|---|---|---|---|---|
| Cookie A | Contains | Contains | Contains | Not Detected | Unknown |

### Label States

The initial label taxonomy should support:

- Contains
- Not Detected
- May Contain
- Unknown
- Insufficient Data

### Functional Requirements

| ID | Requirement |
|---|---|
| P2-FR-01 | The system shall convert Phase 1 signals into standardized labels. |
| P2-FR-02 | Each supported allergen or sensitivity category shall have an explicit label state. |
| P2-FR-03 | The system shall preserve unknown or insufficient-data states. |
| P2-FR-04 | The system shall store product labels in a structured, queryable format. |
| P2-FR-05 | The system shall support traceability from labels to the underlying rule evidence. |
| P2-FR-06 | The labeling logic shall be deterministic and reproducible for the baseline. |
| P2-FR-07 | The label output shall support automated test cases and evaluation. |

### Evaluation Plan

The team will establish a defined set of ground-truth or manually reviewed test cases.

The evaluation will compare:

```text
Rule-Based Baseline
       vs.
ML/NLP Candidate, if evaluated
```

Measures may include:

- Accuracy
- Precision
- Recall
- F1 score
- Coverage
- Explainability
- Maintenance effort
- Computational cost
- Implementation complexity

---

## 11. Phase 3 Requirements — Recommend Safely

### Objective

Use product labels and a confirmed customer profile to identify eligible products, exclude conflicting products, and rank only eligible products.

### Inputs

```text
Confirmed Customer Profile
        +
Structured Product Labels
        +
Synthetic Current-Week Sales
```

### Outputs

A ranked list of eligible product recommendations with understandable explanations.

### Safety Flow

```text
Customer Profile
      ↓
Safety / Suitability Check
      ↓
Eligible Products Only
      ↓
Current-Week Sales Signal
      ↓
Ranking
      ↓
Recommendation
```

### Functional Requirements

| ID | Requirement |
|---|---|
| P3-FR-01 | The system shall accept a customer profile with confirmed allergens, sensitivities, restrictions, and preferences. |
| P3-FR-02 | The system shall compare each product's labels against confirmed customer constraints. |
| P3-FR-03 | The system shall exclude products that conflict with a confirmed user constraint. |
| P3-FR-04 | The system shall handle unknown or insufficient product information conservatively according to defined rules. |
| P3-FR-05 | The system shall apply current-week sales only after eligibility filtering. |
| P3-FR-06 | The system shall never use current-week sales to override a safety exclusion. |
| P3-FR-07 | The system shall return ranked eligible products. |
| P3-FR-08 | The system shall return an explanation for each recommendation. |
| P3-FR-09 | The system shall return exclusion reasons when a product is not eligible. |

### Recommendation Example

```text
Recommended: Cookie A

Why:
- No detected conflict with your confirmed profile.
- Matches your selected dietary preferences.
- Ranked highly among eligible products using synthetic current-week sales.

Important:
- Product information may be incomplete.
- This result is decision support, not medical advice.
```

---

## 12. User Stories

### Safety and Suitability

**As a consumer with a confirmed peanut allergy,**  
I want products with a detected peanut conflict excluded from recommendations,  
so that popularity or sales do not override my confirmed safety constraint.

**As a consumer with multiple food restrictions,**  
I want to see only products that match my confirmed profile,  
so that I do not repeatedly inspect every label manually.

### Transparency

**As a user,**  
I want to understand why a product was recommended,  
so that I can decide whether it is appropriate for me.

**As a user,**  
I want the system to show when product information is unknown or incomplete,  
so that I do not mistake uncertainty for safety.

### Product Evaluation

**As a product team member,**  
I want to compare rule-based labeling with an ML/NLP alternative,  
so that we can choose the approach that provides the best trade-off among quality, explainability, cost, and maintenance.

---

## 13. Non-Functional Requirements

| Category | Requirement |
|---|---|
| Explainability | Every detected signal, label, eligibility result, and recommendation should be traceable to understandable logic or data. |
| Reproducibility | The POC should produce consistent results when run against the same source data and rules. |
| Data processing | The product pipeline should support staged processing for the approximately 400,000-record source dataset. |
| Maintainability | Rules, dictionaries, and supported categories should be stored in a structure that can be inspected and updated. |
| Auditability | Outputs should retain enough information to investigate why a product was labeled, excluded, or recommended. |
| Safety | Confirmed constraints must be evaluated before ranking. |
| Transparency | Synthetic data must be visibly labeled as synthetic in documentation, demonstrations, and evaluation outputs. |

---

## 14. POC Success Criteria

### Data

- The source dataset can be processed through staged cleaning.
- A usable cookie working dataset of approximately 30,000 products can be produced.
- Product data quality issues and unknowns are tracked.

### Phase 1

- Product information can be transformed into structured sensitivity signals.
- A deterministic food-intelligence baseline can be demonstrated.
- Outputs include evidence or traceability for identified signals.

### Phase 2

- Products can be consistently labeled using a standardized taxonomy.
- Labels can be stored and queried in a structured format.
- The baseline can be evaluated against defined ground-truth or test cases.

### Phase 3

- Synthetic customer profiles can be matched against product labels.
- Conflicting or ineligible products are excluded.
- Synthetic current-week sales can rank products only after eligibility is established.
- Recommendations include understandable rationales.

### Overall

- The POC demonstrates technical and product feasibility of the three-phase workflow.
- The POC produces evidence that supports a decision about next-stage investment.
- The POC does not claim market validation, product-market fit, or real-world recommendation effectiveness.

---

## 15. Evaluation Strategy

### Question 1 — Can We Identify the Right Signals?

**Phase:** Phase 1

| Measure | Purpose |
|---|---|
| Precision | Determine how often detected signals are correct |
| Recall | Determine how many relevant signals are detected |
| F1 | Balance precision and recall |
| False negatives | Identify potentially consequential missed signals |
| Coverage | Measure the share of products that receive usable output |

### Question 2 — Can We Label Products Reliably?

**Phase:** Phase 2

| Comparison | Measures |
|---|---|
| Rule-based baseline | Accuracy, precision, recall, F1, coverage, explainability, maintenance, cost |
| ML/NLP candidate | Accuracy, precision, recall, F1, coverage, explainability, maintenance, cost |
| Hybrid candidate | Incremental value relative to added complexity |

### Question 3 — Can We Recommend Appropriately?

**Phase:** Phase 3

| Measure | Purpose |
|---|---|
| Safety constraint adherence | Confirm conflicting products are excluded |
| Eligibility accuracy | Confirm only appropriate products move to ranking |
| Ranking behavior | Confirm sales affects only eligible-product order |
| Explanation quality | Confirm users can understand result reasons |
| Unknown handling | Confirm uncertain products are not treated as confirmed-safe |

---

## 16. Risks and Mitigations

| Risk | Impact | POC Mitigation |
|---|---|---|
| No real customer data | Cannot validate real behavior, trust, or adoption | Use synthetic profiles only for workflow testing |
| No real sales data | Cannot validate real demand | Use synthetic weekly sales only for ranking mechanics |
| Ingredient ambiguity | Labels may be incomplete or incorrect | Use rule dictionaries, conservative states, and evaluation cases |
| Rule-based brittleness | Relevant patterns may be missed | Measure gaps and evaluate ML/NLP alternatives |
| Synthetic-data bias | Generated scenarios may be unrealistic | Define controlled profile and ranking scenarios |
| Product-data limitations | Some product records may be incomplete | Track unknown and insufficient-data states |
| Safety risk | Incorrect interpretation may have serious consequences | Use confirmed hard filters, conservative handling, and explicit limitations |
| Scope creep | POC may become an unbounded product build | Maintain explicit in-scope and out-of-scope boundaries |

---

## 17. POC Limitations

This POC can validate:

- Data structures
- Data processing workflow
- Rule-based signal detection
- Product labeling logic
- Eligibility filtering
- Ranking logic
- Explanation patterns
- Evaluation mechanics

This POC cannot validate:

- Real consumer needs
- Real consumer preferences
- Real customer behavior
- Product adoption
- User trust
- Product-market fit
- Real demand
- Real sales performance
- Medical safety for any individual
- Real-world recommendation effectiveness

---

## 18. Exit Criteria and Next Decision

The POC is complete when the team can demonstrate:

1. A staged pipeline from USDA source records to a cookie working dataset.
2. Structured product-level food intelligence.
3. Consistent standardized product labels.
4. Safe filtering against synthetic confirmed customer profiles.
5. Ranking that applies synthetic sales only among eligible products.
6. Explanations for inclusion, exclusion, and uncertainty.
7. Evaluation results for the rule-based baseline.
8. A documented recommendation on whether to:
   - Improve the rules and data quality.
   - Evaluate an ML/NLP candidate.
   - Expand product categories.
   - Begin controlled user testing.
   - Plan a future MVP.

---

## 19. Post-POC Path

```text
POC
 ↓
Evaluate Technical and Product Feasibility
 ↓
Improve Data and Labeling Quality
 ↓
Collect Real Customer Evidence
 ↓
Incorporate Real Sales or Availability Signals
 ↓
Expand Product Categories
 ↓
Conduct User Testing
 ↓
Build MVP
```

The POC is not the MVP.

The POC proves whether the core concept and workflow justify further investment. A later MVP should test whether real users experience enough value to use, trust, and return to Akshaya Patra.
