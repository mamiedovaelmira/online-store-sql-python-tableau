# Exploratory data analysis for online store
End-to-end sales analytics for an online furniture store: data is extracted from BigQuery with SQL, explored in Python, and presented in a Tableau dashboard.

**Tools:** SQL (BigQuery), Python (pandas, matplotlib, seaborn), Google Colab, Tableau

**Link:** https://colab.research.google.com/drive/1wUSA726vSBetR9aqAk1hED0pdfZ8Dmg5?usp=sharing

## Project goals
- Extract and combine data from several tables with SQL
- Run exploratory analysis in Python: data quality, sales, users, dynamics over time
- Turn the findings into business recommendations
- Build an interactive dashboard in Tableau

## Data
Source: BigQuery project `data-analytics-mate`, dataset `DA` (training dataset from the Data Analytics course at mate.academy).

| Table | What it contains |
| :--- | :--- |
| `session` | Table containing information about user sessions. |
| `session_params` | Additional information about sessions, including devices, browser language, user's country, etc. | 
| `order` | Table of orders. Within a single session, there may be multiple purchased products. |
| `product` | A table listing the products sold on the website. |
| `account_session` | A table containing information about the sessions during which the subscription was created. |
| `account` | Table of website subscribers. A subscriber is a user who has provided their email address for communication. |

A single SQL query joins everything into one session-level table (one row per session, with product and account fields filled in where a purchase or registration happened). It is built with three CTEs (`sessions_info`, `orders_info`, `accounts_info`) and LEFT JOINs, so sessions without orders or accounts are kept.

The result contains 349545 rows.

## Analysis steps

1. **Data overview:** structure, column types, period covered, unique values
2. **Data quality:** missing values (explained by anonymous visitors and sessions without purchases), duplicates, price anomalies
3. **Sales and users:**
   - top continents, countries and product categories by orders and revenue
   - revenue share by device, mobile model and traffic source
   - share of registered users with a confirmed email
   - subscribed vs unsubscribed users: ARPU and conversion
4. **Dynamic:**  daily revenue and 7-day moving averages by continent, traffic channel and device
5. **Conclusions and recommendations**

## Key Findings
- The USA is the main market: about 43% of total revenue (~$13.9M). The geographical distribution of orders is fully correlated with revenue, so the average check is stable across the main markets.
- Dependence on one country is a risk. Europe, especially the UK and France, shows interest but brings less revenue.
- Upholstered furniture leads by revenue (sofas and armchairs, chairs, beds). The category ranking in the USA matches the global one.
- Desktop brings most of the revenue (about 59%), mobile about 39%.
- Organic search (~35.7%) and direct traffic (~26.6%) are the biggest sources of revenue.
- More than 71% of registered users confirmed their email.
- Subscribed and unsubscribed users show almost the same conversion (~10%) and ARPU, so email subscription does not seem to drive purchases.

## Recomendations
- Launch a loyalty program in the US market to move anonymous visitors to registered accounts
- Check the mobile version of the site, especially top furniture categories and the payment flow
- Develop the European direction (UK, France) to reduce dependence on the US

## Dashboard
Tableau dashboard: https://public.tableau.com/app/profile/elmira.mamiedova/viz/Onlinestoresalesanalyticsdashboard/OnlineStoreAnalysis
