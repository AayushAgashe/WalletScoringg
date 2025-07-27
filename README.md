# DeFi Wallet Risk Scoring — Compound V2

This project assigns a **risk score (0–1000)** to DeFi wallet addresses based on their activity in the **Compound V2** protocol. It simulates realistic user behavior to demonstrate the scoring pipeline in the absence of real on-chain data.

---

##  Background

The assignment required fetching transaction history for a set of wallet addresses from Aave V2/V3 or Compound V2, extracting meaningful behavioral features, and computing a risk score for each wallet.

However, **none of the provided wallet addresses had any lending or borrowing activity** on these protocols.

###  Alternate Approach

To demonstrate the working pipeline, **we generated simulated Compound V2 data** that mimics realistic user interactions like:

- Supplying assets (`mint`)
- Borrowing (`borrow`)
- Repaying (`repayBorrow`)
- Redeeming (`redeem`)

---

##  Workflow Summary

### 1. Simulated Data
Created mock Compound V2 transactions for a few wallet addresses, with timestamps, action types, and amounts.

### 2. Feature Engineering
Computed per-wallet features including:

- `mint`, `borrow`, `repayBorrow`, `redeem` totals  
- `net_balance` = mint - borrow  
- `repay_ratio` = repay / borrow  
- `liquidation_risk` = borrow / (mint + repay)  
- `total_txn` = transaction count  

### 3. Scoring
- Used `MinMaxScaler` to normalize features  
- Assigned risk scores based on a weighted sum of behaviors  
- Mapped scores to 0–1000 scale  
- Higher scores indicate low-risk, responsible behavior

---

##  Sample Output

| wallet_id                              | score |
|----------------------------------------|-------|
| 0xabc1234567890abcdef1234567890abcdef | 872   |
| 0xdef1234567890abcdef1234567890abcdef | 405   |
| 0xghi1234567890abcdef1234567890abcdef | 121   |

---

##  Important Notes

- On-chain queries via [The Graph](https://thegraph.com) returned **null or empty** responses for all real wallet addresses.
- Queries were attempted on:
  - Aave V2
  - Aave V3
  - Compound V2
- GraphQL endpoints and Playground were used for debugging and validation.

---

##  Future Improvements

- Re-run pipeline with real data if valid wallets become available  
- Extend support to other DeFi protocols like Aave, Morpho, or Venus  
- Include wallet-level behavioral clustering and anomaly detection  

---

##  Tech Stack

- Python (Pandas, Scikit-learn)
- Google Colab
- GraphQL (via The Graph)
- Simulated data for testing

---

## 📬 Contact

For any clarifications or extensions, feel free to reach out.
Mail:aayushagashe@gmail.com


