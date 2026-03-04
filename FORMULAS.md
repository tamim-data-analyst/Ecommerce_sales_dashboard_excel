# 📐 FORMULAS.md — Logic & Calculations Reference

This file documents every metric, formula, and calculation used in the E-Commerce Analytics Dashboard. It covers both the Excel formulas used in the workbook and the equivalent Python/pandas logic used to generate the Enhanced Dashboard.

---

## 1. Core KPIs

### Total Revenue (Total Sales)
**What it measures:** Sum of all order revenues across the year.

```excel
=SUM(SalesData[Sales])
```
```python
df['Sales'].sum()
# Result: 8,023,381
```

---

### Total Profit
**What it measures:** Sum of all profits earned across all orders.

```excel
=SUM(SalesData[Profit])
```
```python
df['Profit'].sum()
# Result: 3,729,903
```

---

### Total Orders
**What it measures:** Count of all order rows. Each row = one unique order (verified: 0 duplicate Order IDs).

```excel
=COUNTA(SalesData[Order ID])
```
```python
df['Order ID'].count()
# Unique check:
df['Order ID'].nunique()
# Both return: 51,290 — confirming no duplicate Order IDs exist
```

> ✅ **Verification:** `df.duplicated('Order ID').sum()` returned `0`, confirming every Order ID is unique. Total rows = Total unique orders.

---

### Profit Margin %
**What it measures:** Overall profitability as a percentage of revenue.

```excel
=SUM(SalesData[Profit]) / SUM(SalesData[Sales])
```
```python
df['Profit'].sum() / df['Sales'].sum()
# Result: 0.4649 → 46.49%
```

---

### Total Quantity Sold
**What it measures:** Total units sold across all orders.

```excel
=SUM(SalesData[Quantity])
```
```python
df['Quantity'].sum()
# Result: 153,732
```

---

### Average Shipping Cost
**What it measures:** Mean shipping cost per order.

```excel
=AVERAGE(SalesData[Shipping Cost])
```
```python
df['Shipping Cost'].mean()
# Result: $7.27
```

---

### Average Discount
**What it measures:** Mean discount applied per order (as a decimal).

```excel
=AVERAGE(SalesData[Discount])
```
```python
df['Discount'].mean()
# Result: 0.02997 → ~3.0%
```

---

## 2. New KPIs

### Average Order Value (AOV)
**What it measures:** Average revenue generated per order transaction.

```excel
=SUM(SalesData[Sales]) / COUNTA(SalesData[Order ID])
```
```python
df['Sales'].sum() / df['Order ID'].count()
# Result: $156.43
```

---

### Repeat Customer Rate
**What it measures:** Proportion of customers who placed more than one order.

```excel
# Not directly available in Excel without helper columns.
# Requires a helper column counting orders per Customer ID:
=COUNTIF(SalesData[Customer ID], [@[Customer ID]])
# Then count customers where this is > 1 / total unique customers
```
```python
repeat_cust = df.groupby('Customer ID')['Order ID'].count()
repeat_rate = repeat_cust[repeat_cust > 1].count() / repeat_cust.count()
```

---

### Shipping Cost as % of Revenue
**What it measures:** What proportion of revenue is consumed by shipping costs — a logistics efficiency metric.

```excel
=SUM(SalesData[Shipping Cost]) / SUM(SalesData[Sales])
```
```python
df['Shipping Cost'].sum() / df['Sales'].sum()
# Result: ~4.6%
```

---

### Items per Order
**What it measures:** Average number of units in each order — an indicator of basket size and cross-sell effectiveness.

```excel
=SUM(SalesData[Quantity]) / COUNTA(SalesData[Order ID])
```
```python
df['Quantity'].sum() / df['Order ID'].count()
# Result: ~3.0 items per order
```

---

### High Priority Order %
**What it measures:** Share of orders that are Critical or High priority — indicates operational urgency load.

```excel
=COUNTIFS(SalesData[Order Priority],"Critical",SalesData[Order Priority],"High")
 / COUNTA(SalesData[Order ID])

# Correct COUNTIFS for OR condition:
=(COUNTIF(SalesData[Order Priority],"Critical") + COUNTIF(SalesData[Order Priority],"High"))
 / COUNTA(SalesData[Order ID])
```
```python
high_prio = df[df['Order Priority'].isin(['Critical', 'High'])]['Order ID'].count()
high_prio / df['Order ID'].count()
# Result: ~37.6%
```

