
# Zepto Growth Strategy Analysis

This project involves a strategic analysis and simulation to maximize customer growth for Zepto's 10-minute delivery target. The analysis focuses on balancing spending between improving delivery outcomes and marketing to increase customer acquisition over a 30-day period.

## Problem Overview
Zepto aims to achieve a 10-minute delivery target. The probability of successful delivery within 10 minutes, denoted by `p`, is influenced by daily investments `mi` in delivery improvements. Marketing spending `Mi` also impacts customer growth. The objective is to create a growth strategy over a 30-day period, starting with an initial customer base of 1.02 million and an initial capital of 15 million INR.

## Key Equations
1. **Delivery Success Probability (`p`):**
   
   p = 0.8 * (1.25 - exp(-mi / 5))
   
2. **Growth Factor (`G`):**
   
   G = 38/40 + 1/40 * [(0.45 + p)^0.30 + (Mi / (M0 + 1))^0.05]
   
3. **Customer Growth:**

   
   G = Ci / Ci-1

## Solution Outline
1. **Initialization**: Set initial customer base and capital.
2. **Daily Calculations**:
   - Compute probability `p` based on `mi`.
   - Calculate growth factor `G` using `p` and `Mi`.
   - Update customer base `Ci`.
   - Estimate daily profit based on total orders and profit margin.
3. **Capital Update**: Adjust daily capital based on delivery improvement and marketing spending, adding daily profit.
4. **Iteration**: Repeat for 30 days to simulate customer and capital growth.

## Python Code Implementation
The provided Python code calculates daily values for customer growth, orders, and capital over the 30-day period, saving outputs to a CSV for further analysis.

## Recommendations for Optimization
1. **Dynamic Spending**: Adjust `mi` and `Mi` dynamically based on available capital and growth trends.
2. **Retention Strategies**: Balancing customer acquisition with retention strategies can ensure sustained growth.
3. **Sensitivity Testing**: Testing various values of `mi` and `Mi` can identify the optimal spending strategy.

## Files
- **growth_strategy.csv**: Contains daily growth data and capital calculations.
- **Zepto_Growth_Strategy_Analysis.md**: Detailed Markdown report of the analysis.
- **README.md**: Summary of the project and analysis.

