# Olist E-Commerce Sales Dashboard

![Dashboard Preview](dashboard_preview.png)

> **An end-to-end Power BI analytics project** — from raw data to business insight — built on 100K+ real Brazilian e-commerce transactions.

📥 **[Download Power BI Dashboard](https://drive.google.com/file/d/1FiCK6kPaWH7Pj3_F7sY09O43qHP1NcT-/view?usp=share_link)**

---

## What This Project Does

This dashboard gives a business analyst or executive a complete picture of Olist's e-commerce performance at a glance — with the ability to drill into any region or time period interactively. It answers three core business questions:

- **Where is revenue coming from?** — broken down by state and region
- **What is selling?** — top 10 product categories by revenue
- **How is the business trending?** — revenue growth from launch through 2018

---

## Results at a Glance

| KPI | Value |
|---|---|
| Total Revenue | R$ 16.0M |
| Total Orders | 99K |
| Average Order Value | R$ 161 |
| São Paulo revenue share | ~37% |
| Top product category | Beleza & Saúde (R$1.26M) |

---

## Dashboard Features

### Visualisations
- **Revenue trend (2016–2018)** — line chart tracking growth from Olist's launch through peak revenue, with an annotation explaining the partial 2016 data
- **Revenue by state (top 10)** — horizontal bar chart with data labels, filtered to the top 10 states by revenue
- **Revenue by product category (top 10)** — full-width bar chart revealing which categories drive the most value

### Interactive filters
- **State dropdown** — filter every visual by customer state simultaneously

---

## Key Business Insights

**São Paulo is the dominant market.** SP generates R$6.0M — 37% of total revenue — more than the next three states combined. Any growth strategy should prioritise retention in SP while investing in acquisition in high-growth states like MG and RS.

**Revenue grew rapidly but shows signs of plateauing.** The business scaled strongly from launch in September 2016 through mid-2018. The flattening curve toward 2018 suggests the business may be approaching market saturation in its core regions — worth investigating further.

**Health, beauty and lifestyle dominate sales.** The top 5 categories — beauty & health, watches & gifts, bed & bath, sports & leisure, and computer accessories — together account for the majority of category revenue. Electronics have a smaller footprint than expected for an e-commerce platform.

**Note:** Product category names are displayed in Portuguese as provided in the original Olist dataset.

---

## Technical Build

### Data model
Star schema connecting 6 tables across 100K+ rows:

```
olist_orders_dataset          — core order facts
olist_order_items_dataset     — line items, price, freight
olist_order_payments_dataset  — payment values and methods
olist_customers_dataset       — customer location data
olist_products_dataset        — product categories
olist_sellers_dataset         — seller location data
```

Relationships defined on `order_id`, `customer_id`, `product_id`, and `seller_id`.

### DAX measures written from scratch

```dax
Total Revenue (R$) =
    SUM(olist_order_payments_dataset[payment_value])

Total Orders =
    COUNTROWS(olist_orders_dataset)

AOV =
    DIVIDE([Total Revenue (R$)], [Total Orders], 0)

SP Share % =
    DIVIDE(
        CALCULATE(
            SUM(olist_order_payments_dataset[payment_value]),
            olist_customers_dataset[customer_state] = "SP"
        ),
        SUM(olist_order_payments_dataset[payment_value]),
        0
    )

On Time Delivery % =
    DIVIDE(
        COUNTROWS(
            FILTER(olist_orders_dataset,
                olist_orders_dataset[order_delivered_customer_date] <=
                olist_orders_dataset[order_estimated_delivery_date]
            )
        ),
        COUNTROWS(olist_orders_dataset),
        0
    )

Avg Review Score =
    AVERAGE(olist_order_reviews_dataset[review_score])
```

---

## Skills Demonstrated

| Skill | Application |
|---|---|
| Data modelling | Built star schema with 6 related tables and defined all relationships |
| DAX | Wrote 6 measures including CALCULATE, DIVIDE, FILTER, and COUNTROWS |
| Data visualisation | Designed clean, consistent dashboard with professional formatting |
| Business analysis | Translated raw data into actionable insights with real numbers |
| Attention to detail | Annotated partial 2016 data, applied Top N filters, consistent colour palette |

---

## How to Open

1. Download the `.pbix` file using the link at the top of this page
2. Open in **Power BI Desktop** — free at [powerbi.microsoft.com](https://powerbi.microsoft.com)
3. Use the **state dropdown** to explore regional performance
4. Use the **date slicer** to isolate time periods
5. Click any bar or data point to cross-filter all visuals instantly

---

## Dataset

**Source:** [Olist Brazilian E-Commerce — Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
**Period:** September 2016 – August 2018
**Scale:** ~100K orders across 27 Brazilian states
**License:** CC BY-NC-SA 4.0

---

## About

Built by **Nadir Calin** as part of a data analyst portfolio.

This project demonstrates the full analyst workflow — data modelling, measure creation, visual design, and business storytelling — using a real-world public dataset.

[![LinkedIn](https://img.shields.io/badge/Connect-LinkedIn-blue)](https://www.linkedin.com/in/nadircalin/?skipRedirect=true)
