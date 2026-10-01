# Olist Revenue Model (Excel)

I built this to learn Power Query and VBA, which come up in most finance analyst and FP&A job descriptions. It was my first time using either. It uses the public [Olist Brazilian e-commerce dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce), the same data as my [SQL analysis](https://github.com/simarleenkaur17/olist_ecommerce_sql_analysis) and [Tableau dashboard](https://public.tableau.com/app/profile/simarleen.kaur8471/viz/OlistE-CommercePerformanceDashboard).

Power Query and VBA were new to me, so I used Claude (an AI assistant) to teach me each step as I built the model. It also wrote the VBA macro, which I've worked through so I can explain how it works.

<img width="1199" height="497" alt="Dashboard" src="https://github.com/user-attachments/assets/39adf818-2bc6-4788-9126-85d1506d6189" />


## What's in it

- **Data prep:** Power Query imports and joins four raw CSVs (orders, items, products, category translations) and keeps delivered orders only.
- **Automation:** A VBA macro checks data quality and writes the results to a Checks sheet. One button refreshes the data and reruns the checks.
- **Reporting:** Monthly revenue, freight and items sold in a pivot, plus a one-page KPI dashboard.
- **Forecasting:** Two methods tested against six months of actual data, with variance by month.
- **Scenarios:** worst, base and best projections for the next six months, driven by volume and price.

## Sheets

| Sheet | Purpose |
|---|---|
| Dashboard | KPIs, scenario totals, commentary and charts |
| Forecast | Monthly actuals, two forecasts and their variance |
| Scenarios | Inputs, scenario picker and six-month projection |
| Monthly_Actuals | Pivot of revenue, freight and items by month |
| Checks | Data quality results and the Refresh & Check button |
| Sales_Data | Cleaned, merged data (one row per item sold) |

## What I found

- Revenue grew quickly through 2017 and peaked at about R$988k in November 2017, probably because of Black Friday.
- In 2018 it flattened at R$840–980k a month. Jun–Aug 2018 was still 76% up on the same months in 2017.
- The trend forecast overshot Mar–Aug 2018 by 19%, and the miss got bigger every month. A 3-month average did better (10% average error) because growth had stopped.
- Next six months (Sep 2018 – Feb 2019): R$4.5m to R$6.1m, base case R$5.5m. Volume matters more than price.

## Data checks

| Check | Result |
|---|---|
| Rows | 110,197 |
| Duplicate order and item rows | 0 |
| Items with no English category | 1,559 (flagged) |
| Zero, negative or missing prices | 0 |
| Negative or missing freight | 0 |

The 1,559 items (about 1.4%) have no category, or one is missing from the translation file. They're still included in all totals.

## Limitations

- Values are in Brazilian reais (R$).
- Revenue is item price only; freight is shown separately.
- There's no cost data, so this is a revenue model, not a P&L.
- It uses Jan 2017 – Aug 2018, since the months on either side have very little data.
- There's only one November in the data, so seasonality is limited to a November uplift input.
- Scenario inputs are my own assumptions and can't be checked against actuals.

## What I'd do next

- Use the payments file to reconcile payments against item and freight totals.
- Add proper seasonality if there were more than one year of data.
- Break the forecast down by product category.

## How to use

1. Download the dataset from Kaggle and put `olist_orders_dataset.csv`, `olist_order_items_dataset.csv`, `olist_products_dataset.csv` and `product_category_name_translation.csv` in one folder.
2. Open `olist_finance_model.xlsm` in Excel for Microsoft 365 and enable macros.
3. Point each query to your folder (they currently use my file paths).
4. Click **Refresh & Check** on the Checks sheet.
5. Pick a scenario from the dropdown in B11 on the Scenarios sheet.
