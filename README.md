# American Express: Cardmember Profitability & Customer Lifetime Value (CLV) Analysis

> **A practical, end-to-end Data Analytics case study on 500,000 credit card accounts to model cardmember unit economics, isolate perk gaming arbitrage, and rank order customer profitability.**

---

## 1. What We Built

In ultra-premium credit card portfolios (such as American Express Platinum/Premier), **gross spending volume does not directly equate to net issuer profit**.

A cardmember who spends \$50,000 exclusively on 5x points travel categories, claims all \$640+ in annual credits (airline fee credits, Uber, digital entertainment), and pays their bill in full each month operates at a **negative gross margin** for the bank (a *"Perk Gamer"*). Conversely, a moderate spender who carries low-risk revolving balances generates substantial Net Interest Income (NII) at ~20% annual margin.

We built an end-to-end data analytics framework that:
1. Audits and cleans transactional event logs using banking data warehousing principles.
2. Formulates an axiomatic credit card **P&L Statement** ($\text{Revenue} - \text{Direct Costs} - \text{Expected Credit Loss} - \text{Delinquency Friction}$).
3. Segments customers into distinct behavioral cohorts (Prime Revolvers, Premier Transactors, Perk Gamers, and Delinquent accounts).
4. Stratifies 500,000 cardmembers into profitability deciles to identify the **Top 20% most profitable cohort**.

---

## 2. Methodology & Key Results

### Financial P&L Formulation
$$\text{Net Profitability} = \text{Gross Revenue} - \text{Direct Benefit Costs} - \text{Expected Credit Loss} - \text{Delinquency Penalties}$$
* **Net Interest Income (NII)**: $0.20 \times f1$ (Revolve Balance).
* **Interchange Revenue**: $0.027 \times f5$ (Total Spend).
* **Expected Credit Loss (Basel II / IFRS 9)**: $\text{PD} \times \text{EAD} \times \text{LGD} = f11 \times \max(f17, f1) \times 0.85$.
* **Rewards Cash Liability**: $\$0.012 \times f21$ (Points Redeemed).

### Empirical Lift Results (Top 20% vs. Bottom 20%)

| Financial Indicator | Top 20% (Profitable Cohort) | Bottom 20% (Unprofitable Cohort) | Lift / Reduction |
| :--- | :--- | :--- | :--- |
| **Average Revolve Balance ($f1$)** | **\$7,637.33** | \$674.77 | **11.32x Lift in Interest Revenue** |
| **Annual Spend Volume ($f5$)** | **\$4,919.17** | \$1,589.81 | **3.09x Lift in Transaction Spend** |
| **Airlines & Lodging Spend ($f6, f9$)** | **\$15,131.82** | \$4,471.14 | **3.38x Lift in Travel Engagement** |
| **Collection Call Rate ($f3$)** | **0.41%** | 28.04% | **68x Reduction in Bad Debt** |
| **Average Risk Score ($f11$)** | **0.0183** | 0.0655 | **72% Lower Default Risk** |
| **Average Net Contribution** | **+\$2,276.65** | -\$674.16 | **Significant Margin Spread** |

![Decile Lift Chart](images/decile_lift_chart.png)

---

## 3. Technical Decisions & Business Choices

1. **Why Impute Transaction Activity with \$0 Instead of Mean/Median?**
   - In left-joined data warehousing, a `NULL` indicates zero transaction records (hence \$0 expense/revenue for the issuer). Imputing usage with the mean would falsely penalize customers who saved their perks.
2. **Why Universal Unit Economics Instead of Black-Box Machine Learning?**
   - Ground-truth profitability labels were not provided for supervised training. P&L unit economics is transparent, auditable, and directly grounded in banking accounting standards.
3. **Basel II / IFRS 9 Credit Risk Integration**:
   - Rather than treating risk scores as arbitrary penalties, we modeled Expected Loss as $	ext{PD} 	imes 	ext{EAD} 	imes 	ext{LGD}$ with an 85% loss given default benchmark for unsecured credit.

![Customer Cohort Matrix](images/customer_cohort_matrix.png)

---

## 4. Prescriptive Business Strategy Matrix

| Cardmember Cohort | Portfolio Decile | Strategic Action & Policy Recommendation |
| :--- | :--- | :--- |
| **Prime Revolvers** | Deciles 9–10 (Top 20%) | Proactive Credit Line Increases (PCLI) and Pay-Over-Time promotional APR offers. |
| **Premier Transactors** | Deciles 8–10 (Top 20%) | Bespoke transfer partner bonuses and priority annual fee retention incentives. |
| **Perk Gamers** | Deciles 3–5 (Mid Portfolio) | Dynamic point redemption minimums and category multiplier restructuring on low-margin spend. |
| **Distressed Accounts** | Deciles 1–2 (Bottom 20%) | Restrict credit lines and freeze overdraft capacity; route to early loss mitigation. |

---
