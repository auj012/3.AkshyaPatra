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
