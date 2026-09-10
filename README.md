# Supply Chain Performance & OTIF Analytics

## 📌 Overview

An end-to-end Power BI dashboard analyzing supply chain operations using the **OTIF (On-Time In-Full)** framework. It tracks delivery efficiency across regions, warehouses, and transport modes to identify logistics bottlenecks.

---

## 📊 Key Operational Metrics

| Metric | Value | Definition |
| --- | --- | --- |
| **Total Orders** | 100 | Total shipments evaluated |
| **On-Time (OT %)** | 67.00% | Orders delivered with 0 delay days |
| **In-Full (IF %)** | 53.00% | Orders where `DeliveredQty` >= `OrderedQty` |
| **OTIF %** | 66.00% | Orders meeting **both** OT and IF criteria |
| **Avg Delay** | 0.95 Days | Average delivery lag across orders |

---

## 📐 Data Model (Star Schema)

Built using a clean 1-to-Many Star Schema connecting facts and dimensions:

* **`FACT_SCM` (`*`)**: Transactional order & shipment data.
* **`DIM_MATERIAL` (`1`)**: Product details, suppliers, and warehouse locations.
* **`Date_Table` (`1`)**: Dedicated calendar table for time intelligence.

---

## 🧮 Core DAX Measures

```dax
-- On-Time In-Full Rate %
OTIF % = DIVIDE(SUM(FACT_SCM[OTIF]), [Total Orders], 0)

-- On-Time Delivery Rate %
OT % = DIVIDE(SUM(FACT_SCM[OT]), [Total Orders], 0)

-- In-Full Delivery Rate %
IF % = DIVIDE(SUM(FACT_SCM[IF]), [Total Orders], 0)

-- Average Shipping Delay (Days)
Average Delay = AVERAGE(FACT_SCM[DelayDays])

```

---

## 💡 Key Business Insights

* **Regional Bottleneck:** The **East** and **South** regions achieved high fulfillment, while the **West** region lagged significantly (~20% OTIF).
* **Transport Delay:** Orders shipped via **Truck** experienced higher average delays compared to **Air** or **Ship** modes.
* **Warehouse Impact:** **Bangalore** and **Delhi** hubs recorded the highest average shipping delays (1.00 day).

---
