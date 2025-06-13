# Term Deposit Marketing Prediction & Subscriber Segmentation

##  Project Overview  
At Apziva, I designed and delivered a machine-learning solution for a European bank’s term-deposit campaign. Our goals were to:

1. **Predict** which customers would subscribe to a term deposit  
2. **Segment** the subscriber base into actionable sub-groups  

This enabled the client to focus on high-value prospects and tailor their outreach scripts and offers.

---

## Project Workflow  
1. **Data Ingestion & Definition**  
   - Loaded 40 000 call records with 14 attributes (age, job, balance, contact details, call metadata, etc.)  
   - Defined numeric vs. categorical fields for consistent processing  

2. **Exploratory Data Analysis (EDA)**  
   - Uncovered the strongest conversion drivers  
   - Benchmarked subscriber vs. non-subscriber behavior  

3. **Train/Test Split**  
   - Performed a 75/25 stratified split (seed=42)

4. **Model Selection & Tuning**  
   - Used PyCaret to compare models and tune hyperparameters  
   - Selected LightGBM and further tuned with PyCaret 

5. **Feature Selection**  
   - Identified the top predictors for conversion  

6. **Subscriber Extraction (SQL)**  
   - Isolated the 2 896 subscribers (7.24% conversion) via DuckDB  

7. **Subscriber Segmentation (K-Means)**  
   - Ran K-Means (k=4) on scaled numeric features to discover four distinct subscriber personas  

8. **Insights & Business Impact**  
   - Synthesized findings into targeted recommendations  

---

## EDA Key Insights  
- **Call Duration**  
  - **Median** for subscribers: **629 s** vs. **164 s** for non-subscribers  
  - Longer conversations drive higher conversions  

- **Account Balance**  
  - **Median** balance: **€620** (subscribers) vs. **€395** (non-subscribers)  
  - Wealthier customers are more likely to subscribe  

- **Campaign Attempts**  
  - **Mean** attempts before conversion: **2.41** (subscribers) vs. **2.92** (non-subscribers)  
  - Diminishing returns after two calls  

- **Age**  
  - **Median** age: **37** (subscribers) vs. **39** (non-subscribers)  
  - Only a small difference, other factors are more decisive  

- **Job Segments**  
  - **Highest conversion rates:**  
    - Students: **15.65 %**  
    - Retirees: **10.51 %**  
    - Unemployed: **8.70 %**  
  - **Lowest conversion rates:**  
    - Housemaids: **4.88 %**  
    - Blue-collar: **5.70 %**  

---

## Modeling & Feature Importance  
After comparing multiple algorithms, **LightGBM** delivered the best balance of precision and recall on the "yes" class.  

**Top 5 Predictive Features (Random Forest importances):**  
| Feature   | Relative Importance |
|-----------|---------------------:|
| duration  |                37.7% |
| balance   |                12.0% |
| age       |                10.4% |
| day       |                10.1% |
| campaign  |                 4.6% |

---

## Subscriber Segmentation (k = 4)  
Clustered the 2896 subscribers using numeric features (`age`, `balance`, `duration`, `campaign`, `day`). Four meaningful segments emerged:

| Cluster | Size | Avg Age | Avg Balance | Avg Duration | Avg Attempts | Characteristics                               |
|:-------:|-----:|--------:|------------:|-------------:|-------------:|-----------------------------------------------|
| 0       |  774 |    53.2 |     €1,429  |       586 s  |        1.92  | Older, low balance, moderate call lengths     |
| 1       | 1419 |    32.8 |     €1,047  |       529 s  |        1.77  | Young adults, moderate balance & durations    |
| 2       |  116 |    42.1 |    €12,217  |       627 s  |        2.42  | Mid-age, very high balances                   |
| 3       |  587 |    38.8 |     €1,009  |      1197 s  |        4.64  | Moderate age/balance, very long & repeated calls |

**Actionable Takeaways:**  
- **Cluster 2 (High-Balance subscribers):** Prioritize for premium term-deposit offers.  
- **Cluster 3 (Engaged callers with long durations):** Tailor detailed product walkthroughs as they respond to extended conversations.  
- **Cluster 1 (Younger customers):** Offer entry-level or flexible-term products.  
- **Cluster 0 (Older, low-balance):** Bundle marketing with cross-sell opportunities (e.g., savings or retirement planning).

---

## Conclusion & Next Steps  
- **Business Impact:**  
  - Focusing on high-value segments could lift overall campaign ROI by an estimated **15 %**.  
  - Tailored scripts per cluster enable more efficient agent time allocation and stronger customer engagement.

I welcome any questions and look forward to discussing how these techniques can be applied to your data-driven marketing challenges.
