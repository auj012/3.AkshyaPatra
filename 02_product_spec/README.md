# 02 — Product Specification

> Generated from `Product_PRD.md` and `POC_PRD.md`.

# Akshaya Patra — Product Requirements Document

| Field | Value |
|---|---|
| Product | Akshaya Patra — Food Discovery Engine |
| Document Type | Product PRD |
| Status | Product Definition |
| Author | Ushasree Jakilinki |
| Version | 1.0 |
| Last Updated | August 2026 |

---

## 1. Product Summary

Akshaya Patra is a food discovery engine designed to help people discover food products that better match their allergies, sensitivities, dietary restrictions, dietary preferences, and health-related food needs.

The product reduces the repeated manual work of searching for products, reading labels, decoding ingredients, identifying potential conflicts, comparing alternatives, and making food-selection decisions.

### Product Promise

> **We find what you can't see.**

Akshaya Patra is intended to make food discovery more personalized, explainable, and manageable while preserving user control over safety-related decisions.

---

## 2. Problem Statement

Consumers with food allergies, sensitivities, dietary restrictions, or health-related food needs face a repeated discovery burden.

Today, the food-selection process often looks like this:

```text
User needs food
      ↓
Searches for products
      ↓
Reads product labels
      ↓
Decodes ingredients
      ↓
Checks allergens and restrictions
      ↓
Compares alternatives
      ↓
Makes a safety or suitability decision
      ↓
Repeats on the next shopping trip
```

The problem is not simply finding food.

The problem is finding the **right food** within a large, changing product universe while accounting for a person's individual needs and preferences.

Users must repeatedly translate unstructured product information into a decision about whether a product is appropriate for them.

---

## 3. Product Vision

Akshaya Patra will become a trusted food discovery layer that helps users move from manual label research toward personalized product discovery.

The long-term product should enable users to:

- Define and manage their confirmed food needs.
- Discover products that fit confirmed constraints.
- Understand why products are included or excluded.
- Compare relevant product alternatives.
- Receive recommendations without safety exclusions being overridden by popularity or commercial signals.
- Retain control over any inferred or suggested preferences.

---

## 4. Target Users

### Primary User

A consumer who needs to identify food products according to one or more of the following:

- Food allergies
- Food sensitivities
- Dietary restrictions
- Dietary preferences
- Health-related food preferences
- Ingredient exclusions
- Lifestyle or cultural food requirements

### Secondary User

Caregivers, parents, or household decision-makers who manage food needs for multiple people.

### Core User Job

> Help me discover safe, relevant, and appealing food products without repeatedly researching ingredients and labels myself.

---

## 5. User Needs

| User Need | Current Difficulty | Product Outcome |
|---|---|---|
| Identify products that fit confirmed needs | Ingredient and allergen details are inconsistent or difficult to interpret | Structured product intelligence |
| Avoid unsuitable products | Users may overlook conflicts or incomplete information | Conservative filtering and explicit uncertainty |
| Discover alternatives | Manual searching is repetitive and time-consuming | Personalized eligible-product discovery |
| Understand recommendations | Recommendations can feel opaque or untrustworthy | Clear explanations for inclusion and exclusion |
| Maintain control | Inferred preferences may be incorrect | User confirmation for safety-related constraints |

---

## 6. Product Principles

### 1. Safety Before Popularity

A product that violates a confirmed user constraint must not be recommended, regardless of sales, popularity, or other ranking signals.

### 2. User Remains in Control

Akshaya Patra assists with discovery. It does not make medical safety decisions for the user.

### 3. Explainability Matters

Users should be able to understand why a product was included, excluded, or marked as uncertain.

### 4. Confirmed Constraints Are Treated Differently

Confirmed allergens, sensitivities, and restrictions are hard safety or suitability constraints.

Inferred preferences may be presented as suggestions but must not silently become safety restrictions.

### 5. Unknown Must Remain Visible

When product information is incomplete, conflicting, or insufficient, the system must preserve that uncertainty rather than treating it as safe.

