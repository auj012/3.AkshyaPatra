# Akshaya Patra — Intelligence Architecture

```text
┌──────────────────────────┐   ┌──────────────────────────┐   ┌──────────────────────────┐
│    USER INTELLIGENCE     │   │    FOOD INTELLIGENCE     │   │   SALES INTELLIGENCE     │
├──────────────────────────┤   ├──────────────────────────┤   ├──────────────────────────┤
│ Customer Profile         │   │ Data Ingestion           │   │ Sales Data               │
│          ↓               │   │          ↓               │   │          ↓               │
│ Sensitivity              │   │ Cleaning / Filtering     │   │ Weekly Aggregation       │
│ Classification           │   │          ↓               │   │          ↓               │
│          ↓               │   │ Ingredient Processing    │   │ Demand Signal            │
│ Sensitivity Score        │   │          ↓               │   │                          │
│                          │   │ Allergen Classification  │   │                          │
│                          │   │          ↓               │   │                          │
│                          │   │ Product Labels           │   │                          │
└────────────┬─────────────┘   └────────────┬─────────────┘   └────────────┬─────────────┘
             │                              │                              │
             └───────────────┬──────────────┴──────────────┬───────────────┘
                             │                             │
                             ▼                             ▼
                  ┌────────────────────────────────────────────────┐
                  │              RECOMMENDATION ENGINE              │
                  ├────────────────────────────────────────────────┤
                  │ Eligibility Filter                             │
                  │                ↓                               │
                  │ Ranking                                        │
                  │                ↓                               │
                  │ Explanation                                    │
                  └────────────────────────────────────────────────┘
```
