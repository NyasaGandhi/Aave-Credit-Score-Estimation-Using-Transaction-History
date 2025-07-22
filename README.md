# Credit Score Assignment using Aave V2 Transaction Data

# Aave Credit Score
This project analyzes on-chain wallet transactions from the Aave V2 protocol to assign a credit score (0–1000) to each user wallet based on borrowing and repayment behavior.

## Objective
To build a lightweight credit scoring model using rule-based logic and historical DeFi transaction data. The goal is to evaluate wallet trustworthiness for potential use in DeFi credit risk assessment.

## Project Structure
aave_credit_score/
├── user-wallet-transactions.json # Raw transaction data
├── Untitled.ipynb # Main notebook with feature extraction & scoring
├── wallet_credit_scores.xlsx # Final wallet scores
├── score_distribution.png # Score distribution visualization
├── analysis.md # Project analysis and explanation

## Features Engineered

For each wallet:
- Total number of transactions
- Number of borrows & total borrowed amount
- Number of repayments & total repaid amount
- Repayment ratio (repaid/borrowed)
- Custom score calculated based on these features

## Scoring Logic

The credit score is based on a simple rule-based formula:
- High repayment ratio
- Higher total repaid amounts
- More consistent borrowing behavior

Scores range from **0 (poor)** to **1000 (excellent)**.

## Output

- Wallet-level scores saved in `wallet_credit_scores.xlsx`
- Score distribution graph: `score_distribution.png`

##  Tech Stack

- Python (Pandas, Matplotlib)
- Jupyter Notebook
- JSON for data handling
- Excel for output export

## Future Work
- Integrate ML-based scoring
- Deploy as a Streamlit app
- Add support for multiple DeFi protocols

## Author
Nyasa Gandhi
