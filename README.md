Banking Customer Analytics: Portfolio Insights & Dashboard
> An end-to-end analysis of 3,000 bank clients: MySQL for storage, Python for profiling and statistics, and a 4-page Power BI dashboard for loans, deposits and client segments.
![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?logo=mysql&logoColor=white)
![Python](https://img.shields.io/badge/Python-Pandas%20%7C%20Seaborn-3776AB?logo=python&logoColor=white)
![Power BI](https://img.shields.io/badge/Power%20BI-DAX-F2C811?logo=powerbi&logoColor=black)
![Dashboard summary](docs/screenshots/summary.png)
1. Business problem
A retail and private bank wants to understand who its clients are, how large its loan and deposit book is, and where it can grow (upgrades and cross-sell). This project answers three questions:
What does the client base look like by relationship type, loyalty tier, income band, nationality and occupation?
How big are loans and deposits, and how balanced is the portfolio?
Which client attributes are actually related to loan and deposit balances?
2. Dataset
Item	Detail
Source	MySQL database `banking_case`
Tables	`clients` (3,000 rows, 25 columns), `gender`, `investment_advisiors`, `realtionships` (table names kept as in the database)
Client attributes	age, nationality, occupation, fee structure, loyalty class, estimated income, credit cards, loans, deposits, checking and savings balances, foreign-currency account, business lending, properties owned, risk weighting
Lookups	banking relationship (Retail, Institutional, Private Bank, Commercial), gender, 22 investment advisors
3. Tools
MySQL: data storage and lookup tables
Python: Pandas, NumPy, SQLAlchemy and PyMySQL (loading), Matplotlib and Seaborn (visuals)
Power BI: DAX measures, slicers, a 4-page report
4. Approach
Load: connected Python to MySQL with SQLAlchemy and read the four tables into DataFrames.
Profile: checked shape (3,000 x 25), data types, summary statistics and category counts.
Segment: created income bands from `estimated_income`: Low (< 100,000), Mid (100,000 to under 300,000), High (300,000 and above).
Explore: univariate and bivariate count plots (including by loyalty class), histograms with KDE for eight numeric columns, and a correlation heatmap.
Visualize: built the Power BI report on the same tables.
5. Key findings
Finding	Evidence
The book is slightly deposit-heavy	$1.77B bank loans vs $2.01B bank deposits, a loan-to-deposit ratio of about 0.88. Business lending adds $2.60B (total loans $4.37B).
Private Bank dominates the client base	1,352 of 3,000 clients (45%); Retail 660 (22%), Institutional 495, Commercial 493
Most clients sit in the entry loyalty tier	Jade 1,331 (44%), Silver 767, Gold 585, Platinum 317 (11%)
Most clients hold a single credit card	1 card: 1,922 (64%); 2 cards: 765; 3 cards: 313
Mid-income clients carry the most borrowing and deposits	Mid band: 53% of bank loans and 54% of deposits (Low 25% / High 22%)
Deposits follow account balances, not income	Deposits correlate with checking (r = 0.84) and savings (r = 0.75); income is only weakly related to loans and deposits (r = 0.26 to 0.33)
Europe is the largest nationality group	1,309 clients (44%), then Asian 754 and American 507; European clients also hold the largest loan balance ($0.78B)
6. Recommendations
Upgrade campaigns: target Jade and Silver clients with balances close to the next tier, since Platinum is only 11% of the base.
Cross-sell cards: two-thirds of clients hold one card, so a second-card offer is the simplest test.
Lending capacity: deposits exceed loans, so test lending offers for deposit-rich clients.
Segment by balances, not income: income explains little of the loan and deposit variation, so balance-based segments are likely to be more useful.
7. Power BI dashboard
Page	What it shows
Home	Navigation, joining-year and gender filters, headline loan and deposit cards
Loan Analysis	Total loans, bank loans, business lending, card balance; loans by relationship, income band, nationality and top-10 occupations
Deposit Analysis	Total deposits, savings, bank deposits; the same breakdowns for deposits
Summary	All KPIs, loyalty-class split of loans, client count by relationship type
All pages have slicers for banking relationship, gender, investment advisor and joining year. Open `powerbi/Banking_customer_dashboard.pbix` in Power BI Desktop.
![Loan analysis](docs/screenshots/loan-analysis.png)
![Deposit analysis](docs/screenshots/deposit-analysis.png)
8. Run it yourself
```bash
git clone https://github.com/sachingangwar0307/banking-customer-analytics.git
cd banking-customer-analytics
pip install -r requirements.txt

# set your own database credentials (see .env.example)
export DB_PASSWORD="your_password"   # Windows PowerShell: $env:DB_PASSWORD="your_password"
jupyter notebook notebooks/banking_customer_analytics.ipynb
```
You need a local MySQL server with the `banking_case` database and the four tables above.
9. Repository structure
```
banking-customer-analytics/
├── notebooks/banking_customer_analytics.ipynb   # loading, EDA, correlations
├── powerbi/Banking_customer_dashboard.pbix      # 4-page Power BI report
├── docs/screenshots/                            # dashboard images
├── requirements.txt
├── .env.example
└── README.md
```
10. Limitations
The dataset is a single snapshot, so the analysis shows no trend over time.
Correlation does not imply causation.
Dashboard figures were read from the Power BI report with no filters applied.
The `joined_bank` column holds zero dates (`0000-00-00`) in the MySQL rows I inspected, so check it before building any time-based analysis.
Author
Sachin Gangwar, aspiring Data Analyst
LinkedIn · GitHub · sachingangwar0307@gmail.com
