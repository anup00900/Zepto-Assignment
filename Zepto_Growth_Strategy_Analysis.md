
# Growth Strategy for Zepto's 10-Minute Delivery Target

## Problem Analysis
Zepto aims to achieve a 10-minute delivery target, with a probability of success `p` influenced by daily investments `mi` in improving delivery speed. Marketing investments `Mi` also affect customer growth. Our goal is to strategize spending on delivery and marketing to maximize customer growth over 30 days, starting with 1.02 million customers and a capital of 15 million INR.

### Equations Provided:
1. **Delivery success probability (p) depends on `mi`:**
   
   p = 0.8 * (1.25 - exp(-mi / 5))

2. **Growth factor (G) depends on `p` and `Mi`:**
   
   G = 38/40 + 1/40 * [(0.45 + p)^0.30 + (Mi / (M0 + 1))^0.05]

3. **Customer growth: G = Ci / Ci-1**

Our objective is to model customer growth and manage spending over the 30-day period.

## Mathematical Analysis of p
Let's analyze the bounds of the delivery probability function `p`:

Given:
   
   p = 0.8 * (1.25 - exp(-mi / 5))

- **As `mi` approaches zero**:
   - exp(-mi / 5) approaches 1, so p ≈ 0.8 * (1.25 - 1) = 0.2
   - Therefore, as `mi` → 0, p approaches 0.2.

- **As `mi` approaches infinity**:
   - exp(-mi / 5) approaches 0, so p ≈ 0.8 * 1.25 = 1
   - Therefore, as `mi` → ∞, p approaches 1 (maximum probability).

This indicates diminishing returns for increasing `mi`, as `p` asymptotically approaches a maximum of 1.

## Step-by-Step Solution Outline
1. Initialize customer base and capital.
2. Calculate daily spending on delivery improvements (`mi`) and marketing (`Mi`).
3. Compute delivery probability `p` based on `mi`.
4. Calculate growth factor `G` using `p` and `Mi`.
5. Update customer count based on G.
6. Estimate daily orders and profit using order frequency and profit margin.
7. Update capital after accounting for `mi`, `Mi`, and daily profit.
8. Repeat steps for 30 days to project growth and capital.

This strategy balances spending between delivery improvements and marketing to optimize growth.

## Python Code and Explanation
The following Python code implements the strategy over a 30-day period. It calculates daily values for customer growth, orders, and capital:

- **Load order frequency data and calculate daily average orders**.
- **Set initial capital, customer base, and spending amounts**.
- **For each day**:
    1. Calculate `p` based on `mi`.
    2. Compute `G` based on `p` and `Mi`.
    3. Update customer count `Ci`.
    4. Estimate daily profit and update capital.

The daily outputs are stored and saved in a CSV format for analysis.

```python
import numpy as np
import pandas as pd

initial_customers = 1.02 * 10**6
initial_capital = 15 * 10**6
M0 = 5 * 10**6
AOV = 300
profit_margin = 0.20
days = 30
order_data = pd.DataFrame(...)
avg_order_frequency_per_week = order_data['order_frequency_per_week'].mean()
daily_order_frequency = avg_order_frequency_per_week / 7

output_data = []
capital = initial_capital
customers = initial_customers

for day in range(1, days + 1):
    mi = 1 * 10**6  
    Mi = 2 * 10**6  
    p = 0.8 * (1.25 - np.exp(-mi / 5))
    G = (38 / 40) + (1 / 40) * ((0.45 + p)**0.30 + (Mi / (M0 + 1))**0.05)
    new_customers = int(customers * G)
    total_orders = new_customers * daily_order_frequency
    daily_profit = total_orders * AOV * profit_margin
    capital = capital - mi - Mi + daily_profit
    output_data.append([day, capital + mi + Mi - daily_profit, customers, mi, p, Mi, G, new_customers, total_orders, capital])
    customers = new_customers

output_df = pd.DataFrame(output_data, columns=[...])
output_df.to_csv('growth_strategy.csv', index=False)
```

## Recommendations for Improvement
1. **Dynamic Spending Adjustment**: Adjusting `mi` and `Mi` dynamically based on growth and capital could improve customer acquisition.
2. **Customer Retention**: Balancing new customer acquisition with customer retention can lead to more stable growth.
3. **Sensitivity Testing**: Testing different `mi` and `Mi` values across days could help optimize results.
