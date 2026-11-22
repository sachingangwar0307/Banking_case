# Banking Customer Analytics: Portfolio Insights & Dashboard

End-to-end analysis of 3,000 bank clients using **MySQL**, **Python** and **Power BI**, covering loans, deposits, income bands, loyalty tiers and cross-sell potential.

![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?logo=mysql&logoColor=white)
![Python](https://img.shields.io/badge/Python-Pandas%20%7C%20Seaborn-3776AB?logo=python&logoColor=white)
![Power BI](https://img.shields.io/badge/Power%20BI-DAX-F2C811?logo=powerbi&logoColor=black)

![Dashboard summary](docs/screenshots/summary.png)

## Table of contents
1. [Business problem](#1-business-problem)
2. [Dataset](#2-dataset)
3. [Tools used](#3-tools-used)
4. [Approach](#4-approach)
5. [Key findings](#5-key-findings)
6. [Recommendations](#6-recommendations)
7. [Power BI dashboard](#7-power-bi-dashboard)
8. [How to run](#8-how-to-run)
9. [Repository structure](#9-repository-structure)
10. [Limitations](#10-limitations)
11. [Author](#author)

## 1. Business problem

A retail and private bank wants to know **who its clients are, how large its loan and deposit book is, and where it can grow**. This project answers three questions:

1. What does the client base look like by relationship type, loyalty tier, income band, nationality and occupation?
2. How big are loans and deposits, and how balanced is the portfolio?
3. Which client attributes are actually related to loan and deposit balances?

## 2. Dataset

| Item | Detail |
|---|---|
| Source | MySQL database `banking_case` |
| Tables | `clients` (3,000 rows, 25 columns), `gender`, `investment_advisiors`, `realtionships` (table names kept as in the database) |
| Client attributes | Age, nationality, occupation, fee structure, loyalty class, estimated income, credit cards, loans, deposits, checking and savings balances, foreign-currency account, business lending, properties owned, risk weighting |
| Lookups | Banking relationship (Retail, Institutional, Private Bank, Commercial), gender, 22 investment advisors |

## 3. Tools used

| Area | Tools |
|---|---|
| Database | MySQL |
| Analysis | Python, Pandas, NumPy, SQLAlchemy, PyMySQL |
| Visualization | Matplotlib, Seaborn, Power BI (DAX, slicers) |

## 4. Approach

1. **Load:** connected Python to MySQL with SQLAlchemy and read the four tables into DataFrames.
2. **Profile:** checked the shape (3,000 x 25), data types, summary statistics and category counts.
3. **Segment:** created income bands from `estimated_income`: **Low** (under 100,000), **Mid** (100,000 to under 300,000) and **High** (300,000 and above).
4. **Explore:** univariate and bivariate count plots (including by loyalty class), histograms with KDE for eight numeric columns, and a correlation heatmap.
5. **Visualize:** built a 4-page Power BI report on the same tables.

## 5. Key findings

| Finding | Evidence |
|---|---|
| The portfolio is slightly deposit-heavy | $1.77B bank loans vs $2.01B bank deposits (loan-to-deposit ratio about 0.88). Business lending adds $2.60B. |
| Private Bank dominates | 1,352 of 3,000 clients (45%); Retail 660 (22%), Institutional 495, Commercial 493 |
| Most clients are in the entry loyalty tier | Jade 1,331 (44%), Silver 767, Gold 585, Platinum 317 (11%) |
| Most clients hold one credit card | 1 card: 1,922 (64%); 2 cards: 765; 3 cards: 313 |
| Mid-income clients hold the most | Mid band: 53% of bank loans and 54% of deposits (Low 25% / High 22%) |
| Deposits follow balances, not income | Deposits correlate with checking (r = 0.84) and savings (r = 0.75); income is only weakly related to loans and deposits (r = 0.26 to 0.33) |
| Europe