---

## 3. Monthly Performance Metrics

### Monthly Sales
```excel
=SUMIF(SalesData[Months], "Jan", SalesData[Sales])
# Repeat for each month
```
```python
df.groupby('Months')['Sales'].sum()
```

---

### Monthly Profit
```excel
=SUMIF(SalesData[Months], "Jan", SalesData[Profit])
```
```python
df.groupby('Months')['Profit'].sum()
```

---

### Monthly Order Count
```excel
=COUNTIF(SalesData[Months], "Jan")
```
```python
df.groupby('Months')['Order ID'].count()
```

---

### Monthly Profit Margin %
```excel
=SUMIF(SalesData[Months],"Jan",SalesData[Profit])
 / SUMIF(SalesData[Months],"Jan",SalesData[Sales])
```
```python
monthly['Profit'] / monthly['Sales']
```

---

### Monthly Average Order Value (AOV)
```excel
=SUMIF(SalesData[Months],"Jan",SalesData[Sales])
 / COUNTIF(SalesData[Months],"Jan")
```
```python
monthly['Sales'] / monthly['Orders']
```

---

### Month-over-Month (MoM) Sales Growth
**What it measures:** Percentage change in sales compared to the previous month.

```excel
# In a monthly summary table where B2=Jan sales, B3=Feb sales...
=(B3 - B2) / B2
```
```python
monthly_sorted['Sales'].pct_change()
# Jan: — (no prior month)
# Feb: (610240 - 676313) / 676313 = -9.77%
```

---

## 4. Category & Segment Metrics

### Sales by Category
```excel
=SUMIF(SalesData[Product Category], "Fashion", SalesData[Sales])
```
```python
df.groupby('Product Category')['Sales'].sum()
```

---

### Profit Margin by Category
```excel
=SUMIF(SalesData[Product Category],"Fashion",SalesData[Profit])
 / SUMIF(SalesData[Product Category],"Fashion",SalesData[Sales])
```
```python
cat_df['Profit'] / cat_df['Sales']
```

---

### Revenue Share by Category
```excel
=SUMIF(SalesData[Product Category],"Fashion",SalesData[Sales])
 / SUM(SalesData[Sales])
```
```python
cat_df['Sales'] / cat_df['Sales'].sum()
```

---

### Average Order Value by Segment
```excel
=SUMIF(SalesData[Segment],"Consumer",SalesData[Sales])
 / COUNTIF(SalesData[Segment],"Consumer")
```
```python
seg_df['Sales'] / seg_df['Orders']
```

---

## 5. Shipping & Fulfillment Metrics

### Shipping Cost by Mode
```excel
=SUMIF(SalesData[Ship Mode], "Standard Class", SalesData[Shipping Cost])
```
```python
df.groupby('Ship Mode')['Shipping Cost'].sum()
```

---

### Shipping Cost as % of Sales by Mode
```excel
=SUMIF(SalesData[Ship Mode],"Standard Class",SalesData[Shipping Cost])
 / SUMIF(SalesData[Ship Mode],"Standard Class",SalesData[Sales])
```
```python
ship_df['ShipCost'] / ship_df['Sales']
# Standard Class: 4.77%
# First Class:    4.41%
# Same Day:       4.41%
# Second Class:   4.45%
```

---

### Average Fulfillment Days (Aging) by Ship Mode
**What it measures:** Mean number of days between Order Date and Ship Date, by shipping method.

```excel
=AVERAGEIF(SalesData[Ship Mode], "Standard Class", SalesData[Aging])
```
```python
df.groupby('Ship Mode')['Aging'].mean()
# Same Day:       1.0 day
# First Class:    5.5 days
# Second Class:   5.5 days
# Standard Class: 5.5 days
```

> 💡 Note: `Aging` column = `Ship Date - Order Date` in days (pre-calculated in dataset).

---

## 6. Discount Impact Analysis

### Discount Tier Segmentation
**Logic:** Orders are grouped into 1% discount buckets to measure profit erosion per tier.

```excel
# Helper column for discount tier:
=IF(Discount<=0.01,"0-1%",IF(Discount<=0.02,"1-2%",IF(Discount<=0.03,"2-3%",
  IF(Discount<=0.04,"3-4%","4-5%"))))
```
```python
bins   = [0, 0.01, 0.02, 0.03, 0.04, 0.051]
labels = ['0-1%', '1-2%', '2-3%', '3-4%', '4-5%']
df['Disc_Bin'] = pd.cut(df['Discount'], bins=bins, labels=labels)
```

