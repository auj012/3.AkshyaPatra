# Akshaya Patra — POC Implementation

```text
                         DATA SOURCES
                              │
              ┌───────────────┼───────────────┐
              │               │               │
              ▼               ▼               ▼
        Product Data    Customer Data     Sales Data
          ~400K          Synthetic        Synthetic
              │               │               │
              ▼               ▼               ▼
        Python / Pandas   Python          Python
        Processing       Generator       Generator
              │               │               │
              ▼               ▼               ▼
        ~30K Cookies   Customer Profiles  Weekly Sales
              │               │               │
              ▼               │               │
       Food Intelligence      │               │
       Rules / ML / Hybrid    │               │
              │               │               │
              ▼               │               │
        Product Labels        │               │
              │               │               │
              └───────────────┼───────────────┘
                              ▼
                         SQLite DB
                              │
                              ▼
                   Recommendation Engine
                              │
                    ┌─────────┴─────────┐
                    ▼                   ▼
              Eligibility            Ranking
                Filter                 │
                    │                  │
                    └────────┬─────────┘
                             ▼
                       Recommendation
                             │
                             ▼
                           Output
```
