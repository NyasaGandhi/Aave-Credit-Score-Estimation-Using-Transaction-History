# Project Analysis: Aave Credit Score

## Overview

This project aims to analyze user wallet transactions from the Aave V2 protocol to compute a simple credit score for each wallet. The approach focuses on understanding user behavior based on borrow, deposit, and repayment actions to infer creditworthiness.

## Dataset Description

- **File**: `user-wallet-transactions.json`
- **Format**: JSON array
- **Total records**: 3497
- **Key fields**:
  - `userWallet`: Wallet address
  - `action`: Type of action (e.g., `borrow`, `repay`, `deposit`)
  - `actionData`: Contains transaction details like `amount`
  - `timestamp`: Unix timestamp of the event

## Data Processing Steps

1. **Loaded JSON file** and parsed it into a Pandas DataFrame.
2. **Inspected and cleaned** the data:
   - Extracted numeric values from `actionData["amount"]`
   - Filtered key actions: `borrow`, `repay`, `deposit`, etc.
3. **Grouped by wallet** to extract user-level features.

## Feature Engineering

For each wallet, the following features were calculated:

| Feature           | Description                                  |
|-------------------|----------------------------------------------|
| `num_txns`        | Total number of transactions                 |
| `num_borrow`      | Number of borrow actions                     |
| `num_repay`       | Number of repayment actions                  |
| `total_borrowed`  | Total amount borrowed                        |
| `total_repaid`    | Total amount repaid                          |
| `repay_ratio`     | Total repaid / Total borrowed                |

These features were compiled into a DataFrame for further analysis.

## Scoring Logic

A simple rule-based scoring formula was applied:
score = min(1000, repay_ratio * 1000)

- A wallet that repaid 100% of what it borrowed receives a score of 1000.
- Wallets with no repayment or low repayment ratios receive lower scores.

## Score Distribution

The wallet scores were visualized using a histogram (`score_distribution.png`), showing how most wallets cluster around high or low scores, indicating strong or weak repayment behavior.

## Observations

- A significant number of wallets have **perfect repayment ratios**, suggesting responsible usage.
- Some wallets show **zero repayments** despite multiple borrow actions.
- Score distribution is **bimodal**, reflecting clear behavioral patterns.

## Insights

- Repayment ratio is a strong initial proxy for creditworthiness in DeFi.
- Borrowing behavior alone doesn't indicate risk; **repayment behavior matters more**.
- Adding metrics like time-to-repay or collateral use could enhance the model.

## Conclusion

The current system provides a foundational approach to credit scoring for DeFi wallets using Aave V2 transaction data. While simple, this method offers interpretable and actionable insights.

Future work could incorporate machine learning or deploy this model in a web app for broader access.
