# Brazilian E-Commerce Analytics & Business Optimization (Olist Dataset)

## Executive Summary

This project analyzes over **100,000 orders** placed between 2016 and 2018 on **Olist**, Brazil's largest marketplace department store. By joining 11 relational datasets, this analysis evaluates customer purchase patterns, revenue growth, delivery bottlenecks, and customer satisfaction drivers.

### Data Sources
- **Olist Dataset:** [Olist Brazilian E-Commerce Dataset on Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) - Anonymized commercial data representing over 100,000 real-world orders.
- **Translated Reviews Dataset:** [Olist Order Reviews Translated on Kaggle](https://www.kaggle.com/datasets/pavelgrigoryev/olist-order-reviews-translated) - English translations of the Portuguese customer reviews.
- **Brazilian Geospatial Data:** [Brazil States GeoJSON](https://raw.githubusercontent.com/codeforamerica/click_that_hood/master/public/data/brazil-states.geojson).

### Key Objectives
- Analyze monthly order volumes and revenue trajectories.
- Evaluate the impact of peak promotional events, such as **Black Friday**.
- Identify high-performing product categories driving the majority of platform revenue.
- Map the geographic distribution of customers and sellers to identify logistical gaps.
- Understand payment preferences and installment behaviors.
- Investigate the root causes of negative customer reviews and delivery failures.

---

## Technical Stack & Tools

- **Microsoft Excel:** Interactive dashboards and dynamic pivot tables.
- **Python (Pandas & NumPy):** Data cleaning, timestamp conversion, multi-table joins, and feature engineering.
- **Large Language Models (`agno` & Groq API):** Automated English translation pipeline for Portuguese customer reviews.
- **Visualization & Text Analytics:** Pareto charts, geographic distribution plots, heatmaps, N-gram distributions, and multi-language word clouds.

---

## Data Architecture & Engineering

The raw dataset spans **11 CSV files** connected via primary and foreign keys (e.g., `order_id`, `customer_id`). A structured data pipeline was developed to aggregate and model the data accurately without row duplication.

<div align="center">
  <img src="./Chart/Database_schema.png" alt="Database Schema" width="90%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure: Olist Relational Database Schema across all 11 tables.</em></p>
</div>

### Data Preparation Steps
1. **Payment Aggregation:** Grouped multiple payment records per order into a single, consolidated payment row.
2. **Review Consolidation:** Merged distinct review scores and text comments into a unified review record per order.
3. **Category Translation:** Mapped original Portuguese category names (`beleza_saude`) to English equivalents (`health_beauty`).
4. **Feature Engineering:** Extracted actionable metrics including `Purchase Hour`, `Shipping Days`, and `Delivery Delay`.
5. **Master Datasets:** Constructed an **Item Master** (item-level) and an **Order Master** (order-level) for streamlined analysis.

---

## Business Insights & Visual Analytics

### 1. Revenue & Order Growth Trends

<div align="center">
  <img src="./Chart/Acquisition_Trend.png" alt="Customer Acquisition Trend" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 1: Customer Acquisition & Onboarding Trajectory Over Time.</em></p>
</div>

<div align="center">
  <img src="./Chart/Customer_Order_Distribution.png" alt="Customer Order Distribution" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 2: Customer Order Frequency & Order Count Distribution.</em></p>
</div>

<div align="center">
  <img src="./Chart/Revenue_and_Freight_over_time.png" alt="Revenue and Freight Over Time" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 3: Revenue & Freight Cost Comparison Over Time.</em></p>
</div>

<div align="center">
  <img src="./Chart/Revenue_trend.png" alt="Monthly Revenue Trend" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 4: Monthly Revenue Trend (September 2016 to August 2018).</em></p>
</div>

<div align="center">
  <img src="./Chart/Order_each_month.png" alt="Numbers of Order in Each Month" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 5: Monthly Order Volume Trajectory.</em></p>
</div>

#### Key Findings
- **Rapid 2017 Expansion:** Order volumes grew steadily quarter-over-quarter throughout 2017 as marketplace adoption expanded.
- **Black Friday Peak:** **November 2017** set an all-time record, crossing **BRL 1,000,000 in revenue** and **7,200 orders** in a single month.
- **Customer Acquisition:** New user onboarding climbed sharply in 2017 before settling into a predictable monthly baseline in 2018.
- **Customer Retention Opportunity:** Over **90% of customers made only one purchase**, pointing to a major opportunity for retention and loyalty campaigns.
- **Freight & Revenue Alignment:** Total freight spend moved in lockstep with gross sales, indicating stable shipping rates over the period.
- **Volume Plateau:** By 2018, platform demand matured at a steady run rate of **6,000 to 7,000 orders per month**.

---

### 2. Purchase Seasonality & Temporal Heatmaps

<div align="center">
  <img src="./Chart/Seasonality_Heatmap.png" alt="Category Seasonality Heatmap" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 6: Top 20 Product Categories Monthly Demand Seasonality Heatmap.</em></p>
</div>

<div align="center">
  <img src="./Chart/Nov2017_timeline.png" alt="Purchase Timeline of Nov 2017" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 7: Day-and-Hour Purchase Heatmap for November 2017.</em></p>
</div>

#### Key Findings
- **Peak Shopping Hours:** On **Black Friday** (November 24th), shopping activity stayed intense throughout the day, running strong from **10:00 AM to 11:00 PM**.
- **Category-Specific Seasonality:**
  - **Q4 Holiday Demand:** Orders for **Toys** more than doubled in November (485 orders) and December (436 orders) compared to Q1. **Garden Tools** also experienced a notable Q4 surge in November.
  - **Early-Year Tech Spending:** **Computers & Accessories** peaked early in the year (crossing 1,000 orders in February), matching post-holiday upgrades and company IT refresh cycles.
  - **Mid-Year Everyday Goods:** **Bed, Bath & Table** and **Health & Beauty** provided steady baseline volume year-round, peaking between May and August.
- **Data Coverage Note:** Lower total numbers in September and October are due to dataset cutoff dates (the dataset ends in August 2018, meaning those two months are only represented in 2017).
- **Inventory Planning:** Sellers in seasonal categories (Toys, Gifts) should stock up 60 days before November, while everyday home and beauty categories require steady safety stock through mid-year.

---

### 3. Product Performance & Market Basket Analysis

<div align="center">
  <img src="./Chart/Co-occurrence Matrix.png" alt="Co-occurrence Matrix" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 8: Product Category Co-occurrence Heatmap Matrix.</em></p>
</div>

<div align="center">
  <img src="./Chart/Category_analysis.png" alt="Category Analysis Breakdown" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 9: Product Category Performance & Distribution Analysis.</em></p>
</div>

<div align="center">
  <img src="./Chart/Basket_Analysis.png" alt="Market Basket Analysis" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 10: Market Basket & Co-Purchasing Association Analysis.</em></p>
</div>

<div align="center">
  <img src="./Chart/pareto_analysis.png" alt="Pareto Analysis" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 11: Pareto Cumulative Contribution Analysis.</em></p>
</div>

<div align="center">
  <img src="./Chart/Product_by_revenue.png" alt="Product by Revenue" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 12: Products by Revenue.</em></p>
</div>

<div align="center">
  <img src="./Chart/Revenue_by_product_category.png" alt="Revenue by Product Category" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 13: Top 10 Product Categories by Revenue.</em></p>
</div>

#### Top Category Co-occurrence Pairings

| Category 1 | Category 2 | Co-occurrence Count |
| :--- | :--- | :---: |
| `furniture_decor` | `bed_bath_table` | **70** |
| `bed_bath_table` | `home_confort` | **43** |
| `furniture_decor` | `housewares` | **24** |
| `housewares` | `bed_bath_table` | **20** |
| `cool_stuff` | `baby` | **20** |
| `toys` | `baby` | **19** |
| `garden_tools` | `furniture_decor` | **17** |
| `baby` | `bed_bath_table` | **17** |

#### Key Findings
- **Top Revenue Drivers:** **Health & Beauty** generated the most revenue (>BRL 1.2M), followed closely by **Watches & Gifts** and **Bed, Bath & Table**.
- **Pareto Principle in Action:** Out of more than 70 product categories, just **17 categories generate 80% of total revenue**.
- **Cross-Category Buying Habits:** The strongest co-purchasing happens within Home Improvement, especially **Furniture & Decor** alongside **Bed, Bath & Table**. A secondary cluster appears around **Baby, Toys, and Cool Stuff**.
- **Merchandising Opportunity:** Adding "Frequently Bought Together" recommendations and multi-item bundle discounts (such as nursery packs or bedroom sets) can directly lift Average Order Value (AOV).

---

### 4. Delivery Performance & Customer Ratings

<div align="center">
  <img src="./Chart/State_Pairwise_logistic_analysis.png" alt="State Pair-wise Logistic Analysis" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 14: State Pair-wise Logistics Heatmap.</em></p>
</div>

<div align="center">
  <img src="./Chart/State_Pairwise_Freight_analysis.png" alt="State Pair-wise Freight Analysis" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 15: State Pair-wise Freight Heatmap.</em></p>
</div>

<div align="center">
  <img src="./Chart/Top_city_pairs.png" alt="Top City Pairs Logistics Performance" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 16: Top City Pairs Delivery Analysis.</em></p>
</div>

<div align="center">
  <img src="./Chart/Mean_delivery_days_by_customer_state.png" alt="Mean Delivery Days by Customer State" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 17: Mean Delivery Days by Customer State.</em></p>
</div>

<div align="center">
  <img src="./Chart/Late_deliveries_by_state.png" alt="Late Deliveries by State" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 18: Late Deliveries Distribution by Customer State.</em></p>
</div>

<div align="center">
  <img src="./Chart/Mean_freight_by_customer_state.png" alt="Mean Freight by Customer State" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 19: Mean Freight by Customer State.</em></p>
</div>

<div align="center">
  <img src="./Chart/Intrastate_and_Interstate.png" alt="Intrastate vs Interstate Delivery" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 20: Intrastate vs. Interstate Logistic Performance.</em></p>
</div>

<div align="center">
  <img src="./Chart/delivery_performance.png" alt="Monthly Delivery Performance" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 21: Monthly Delivery Performance against Estimated Deadlines.</em></p>
</div>

<div align="center">
  <img src="./Chart/Non_Delivered_Order_Value.png" alt="Non Delivered Order Value" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 22: Financial Impact of Undelivered & Canceled Orders Over Time.</em></p>
</div>

<div align="center">
  <img src="./Chart/review_score_distribution.png" alt="Distribution of Review Score" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 23: Review Score Distribution.</em></p>
</div>

<div align="center">
  <img src="./Chart/Late_delivery_percentage_by_review_score.png" alt="Late Delivery Percentage by Review Score" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 24: Late Delivery Percentage by Review Score.</em></p>
</div>

#### Key Findings
- **On-Time Delivery Rate:** Platform logistics performed reliably overall, with **95% of orders delivered on or before the promised deadline**.
- **Impact of Lost & Canceled Orders:** Tracking canceled and lost-in-transit shipments is essential, as these directly erode GMV and increase support overhead.
- **Customer Sentiment:** Feedback is mostly positive, with **77% of all reviews giving 4 or 5 stars**.
- **Root Cause of 1-Star Reviews:** Detailed analysis shows that 1-star ratings are primarily driven by **prolonged delivery delays, unfulfilled orders, damaged goods, or items that did not match catalog descriptions**.
- **Regional Delivery & Freight Differences:** Shipping times and freight costs vary significantly by state. Interstate deliveries take longer and cost more than local intrastate fulfillment. Strategic routing and regional stocking can help reduce these delays.

<div align="center">

#### Logistics & Goods Price Correlation Matrix
*Note: Only single-seller orders are considered for this correlation matrix.*

| Metric | Goods Price | Freight | Weight | Distance | Delivery Days |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Goods Price** | 1.000000 | 0.409327 | 0.348810 | 0.080238 | 0.057668 |
| **Freight** | 0.409327 | 1.000000 | 0.642533 | 0.320452 | 0.174836 |
| **Weight** | 0.348810 | 0.642533 | 1.000000 | -0.009669 | 0.074625 |
| **Distance** | 0.080238 | 0.320452 | -0.009669 | 1.000000 | 0.393387 |
| **Delivery Days** | 0.057668 | 0.174836 | 0.074625 | 0.393387 | 1.000000 |

</div>

**Correlation Matrix Findings:**
- **Weight Drives Freight Costs:** The strongest correlation in the matrix is between `Freight` and `Weight` (0.642), much higher than `Freight` and `Distance` (0.320). Physical package weight affects shipping prices far more than the delivery distance.
- **Delivery Time Factors:** `Distance` has a moderate correlation with `Delivery Days` (0.393), which is expected. However, `Delivery Days` is virtually uncorrelated with `Goods Price` (0.057) and `Weight` (0.074). This confirms that delivery delays are operational logistics bottlenecks rather than issues tied to item value or package size.

---

### 5. Geographic Supply & Demand

<div align="center">
  <img src="./Chart/Revenue_by_state.png" alt="Revenue by State" width="45%" style="border-radius: 8px; margin-right: 2%; margin-bottom: 15px;" />
  <img src="./Chart/Orders_by_state.png" alt="Orders by State" width="45%" style="border-radius: 8px; margin-bottom: 15px;" />
  <br>
  <img src="./Chart/Customer_by_state.png" alt="Customer by State" width="45%" style="border-radius: 8px; margin-right: 2%; margin-bottom: 15px;" />
  <img src="./Chart/Seller_by_state.png" alt="Seller by State" width="45%" style="border-radius: 8px; margin-bottom: 15px;" />
  <br>
  <img src="./Chart/AOV_by_state.png" alt="AOV by State" width="45%" style="border-radius: 8px; margin-right: 2%; margin-bottom: 15px;" />
  <img src="./Chart/ARPU_by_state.png" alt="ARPU by State" width="45%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 25: Geographic Distribution of Key Metrics (Revenue, Orders, Customers, Sellers, AOV, ARPU) across Brazilian States.</em></p>
</div>

<div align="center">
  <img src="./Chart/Brazil_coordinates.png" alt="Brazil Map Coordinates" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 26: Geographic Plot of Brazilian Coordinates.</em></p>
</div>

<div align="center">
  <img src="./Chart/South_america.png" alt="South America Regional Map" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 27: South America Regional Geographic Map.</em></p>
</div>

<div align="center">
  <img src="./Chart/Top-10_state_by_customer.png" alt="Top 10 States based on Customer and Seller" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 28: Customer vs. Seller Distribution by State.</em></p>
</div>

<div align="center">
  <img src="./Chart/Revenue_by_top10_state.png" alt="Revenue Generation of Top-10 State" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 29: Revenue Contribution by Top 10 States.</em></p>
</div>

<div align="center">
  <img src="./Chart/Orders_by_seller_state.png" alt="Orders by Seller State" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 30: Orders by Seller State.</em></p>
</div>

<div align="center">
  <img src="./Chart/Orders_per_seller_by_state.png" alt="Orders per Seller by State" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 31: Average Orders per Seller by State.</em></p>
</div>

#### Key Findings
- **São Paulo Market Dominance:** The state of **SP** accounts for **38% of total revenue**, **42% of the customer base**, and **60% of all registered sellers**.
- **Regional Supply Imbalances:** States like **Rio de Janeiro (RJ)** and **Minas Gerais (MG)** show strong buyer demand but lack local seller representation.
- **Logistics Recommendation:** Heavy reliance on São Paulo sellers drives up freight costs and extends shipping times for RJ and MG buyers. Opening regional cross-docking hubs in these states would reduce shipping fees and improve delivery times.

---

### 6. Seller Economics & Fulfillment Analytics

<div align="center">
  <img src="./Chart/Seller_Order_Analysis.png" alt="Seller Order Volume Analysis" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 32: Seller Order Volume & Revenue Performance Distribution.</em></p>
</div>

<div align="center">
  <img src="./Chart/Seller_analysis.png" alt="Seller Fulfillment Analysis" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 33: Seller Fulfillment Distribution & Order Status Breakdown.</em></p>
</div>

#### Top 5 Sellers by Gross Revenue & Order Fulfillment Breakdown

| Rank | Seller ID | Revenue (BRL) | Orders | AOV (BRL) | Delivered | Shipped | Canceled | Invoiced / Processing |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **1** | `4869f7a5dfa277a7dca6462dcf3b52b2` | **229,473** | 1,132 | **202.71** | **1,124** | 7 | 1 | 0 |
| **2** | `53243585a1d6dc2643021fd1853d8905` | **222,776** | 358 | **622.28** | **348** | 4 | 0 | 6 (5 inv, 1 proc) |
| **3** | `4a3ca9315b744ce9f8e9374361493884` | **200,473** | 1,806 | **111.00** | **1,772** | 31 | 2 | 1 (inv) |
| **4** | `fa1c13f2614d7b5c4749cbc52fecda94` | **194,042** | 585 | **331.70** | **578** | 4 | 1 | 2 (proc) |
| **5** | `7c67e1448b00f6e969d365cea6b010ab` | **187,924** | 982 | **191.37** | **973** | 7 | 0 | 2 (inv) |

#### Key Findings
- **Revenue Concentration:** A small group of top sellers produces a large share of marketplace GMV, led by the top seller at over **BRL 229,000**.
- **High-AOV vs. High-Volume Strategy:** Seller `53243585...` generated BRL 222,776 across just 358 orders (premium BRL 622 AOV). In contrast, Seller `4a3ca931...` generated BRL 200,473 through high order volume (1,806 orders at BRL 111 AOV).
- **Fulfillment Reliability:** Top sellers maintained strong fulfillment standards, achieving **>98.5% delivery completion rates** with minimal cancellations.
- **Vendor Retention:** Introducing tiered commission discounts for high-volume sellers and automated dispatch reminders can help retain top merchants and reduce seller-side fulfillment delays.

---

### 7. Payment Preferences & Installments

<div align="center">
  <img src="./Chart/payment_type.png" alt="Number of Order based on Payment Type" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 34: Payment Method Distribution.</em></p>
</div>

#### Key Findings
- **Credit Card Popularity:** Roughly **75% of all orders** are paid by Credit Card, with customers frequently choosing 3 to 10 month installment plans.
- **Boleto Payment Drop-off:** **Boleto** makes up around 19% of orders, but many issued vouchers expire unpaid, leading to lost conversions.
- **Recovery Strategy:** Sending automated WhatsApp or SMS payment reminders within 24 hours of Boleto issuance can recover a substantial portion of abandoned orders.

---

## Natural Language Processing & AI Review Translation

To analyze Portuguese customer reviews in English, a translation pipeline was set up using **Python, Agno (`Agent`), Groq, and Pydantic** to automate translation and structure the text for sentiment analysis.

### Translation Pipeline Code Snippet

```python
import pandas as pd
from agno.agent import Agent
from agno.models.groq import Groq
from pydantic import BaseModel, Field
import time

df = pd.read_csv("/content/olist_order_reviews_dataset.csv")
new_df = df.dropna(subset=["review_comment_message"], how="all")

new_df_1 = new_df.set_index("review_id")["review_comment_message"].to_dict()

class Response(BaseModel):
    english: str = Field(..., description="Give the english translated text")

agent = Agent(
    model=Groq(id="qwen/qwen3-32b", api_key="<API-Key>"),
    instructions="You are a Portuguese to English translator.",
    output_schema=Response
)

translated_df = {}
for i, j in list(new_df_1.items())[:500]:
    response = agent.run(j, output_schema=Response)
    translated_df[i] = response.content.english
    time.sleep(3)
```

---

### Review Sentiment Analysis

- The translated reviews dataset (from Kaggle) replaced original Portuguese columns with English translations:
    - `review_comment_title` (translated via Google Cloud API)
    - `review_comment_message` (translated via Google Cloud API)

- Sentiment was analyzed using **TextBlob** and **VADER**.
    - Both tools rely on predefined lexicons where words have positive or negative weights. They scan sentences, look up words in their dictionary, and calculate an aggregate sentiment score.

<div align="center">
  <img src="./Chart/Sentiment_by_review_bucket.png" alt="Sentiment Score Distribution by Review Score Bucket" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 35: Sentiment Score Distribution Across Review Score Buckets.</em></p>
</div>

#### Limitations of TextBlob and VADER
Because both tools are rule-based, they do not understand context. Typical failure cases include:
- **Implicit Sentiment:** *"I had to call customer service three times to get my package."* (Clearly negative experience, but contains no explicitly negative dictionary words).
- **Sarcasm and Irony:** *"Great job taking 40 days to deliver."* (Incorrectly scored as positive due to the phrase "great job").
- **Mixed Sentiment (Aspects):** *"The product is amazing but the transport company lost my first package."* (Positive product feedback and negative shipping feedback cancel each other out to a neutral score).

#### Sentiment Score Correlation Matrix (Kendall Method)

<div align="center">

| Metric | Review Score | Textblob Subjectivity | Textblob Polarity | Vader Compound |
| :--- | :---: | :---: | :---: | :---: |
| **Review Score** | 1.000000 | 0.191106 | 0.432982 | 0.469155 |
| **Textblob Subjectivity** | 0.191106 | 1.000000 | 0.460677 | 0.300689 |
| **Textblob Polarity** | 0.432982 | 0.460677 | 1.000000 | 0.545046 |
| **Vader Compound** | 0.469155 | 0.300689 | 0.545046 | 1.000000 |

</div>

**Correlation Matrix Findings:**
- **VADER vs. TextBlob Accuracy:** `Vader Compound` shows a stronger positive correlation (0.469) with the actual `Review Score` than `Textblob Polarity` (0.433), showing that VADER is slightly better at capturing customer sentiment in this dataset.
- **Subjectivity Independence:** `Textblob Subjectivity` has a weak correlation with `Review Score` (0.191). Whether a customer's review is opinionated or strictly factual has little bearing on whether they leave a positive or negative rating.

---

### Customer Review Text Analytics (N-Gram Analysis and Wordcloud)

<div align="center">
  <img src="./Chart/Positive_review_Ngrams.png" alt="Positive Review N-Grams Analysis" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 36: Top Positive Review N-Grams & Key Phrases.</em></p>
</div>

<div align="center">
  <img src="./Chart/Negative_review_Ngrams.png" alt="Negative Review N-Grams Analysis" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 37: Top Negative Review N-Grams & Key Phrases.</em></p>
</div>

<div align="center">
  <img src="./Chart/Portuguese_wordcloud.png" alt="Portuguese Word Cloud Analytics" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 38: Portuguese Word Cloud Analysis.</em></p>
</div>

<div align="center">
  <img src="./Chart/English_wordcloud.png" alt="English Word Cloud Analytics" width="85%" style="border-radius: 8px; margin-bottom: 15px;" />
  <p><em>Figure 39: English Translated Word Cloud Analysis.</em></p>
</div>

#### Text Analytics Key Findings
- **High-Frequency Portuguese Terms:** **`produto`** (product), **`entrega`** (delivery), **`prazo`** (deadline), and **`recebi`** (received).
- **Positive Sentiment Drivers:** Satisfied customers consistently praise early fulfillment, product quality, and smooth delivery (*"arrived before deadline"*, *"excellent product"*, *"highly recommend"*).
- **Negative Sentiment Drivers:** Negative reviews are dominated by shipping delays, lost packages, and items that did not match expectations (*"product not received"*, *"delivery delay"*, *"different from picture"*).
- **Operational Takeaway:** Customer ratings on Olist are driven primarily by two operational fundamentals: delivering on or before promised dates, and ensuring products match catalog descriptions.