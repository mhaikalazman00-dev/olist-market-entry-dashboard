# Olist Market Research Dashboard (Power BI)

A market research dashboard built in Power BI from the Olist Brazilian e-commerce dataset on Kaggle. It helps sellers assess product marketability by looking at demand, pricing, geography, and market saturation.

![Dashboard preview](images/dashboard.png)
<!-- Replace with a screenshot of your dashboard -->

## Background

Olist is a Brazilian software-as-a-service provider that helps small businesses manage stock across multiple sales channels. For example, if a seller has five refrigerators listed on eBay, Amazon, and Shopee, a sale on one channel updates the stock everywhere so inventory is not mismanaged. The dataset also reflects a logistics component, including a suggested shipping limit date for sellers.

Product IDs and seller IDs in the dataset are hashed for privacy, so the actual products and sellers are unknown.

## Project Scope and Design Decisions

After reviewing the data, I chose to build a **market research dashboard** rather than a typical corporate performance dashboard, for three reasons:

1. **No revenue tracking.** Olist does not earn commission on sales, so sales revenue would be a vanity metric for the company. Revenue is deliberately left out.
2. **Hashed product IDs limit product-level insight.** They are still useful for analyzing price distribution per product and per category, so they are used for that purpose only.
3. **No seller performance tracking.** Even though hashed seller IDs would technically allow it, tracking individual sellers would breach the confidentiality expected between a service provider and its clients. Olist also offers no consulting services that would make use of such insights.

## Dashboard Features

- **Sales trends:** average products sold per month and total quantity sold per month.
- **Price distribution:** box plot (built as a pseudo box plot, since Power BI has no dedicated native box plot visual) by product ID and by category.
- **Geospatial popularity:** popularity of categories and products across Brazilian states, shown on a filled map.
- **Market saturation:** number of sellers per product ID and per category, to show how crowded each market is.

## Data Cleaning and Preparation

1. **Split the order purchase timestamp into date and time columns.** The purchase time is still valuable, but Power BI requires a pure date column to build a date table. Separating the original timestamp into a date column and a time column solves this while preserving both.
2. **Mapped state abbreviations to full state names.** The customers table only contained state abbreviations (e.g. `SP`), which Power BI's native filled map failed to recognize. Using Python, I merged in a CSV of Brazilian states and their abbreviations, then stripped accents and diacritics from the state names using Python's `unicodedata` module, since the map visual requires plain characters. This added a new state name feature to the customers table.

## Tools Used

- Power BI
- Python (data cleaning)
- Kaggle (data source)

## Future Improvements

Track additional variables to better help people assess product marketability from the current market research.

## Data Source

[Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) on Kaggle.
