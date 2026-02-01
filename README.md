# Bank Customer Transaction & Risk Analysis (SQL + Python)

In this project, I analyzed over 6.3 million banking transactions to design and refine a rule-based risk monitoring framework using SQL and Python.

Rather than building a machine learning model, I focused on structured querying, behavioral analysis, and iterative rule refinement — similar to how transaction monitoring systems are often developed in practice.

---

## 📑 Table of Contents

- [Why I Built This Project](#why-i-built-this-project)
- [How My Analysis Evolved](#how-my-analysis-evolved)
- [Initial Risk Logic](#initial-risk-logic)
- [Refining the Logic](#refining-the-logic)
- [Customer-Level Insights](#customer-level-insights)
- [Tools Used](#tools-used)
- [What This Project Shows About My Approach](#what-this-project-shows-about-my-approach)

---

## Why I Built This Project

I wanted to simulate how transaction-level risk monitoring works using structured logic rather than predictive modeling.

My goal was to:
- Understand transaction behavior at scale
- Identify practical risk signals
- Design explainable screening rules
- Refine those rules to reduce false positives
- Translate the findings into meaningful insights

---

## How My Analysis Evolved

I began by validating the dataset and assessing its structure. After loading 6.3 million records, I evaluated transaction frequency per customer and discovered that most customers performed only one to three transactions.

That immediately influenced my direction.

Since repeat behavior was limited, frequency-based risk scoring would not provide meaningful insight. Instead, I shifted my focus to transaction-level behavior — specifically transaction size, transaction type, and balance movement.

I then analyzed transaction types and balance changes to understand which activities had the greatest financial impact. TRANSFER and CASH_OUT transactions clearly resulted in the largest balance reductions.

---

## Initial Risk Logic

I first implemented a simple rule:

High Risk:
- Transaction amount greater than 1,000,000  
- Transaction type is TRANSFER or CASH_OUT  

This flagged 130,507 transactions (approximately 2% of the dataset).

While this captured large-value activity, I recognized that high amount alone does not necessarily indicate disruptive behavior.

---

## Refining the Logic

To improve precision, I introduced balance depletion intensity into the rule.

Instead of flagging every large transfer, I classified transactions as High Risk only when they reduced the sender’s balance by more than 80%.

This refinement reduced high-risk transactions to 65,542 (about 1% of total activity), creating a more focused and behavior-driven classification.

This step significantly reduced noise and better isolated transactions that meaningfully disrupted account balances.

---

## Customer-Level Insights

After refining transaction-level logic, I aggregated exposure at the customer level.

The results showed that most high-risk exposure was driven by one-time large transactions rather than repeated risky behavior. This reinforced my earlier finding that risk in this dataset is event-driven rather than frequency-driven.

In this context, monitoring large, aggressive balance-depleting transactions is more important than tracking repeat patterns.

---

## Tools Used

- SQL (SQLite) for querying and rule implementation  
- Python (Pandas) for data manipulation  
- Matplotlib for visualization  
- Jupyter Notebook for structured analysis  

---

## What This Project Shows About My Approach

This project reflects how I approach analytical problems:

- I validate assumptions before building logic  
- I adapt when the data challenges initial expectations  
- I design explainable, structured rules  
- I refine logic to improve precision  
- I focus on translating technical analysis into clear insights  

The result is a practical, behavior-driven transaction monitoring framework built entirely with SQL and Python.