### 6. Evidence Before AI Complexity

The product should use the simplest viable approach that meets quality, safety, and maintainability needs.

ML/NLP should be introduced when evidence demonstrates meaningful improvement over deterministic approaches.

### 7. Synthetic Data Must Be Identified Clearly

Synthetic data is appropriate for testing workflows and logic but must never be represented as real customer, sales, adoption, or market evidence.

---

## 7. Product Concept

Akshaya Patra is organized around three connected capabilities.

```text
                    AKSHAYA PATRA
                         │
          ┌──────────────┼──────────────┐
          ↓              ↓              ↓
       PHASE 1         PHASE 2        PHASE 3
       Predict         Label          Recommend
     Sensitivities    Products          Safely
```

### Phase 1 — Predict Sensitivities

Identify relevant allergen, sensitivity, dietary, and ingredient-related signals from available product information.

**Outcome:** Product-level food intelligence.

### Phase 2 — Label Products

Transform product intelligence into standardized and queryable product labels.

**Outcome:** A structured product representation that downstream filtering and recommendation services can use consistently.

### Phase 3 — Recommend Safely

Match a customer's confirmed profile against eligible products, then rank only those eligible products using permitted ranking signals.

**Outcome:** A ranked, explainable set of suitable product recommendations.

---

## 8. Intended Product Experience

```text
User Profile
     ↓
Product Intelligence
     ↓
Sensitivity Identification
     ↓
Product Labeling
     ↓
Safety / Suitability Filtering
     ↓
Permitted Ranking Signals
     ↓
Recommendation Ranking
     ↓
Recommendation + Explanation
```

The intended user experience moves food discovery away from repeated manual ingredient research while retaining user visibility and decision-making control.

---

## 9. Core Product Requirements

### Product Profile Management

The product should allow a user to maintain a profile containing confirmed food constraints and preferences.

The profile may include:

- Confirmed allergens
- Confirmed sensitivities
- Dietary restrictions
- Dietary preferences
- Ingredient exclusions
- Household member needs
- Other selected food criteria

### Product Intelligence

The system should derive structured signals from product-level data, including ingredient information and available allergen declarations.

The system should preserve source information and uncertainty where practical.

### Structured Product Labels

The system should represent relevant product attributes using consistent labels.

Example:

| Attribute | Label |
|---|---|
| Milk | Contains |
| Soy | Contains |
| Wheat | Contains |
| Peanut | Not Detected |
| Tree nuts | Unknown |

Suggested label states:

- Contains
- Not Detected
- May Contain
- Unknown
- Insufficient Data
- Not Applicable

### Eligibility Filtering

The system must evaluate products against the user's confirmed profile before any ranking occurs.

Products with detected conflicts against a confirmed exclusion must be excluded from recommendations.

### Ranking

The system may apply ranking signals only after product eligibility has been determined.

Potential future ranking signals may include:

- Product relevance
- User preferences
- Product availability
- Current demand
- Current-week sales
- Product quality signals
- User feedback

### Explanations

Every recommendation should provide a concise explanation that describes:

- Why the product is eligible.
- Which confirmed constraints it satisfies.
- Which product signals informed the result.
- Whether relevant information is unknown or insufficient.
- Which non-safety signals influenced ranking.

Example:

> Recommended because no detected conflict was found with your confirmed profile. This product is ranked highly among eligible options based on your preferences and current product demand.

---

## 10. Safety Requirements

Akshaya Patra is a food discovery and decision-support product, not a medical device or medical advice service.

The product must:

- Treat confirmed safety constraints as hard filters.
- Never let a ranking signal override a confirmed exclusion.
- Clearly surface uncertain, incomplete, or unavailable product information.
- Avoid silently inferring medical conditions or safety constraints.
- Require user confirmation before treating suggestions as safety-related profile restrictions.
- Communicate that users should verify labels and consult qualified professionals when appropriate.

The product must not:

- Guarantee individual medical safety.
- Diagnose allergies, intolerances, or health conditions.
- Provide medical advice.
- Represent uncertain product data as confirmed-safe information.

