# Analysis of Wallet Credit Scores

## Score Distribution

The following table summarizes how wallet credit scores are distributed in this dataset:

| Score Range | Number of Wallets | % of Total |
| ----------- | ---------------- | ---------- |
| [400, 500)  | 2                | 0.06%      |
| [500, 600)  | 653              | 18.67%     |
| [600, 700)  | 36               | 1.03%      |
| [700, 800)  | 28               | 0.80%      |
| [800, 900)  | 7                | 0.20%      |
| [900, 1000) | 15               | 0.43%      |

**Interpretation:**  
- The **majority of wallets** cluster in the 500–600 range, showing average or moderate usage.
- A very small number of wallets achieve either very low or very high scores.
- This distribution indicates that, under the current features and scoring logic, most users are seen as neither extremely risky nor extremely reliable.

**Score Distribution Visualization:**  
(You can include your histogram plot here, e.g. by screenshot or image if required.)

---

## Behavioral Analysis by Score Range

### 1. **[900, 1000): High-Scoring Wallets**
- These wallets have **no liquidations** and a **repay ratio of 0**.
- Most did not participate in risky actions or perhaps were simply not very active.
- Current logic rewards "no risk" as much as responsible active usage.

### 2. **[500, 600): Most Common Wallets**
- These accounts likely had some activity but did not repay or get liquidated.
- Many wallets may have only deposited or made simple, low-risk transactions.

### 3. **[400, 500): Lowest Scores**
- Wallets here experienced multiple liquidations and no repayments.
- Represents high-risk or failed usage, such as borrowing with no intention (or ability) to repay.

---

## Top 5 Wallets (By Credit Score)

| Wallet Address                                  | Credit Score | Repay Ratio | Liquidations |
|-------------------------------------------------|--------------|-------------|--------------|
| 0x02f21b7c148d5fc587a285d2f538f29c36176e52      | 1000         | 0.0         | 0            |
| 0x03e03279f11cfca9f44bcfdb41d767af0e71a1a6      | 1000         | 0.0         | 0            |
| 0x03aad34b8d729c000e980d676b5012ce024e6ba4      | 1000         | 0.0         | 0            |
| 0x03ab5739cf27680d40bdfa8778a63a9239badc40      | 1000         | 0.0         | 0            |
| 0x03abec9490d905b2e93c469e7f7409b085bfff8a      | 1000         | 0.0         | 0            |

**Observation:**  
- All top wallets did not get liquidated or repay (probably just deposited).
- High score is assigned for not engaging in any risky activity.

---

## Bottom 5 Wallets (By Credit Score)

| Wallet Address                                  | Credit Score | Repay Ratio | Liquidations |
|-------------------------------------------------|--------------|-------------|--------------|
| 0x003be39433bde975b12411fbc3025d49d813a84f      | 408          | 0.0         | 3            |
| 0x02e2b3f9e177e918e67e25b1a1b6a739049f9e22      | 483          | 0.0         | 0            |
| 0x0198d8a7463819a22facc2b96a7402f1bbbd1a82      | 500          | 0.0         | 0            |
| 0x0486b904c347c7794e70a37c8d53a67b64b38b5f      | 500          | 0.0         | 0            |
| 0x0488456ea17ec42ad21df20efb4a35a37d710064      | 500          | 0.0         | 0            |

**Observation:**  
- The lowest wallet score is due to three liquidations and no repayments.
- Others have no repayments or liquidations—likely low activity, but not as severely penalized.

---

## Insights

- **Majority of users** display moderate protocol usage and risk, thus scoring in the middle.
- **Very high scores** are mostly for inactive or low-risk users (possibly a limitation of current feature set).
- **Low scores** are strongly correlated with liquidation events and absence of repayment.
- **Repay ratio** is 0 for all top and bottom wallets, highlighting the importance of activity type over volume.

**Recommendation:**  
- To improve, future models should differentiate between "good inactivity" and "good active usage" (e.g., borrowing and successfully repaying).
- More features, such as transaction timing or diversity, could improve discrimination.

---

*See the notebook for code, full feature definitions, and score calculation details.*
