# Credit Score Assignment using Aave V2 Transaction Data

## Overview

This project processes user-wallet transactions from the Aave V2 protocol to engineer features and assign credit scores. The aim is to analyze DeFi behavior and generate a trustworthiness metric (score from 0 to 1000) for each wallet.

##  Dataset

- **Source**: A JSON file containing historical user-wallet transaction data from the Aave V2 protocol.
- **Structure**: Each transaction record includes:
  - `userWallet`: Wallet address
  - `action`: Type of transaction (e.g., deposit, borrow, repay, etc.)
  - `actionData`: Contains transaction-specific fields like `amount`
  - `timestamp`, `txHash`, etc.

##  Feature Engineering

For each unique wallet, the following features are computed:

- `num_txns`: Total number of transactions
- `num_deposit`, `num_borrow`, `num_repay`, etc.: Counts of each action type
- `total_deposit`, `total_borrowed`, `total_repaid`: Summed amounts for key actions
- `repay_ratio`: Ratio of total repaid to total borrowed

##  Credit Score Logic

A rule-based scoring system could look like this:

```python
if repay_ratio >= 0.9 and total_borrowed > 0:
    score = 900
elif repay_ratio >= 0.5:
    score = 600
else:
    score = 300
