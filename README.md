# 🛒 E-Commerce Sales Analytics Dashboard

A comprehensive end-to-end business analytics project built on 51,290 global e-commerce transactions spanning January to December 2015. The project transforms raw transactional data into an interactive Excel dashboard enriched with advanced KPIs, trend analysis, and strategic business recommendations.

---

## 📁 Project Structure

```
ecommerce-analytics/
│
├── E-Commerce_Dashboard_Analytics.xlsx   # Main workbook (data + original dashboard + pivot)
├── E-Commerce_Enhanced_Dashboard.xlsx    # Enhanced dashboard with all new analytics sections
├── Ecommerce_Dashboard_Report.pdf        # Full write-up report (11 sections)
├── FORMULAS.md                           # All Excel formulas and logic used
└── README.md                             # This file
```

---

## 📊 Dataset Overview

| Attribute         | Details                                      |
|-------------------|----------------------------------------------|
| Total Records     | 51,290 orders                                |
| Time Period       | January 2015 – December 2015                 |
| Columns           | 21                                           |
| Regions           | 13 (Africa, Canada, Caribbean, Central, Central Asia, EMEA, East, North, North Asia, Oceania, South, Southeast Asia, West) |
| Product Categories| Auto & Accessories, Electronic, Fashion, Home & Furniture |
| Customer Segments | Consumer, Corporate, Home Office             |
| Shipping Modes    | First Class, Same Day, Second Class, Standard Class |

### 📋 Column Descriptions

| Column           | Description                                          |
|------------------|------------------------------------------------------|
| `Order ID`       | Unique identifier for each order                     |
| `Order Date`     | Date the order was placed                            |
| `Ship Date`      | Date the order was shipped                           |
| `Aging`          | Number of days between order and ship date           |
| `Ship Mode`      | Shipping method selected by customer                 |
| `Product Category` | High-level product grouping                        |
| `Product`        | Specific product name                                |
| `Sales`          | Revenue generated from the order ($)                 |
| `Quantity`       | Number of units ordered                              |
| `Discount`       | Discount applied (as a decimal, e.g. 0.05 = 5%)     |
| `Profit`         | Profit earned from the order ($)                     |
| `Shipping Cost`  | Cost of shipping the order ($)                       |
| `Order Priority` | Fulfillment urgency (Critical / High / Medium / Low) |
| `Customer ID`    | Unique identifier for each customer                  |
| `Customer Name`  | Full name of the customer                            |
| `Segment`        | Customer segment classification                      |
| `City`           | Customer city                                        |
| `State`          | Customer state/province                              |
| `Country`        | Customer country                                     |
| `Region`         | Broader geographic region                            |
| `Months`         | Month name extracted from Order Date                 |

---

## 📈 Key Metrics (Full Year)

| KPI                        | Value         |
|----------------------------|---------------|
| Total Revenue              | $8,023,381    |
| Total Profit               | $3,729,903    |
| Profit Margin              | 46.49%        |
| Total Orders               | 51,290        |
| Total Units Sold           | 153,732       |
| Average Order Value (AOV)  | $156.43       |
| Average Shipping Cost      | $7.27         |
| Average Discount           | 3.0%          |
| Peak Revenue Month         | December      |
| Lowest Revenue Month       | February      |

---

## 🗂️ Dashboard Sheets

### Sheet 1 — Sales Data
Raw transactional data with 51,290 rows and 21 columns. This is the single source of truth for all analysis.

### Sheet 2 — Pivot & Slicers
The original summary dashboard with pivot tables and Excel slicers for interactive filtering by month, category, region, and segment.

### Sheet 3 — Enhanced Dashboard
A fully rebuilt analytics layer featuring:

| Section                          | What It Shows                                              |
|----------------------------------|------------------------------------------------------------|
| Core KPIs                        | Revenue, Profit, Orders, Profit Margin                     |
| New Performance Indicators       | AOV, Repeat Rate, Ship Cost %, Items/Order, Priority %     |
| Monthly Performance Trend        | 12-month breakdown with MoM growth and margin              |
| Category Performance             | Revenue share, profit, margin by product category          |
| Segment Performance              | Sales, profit, AOV by customer segment                     |
| Shipping & Fulfillment Analysis  | Cost ratio and fulfilment days by shipping mode            |
| Discount Impact Analysis         | Profit erosion across discount tiers (0–5%)                |
| Top 10 Products                  | Revenue, profit, margin, units for top performers          |
| Regional Performance             | All 13 regions ranked by revenue with AOV and margin       |
| Business Insights Box            | 8 prioritised, data-backed recommendations                 |

---

## 💡 Key Business Insights

1. **Fashion dominates** — 65% of total revenue; top product is T-Shirts at $692K
2. **Discount erodes profit** — each 1% discount tier reduces avg profit by ~$4–5 (up to -20.3% at 4–5%)
3. **Standard Class shipping** has the highest cost ratio (4.77%) despite being the most common mode
4. **Central region leads** globally; Canada significantly underperforms ($60K vs $1.74M for Central)
5. **December and March** are peak months; February is the weakest (-9.8% MoM)
6. **Profit margin is stable** at ~46.5% across all months and segments — a sign of consistent cost structure
7. **Electronics is underrepresented** at only 4.9% revenue share — an untapped growth opportunity
8. **Repeat customer loyalty** programme could add ~$200K in annual revenue with a 5% retention improvement

---

## 🛠️ Tools & Technologies

| Tool            | Purpose                                      |
|-----------------|----------------------------------------------|
| Microsoft Excel | Dashboard, pivot tables, slicers, charts     |
| Python 3        | Data analysis and dashboard generation       |
| pandas          | Data manipulation and metric calculation     |
| openpyxl        | Excel file creation and formatting           |
| reportlab       | PDF report generation                        |

---

## 🚀 How to Use

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/ecommerce-analytics.git
   cd ecommerce-analytics
   ```

2. **Open the Enhanced Dashboard**
   Open `E-Commerce_Enhanced_Dashboard.xlsx` in Microsoft Excel or LibreOffice Calc.

3. **Use Slicers** (in the Pivot & Slicers sheet) to filter by Month, Region, Category, or Segment interactively.

4. **Read the Report**
   Open `Ecommerce_Dashboard_Report.pdf` for the full analytical write-up with all findings and recommendations.

5. **Refer to FORMULAS.md** for a breakdown of every metric, formula, and logic used in the dashboard.

---

## 📄 Report Contents (PDF)

The accompanying PDF report covers:
1. Executive Summary
2. Original Dashboard — Existing Metrics
3. New KPIs Introduced
4. Monthly Performance Trend
5. Category & Segment Performance
6. Shipping & Fulfillment Analysis
7. Discount Impact on Profit
8. Top 10 Products by Revenue
9. Regional Performance
10. Key Business Insights & Recommendations
11. Summary of Dashboard Changes

---

## 👤 Author

**Your Name**
- GitHub: [@yourusername](https://github.com/yourusername)
- LinkedIn: [linkedin.com/in/yourprofile](https://linkedin.com/in/yourprofile)

---

## 📝 License

This project is open source and available under the [MIT License](LICENSE).
