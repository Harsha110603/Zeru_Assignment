# Aave V2 DeFi Wallet Credit Scoring

**Author:** SAI HARSHA VARDHAN REDDY N

---

## Overview

This project implements a pipeline to assign a **credit score (0–1000)** to each wallet address based solely on historical transaction-level data from the Aave V2 protocol.  
Scores reflect on-chain behaviors: higher means more responsible usage, lower means riskier or more exploitative patterns.

---

## Solution Architecture

- **Data Loading:**  
  Ingests raw transaction JSON with records of user actions (`deposit`, `borrow`, `repay`, `redeemunderlying`, `liquidationcall`).

- **Feature Engineering:**  
  For each wallet, computes features including:
    - **total_txns**: Total transactions (all actions)
    - **unique_actions**: Number of distinct action types
    - **total_amount_usd**: Sum of all transaction amounts in USD
    - **num_deposits**, **num_borrows**, **num_repays**, **num_redeems**, **num_liquidations**
    - **active_days**: Number of unique days of protocol usage
    - **repay_ratio**: num_repays / num_borrows (0 if no borrows)

- **Score Assignment:**  
  1. **Rule-based score:**  
     ```
     score = 500 
           + 200 * (repay_ratio)
           - 50 * (num_liquidations)
           + 0.05 * (total_amount_usd)
     ```
     - Score is clipped to 0–1000.
  2. **Random Forest Regressor:**  
     Trained on the extracted features and rule-based scores to predict a more nuanced `credit_score`.

- **Output:**  
  - `scores.csv`: wallet address and credit score.
  - Score distribution histogram.
  - Interpretation summary.

---

**Note:** The scoring system is fully transparent and extensible. Only on-chain historical data is considered (no off-chain or KYC data).

---

