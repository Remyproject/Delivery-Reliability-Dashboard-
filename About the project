# Delivery Reliability Dashboard  
**From reporting metrics to decision pressure**

## Overview

This project is a one-page operational dashboard designed to answer a simple but uncomfortable question:

**Are we actually keeping our delivery promises?**

Instead of tracking as many metrics as possible, the dashboard focuses on:
- What is breaking
- Where to intervene first
- Whether the problem is repeating

The goal is not visibility.  
The goal is **action**.

---

## Business Problem

Most supply chain dashboards fail for one reason:

They describe performance without forcing decisions.

Teams see:
- OTIF percentages
- Delivery counts
- Trend lines

But they still leave meetings asking:
- *What should we fix first?*
- *Where is the real damage coming from?*
- *Is this noise or a systemic issue?*

This dashboard was built to remove that ambiguity.

---

## Business Questions This Dashboard Answers

1. **Are we meeting delivery commitments right now?**
2. **Which products are responsible for most failures?**
3. **How are deliveries failing (late, incomplete, or both)?**
4. **Are failures isolated or repeating over time?**

If a visual does not help answer one of these questions, it does not exist on the dashboard.

---

## Dataset Overview

Core delivery-level fields used:

- `order_id`
- `order_placement_date`
- `product_id`
- `order_qty`
- `delivery_qty`
- `on_time` (1 = Yes, 0 = No)
- `in_full` (1 = Yes, 0 = No)

The model intentionally avoids unnecessary dimensions to keep focus on delivery reliability.

---

## Key KPIs (Decision Layer)

| KPI | Purpose |
|---|---|
| **OTIF % (Current Month)** | Measures reliability of delivery promises |
| **Late Delivery Rate** | Identifies timing failures |
| **In-Full Failure Rate** | Identifies fulfillment failures |
| **Total Orders** | Context for scale |
| **Month-over-Month Delta** | Shows direction, not just status |

> KPIs are compared against the previous month to force a directional conversation, not a static one.

---

## Core Logic Design

### Failed Delivery Flag (Row-Level Classification)

```DAX
Failed Delivery Flag =
IF(
    supply_chain[on_time] = 0
        || supply_chain[in_full] = 0,
    1,
    0
)


Failure Type =
SWITCH(
    TRUE(),
    supply_chain[on_time] = 0 && supply_chain[in_full] = 1, "Late Only",
    supply_chain[on_time] = 1 && supply_chain[in_full] = 0, "In-Full Only",
    supply_chain[on_time] = 0 && supply_chain[in_full] = 0, "Late & In-Full",
    BLANK()
)
