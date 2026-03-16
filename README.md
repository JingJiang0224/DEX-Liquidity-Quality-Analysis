# On-Chain Trading Data: DEX Liquidty Quality Analysis



**Authour**: Jing Jiang

**Date**: Nov 2025 - Feb 2026

**Data Source**: On-chain trading data from Uniswap V2

**Tools**: Dune Analytics, SQL

**Link of Dashboard**: link

**Link of Code**: link



<br />
<br />



## Research Question 
Which liquidity pools on Uniswap V2 provide the **highest market quality**?

<br />



## Introduction

This project evaluates **the quality of liquidity pools on Uniswap V2** using on-chain trading data.

**Uniswap V2** allows anyone to create liquidity pools, resulting in thousands of trading pairs with highly uneven liquidity, activity, and trader participation. Many pools are inactive, illiquid, or dominated by automated trading.

<br />

To identify economically meaningful pools, this analysis ranks pairs across **three dimensions**:

- Liquidity Capacity
- Trade Activity
- Price Quality

The goal is to highlight pools that provide stable liquidity, active trading, and efficient price discovery.
<br />


<br />


## **Methodology**

### A. Analytical Framework

This project proposes a **multi-dimensional framework** to systematically evaluate the quality of trading pairs on Uniswap V2.

Rather than relying on a single metric such as trading volume or liquidity size, the analysis evaluates pools across three complementary dimensions that reflect different aspects of market performance:

1. **Liquidity Quality** — whether a pool provides sufficient and stable liquidity depth

2. **Trade Activity** — whether the pool is consistently used by diverse participants

3. **Market Quality** — whether trades can be executed efficiently with prices aligned to the broader market

Each dimension captures a different characteristic of a healthy trading market. Together, by condensing score for each dimension, they provide a more comprehensive view of pool quality.

Framework flow:


<br />

### B. Methodology Overview
### Step 1 - Data Aggregation and Preprocessing



<br />
<br />
Project Title
 
 ├ Overview
 
 ├ Methodology
 
 ├ Metrics
 
 ├ Dashboard
 
 └ Key Findings

> Key Insight  
> Pools with high liquidity do not always attract organic trading activity.

### Step 2 - Metric Construction in Each Dimension
**(1) Dimension 1: Liquidity Quality**

&nbsp;&nbsp;**Goal:** Liquidity Quality dimension is to measure how much liquidity exists and how reliable it is. 


<br />

&nbsp;&nbsp;**Metrics used:**

&nbsp;&nbsp;**a. Liquidity Depth**
   - avg_reserve_usd_7d 


&nbsp;&nbsp;**b. Liquidity Stability**
   - liquidity_stability_score
              
              - liquidity_volatility_7d = stddev(liquidity_7d) / mean(liquidity_7d)
              
              - normalize liquidity_volatility_7d into liquidity_volatility_score in the range [0,1]
              
              - liquidity_stability_score = 1 - liquidity_volatility_score 

&nbsp;&nbsp;**c. Liquidity Distribution**
   - liquidity_distribution_score
              
              - lp_gini = SUM((2 * rank - num_holders - 1) * balance_rank) / (num_holders * SUM(balance))

              - normalize lp_gini into the range of [0,1]

              - liquidity_concentration_score = 0.6 * lp_gini + 0.4 * top1_share

              - liquidity_distribution_score = 1 - liquidity_concentration_score

<br />

&nbsp;&nbsp;**Weights assigned:**
     - Liquidity Depth Score: 0.5
     - Liquidity Stability Score: 0.3
     - Liquidity Distribution Score: 0.2

&nbsp;&nbsp;All metrics are normalized to a 0-1 score, then aggregated with weights into a dimension score for each pool.

<br />
<br />







**(2) Dimension 2: Trade Activity**

&nbsp;&nbsp;**Goal:** To measure whether a pool exhibits consistent, diversified, and economically meaningful trading behavior, rather than activity concentrated in automated or arbitrage patterns. 

<br />

&nbsp;&nbsp;**Metrics used:**

 - **Consistency of Usage**: `swap_days_7d` 

 - **Participation Breadth**: `unique_traders_7d` 

 - **Economic Depth**: `median_daily_volume_7d`

 - **Organic Participation (EOA Share)**: `eoa_like_traders_share`, `eoa_like_volumes_share`
   - eoa_like_traders_share = eoa_like_traders / all_traders
   - eoa_like_volumes_share = eoa_like_volumes / total_volumes

<br />

&nbsp;&nbsp;**Weights assigned:**
   - Usage Consistency Score: 0.25
   - Participation Breadth Score: 0.35
   - Economic Depth Score: 0.3
   - Organic Participation Score: 0.15

&nbsp;&nbsp;All metrics are normalized to a 0-1 score, then aggregated with weights into a dimension score for each pool.

<br />
<br />

**(3) Dimension 3: Market Quality**

&nbsp;&nbsp;**Goal:** To evaluate whether trades in a pool can be executed efficiently and at prices close to the broader market. 

<br />

&nbsp;&nbsp;**Metrics used:**

&nbsp;&nbsp;**a. Price Impact**
 - median_sim_price_impact_7d

&nbsp;&nbsp;**b. Price Efficiency**
 - median_price_deviation_7d 

<br />

&nbsp;&nbsp;**Weights assigned:**
   - Price Impact Score: 0.7
   - Price Efficiency Score: 0.3

&nbsp;&nbsp;All metrics are normalized to a 0-1 score, then aggregated with weights into a dimension score for each pool.

<br />
<br />




#### Step 3 - Dimension Scoring and Ranking
All metrics are normalized to a 0–1 score, then aggregated into dimension scores and an overall pool score.


<br />


### **Key Results**

Key Findings


Visual Analysis


<br />


### **Limitations**

Several limitations should be considered:

Price deviation depends on the quality of the reference price source.

EOA classification approximates organic activity but cannot perfectly separate human users from automated wallets.

The analysis focuses on 7-day metrics, which may not capture longer-term market dynamics.