---

## 11. Future Product Scope

The long-term Akshaya Patra product may expand across the following dimensions.

| Area | Future Direction |
|---|---|
| Product coverage | Expand beyond cookies into broader food categories |
| Product data | Add retailer, manufacturer, and verified product data sources |
| Customer data | Support real user profiles with consent and privacy controls |
| Ranking | Add availability, preferences, feedback, and demand signals |
| Intelligence | Evaluate ML/NLP or hybrid approaches where justified |
| User experience | Add saved lists, household profiles, comparisons, and alerts |
| Validation | Conduct user research, usability testing, and real-world pilots |
| Integrations | Connect to grocery, retailer, shopping, or inventory systems |

---

## 12. Out of Scope

The initial product definition does not include:

- Medical diagnosis
- Medical advice
- Guaranteed medical safety
- Automatic inference of unconfirmed safety constraints
- A claim of complete coverage of the U.S. food universe
- A claim that every ingredient listing is complete, current, or error-free
- A commitment to a specific ML model or NLP approach
- A commitment to a specific retailer, commerce, or checkout integration

---

## 13. Product Success Measures

Future product success should be evaluated across four areas.

### User Value

- Reduction in reported manual research effort
- Time to identify suitable products
- User understanding of recommendations
- User confidence in explanations
- Repeat use and retention

### Safety and Suitability

- Constraint adherence
- Rate of conflicting recommendations
- Rate of correctly surfaced unknowns
- User-reported product relevance

### Product Intelligence Quality

- Precision
- Recall
- F1 score
- Coverage
- False-negative rate
- Explanation accuracy

### Business and Product Validation

- User adoption
- Engagement
- Profile completion
- Saved or selected products
- Customer feedback
- Product-market fit indicators

---

## 14. Risks and Constraints

| Risk or Constraint | Product Impact | Product Response |
|---|---|---|
| Incomplete ingredient data | Incorrect or uncertain product interpretation | Preserve uncertainty and display data limitations |
| Ingredient ambiguity | Possible incorrect allergen or sensitivity labeling | Use conservative rules, evaluation, and review processes |
| Product data changes | Previously processed information may become outdated | Support refresh and versioning strategies |
| False negatives | Potentially consequential user outcome | Prioritize conservative exclusions and explicit limitations |
| User trust | Users may not rely on opaque recommendations | Provide traceable explanations |
| Data privacy | Customer profiles may contain sensitive food-related data | Use consent, minimization, and appropriate access controls |
| Model brittleness | Rules or models may miss patterns | Measure performance and evaluate alternatives |
| Regulatory expectations | Food and health-related claims can create risk | Clearly define the product as decision support, not medical advice |

---

## 15. Product Decision Framework

Akshaya Patra should use evidence to decide when to add technical complexity.

```text
Rule-Based Baseline
      ↓
Evaluation
      ↓
Quality Gap Identified?
      ↓
No ──→ Improve Rules and Data Quality
      ↓
Yes
      ↓
Evaluate ML/NLP Candidate
      ↓
Compare Quality, Cost, Explainability, and Maintenance
      ↓
Select Rules, ML/NLP, or Hybrid Approach
```

The decision is not whether to use AI for appearance. The decision is whether a more complex method creates measurable product value without compromising safety, explainability, or maintainability.

---

## 16. Open Questions

- Which product data sources will provide the most reliable and complete ingredient information at scale?
- What label taxonomy best represents ambiguity, cross-contact risk, and incomplete information?
- Which user controls are necessary for profile creation and confirmation?
- What explanation format creates understanding without overstating certainty?
- What performance threshold is required before expanding to additional food categories?
- When should human review be introduced for ambiguous or high-risk product records?
- Which privacy, security, and consent requirements apply before real customer profiles are collected?

---

## 17. Product Direction

Akshaya Patra will begin by proving that structured food intelligence can support safe, explainable product discovery.

The initial POC validates feasibility. A future MVP should validate whether real users receive enough value from the experience to adopt and trust it.

---

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