---

### Average Profit by Discount Tier
```excel
=AVERAGEIF(HelperCol[Disc_Tier], "0-1%", SalesData[Profit])
```
```python
df.groupby('Disc_Bin', observed=True)['Profit'].mean()
# 0-1%: $80.32
# 1-2%: $77.09
# 2-3%: $73.83
# 3-4%: $68.31
# 4-5%: $63.99
```

---

### Profit Drop % vs Baseline (0-1% tier)
```excel
=(AverageProfitTier - AverageProfitBaseline) / AverageProfitBaseline
```
```python
base = disc_df['AvgProfit'].iloc[0]   # 0-1% tier avg profit
disc_df['Drop'] = (disc_df['AvgProfit'] - base) / base
# 1-2%: -4.0%
# 2-3%: -8.1%
# 3-4%: -15.0%
# 4-5%: -20.3%
```

---

## 7. Regional Performance

### Sales by Region
```excel
=SUMIF(SalesData[Region], "Central", SalesData[Sales])
```
```python
df.groupby('Region')['Sales'].sum()
```

---

### Profit Margin by Region
```excel
=SUMIF(SalesData[Region],"Central",SalesData[Profit])
 / SUMIF(SalesData[Region],"Central",SalesData[Sales])
```
```python
reg_df['Profit'] / reg_df['Sales']
```

---

### Average Order Value by Region
```excel
=SUMIF(SalesData[Region],"Central",SalesData[Sales])
 / COUNTIF(SalesData[Region],"Central")
```
```python
reg_df['Sales'] / reg_df['Orders']
```

---

## 8. Order Priority Analysis

### Orders by Priority
```excel
=COUNTIF(SalesData[Order Priority], "Critical")
```
```python
df['Order Priority'].value_counts()
# Medium:   29,433 (57.4%)
# High:     15,501 (30.2%)
# Critical:  3,932  (7.7%)
# Low:       2,424  (4.7%)
```

---

### Average Fulfillment Days by Priority
```excel
=AVERAGEIF(SalesData[Order Priority], "Critical", SalesData[Aging])
```
```python
df.groupby('Order Priority')['Aging'].mean()
```

---

### Priority as % of Total Orders
```excel
=COUNTIF(SalesData[Order Priority],"Critical") / COUNTA(SalesData[Order ID])
```
```python
prio_df['Orders'] / prio_df['Orders'].sum()
```

---

## 9. Top Product Ranking

### Sales by Product
```excel
# Use a pivot table: Row = Product, Values = Sum of Sales, sorted descending
=SUMIF(SalesData[Product], "T-Shirts", SalesData[Sales])
```
```python
df.groupby('Product')['Sales'].sum().sort_values(ascending=False).head(10)
```

---

### Product Profit Margin
```excel
=SUMIF(SalesData[Product],"T-Shirts",SalesData[Profit])
 / SUMIF(SalesData[Product],"T-Shirts",SalesData[Sales])
```
```python
prod_df['Profit'] / prod_df['Sales']
```

---

## 10. Data Validation Checks Used

| Check | Formula / Code | Result |
|-------|----------------|--------|
| Duplicate Order IDs | `df.duplicated('Order ID').sum()` | 0 — no duplicates |
| Null values | `df.isnull().sum()` | 0 — no missing data |
| Negative profits | `df[df['Profit'] < 0].shape[0]` | 0 — no loss-making orders |
| Discount range | `df['Discount'].between(0, 0.05).all()` | True — all within 0–5% |
| Aging range | `df['Aging'].min(), df['Aging'].max()` | 1 to 10 days |

---

## 📌 Formula Naming Conventions Used in Excel

| Convention | Meaning |
|------------|---------|
| `SalesData[Column]` | Structured table reference (Excel Table named `SalesData`) |
| `SUMIF(range, criteria, sum_range)` | Conditional sum |
| `COUNTIF(range, criteria)` | Conditional count |
| `AVERAGEIF(range, criteria, avg_range)` | Conditional average |
| `SUMIFS(...)` | Multi-condition sum |
| `COUNTIFS(...)` | Multi-condition count |

---

*All formulas verified against the raw Sales Data sheet (51,290 rows, 21 columns).*
