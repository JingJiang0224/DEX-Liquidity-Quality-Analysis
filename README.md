# On-Chain Trading Data: DEX Liquidty Quality Analysis



**Authour**: Jing Jiang

**Date**: Nov 2025 - Feb 2026

**Data Source**: On-chain trading data from Uniswap V2

**Tools**: Dune Analytics, SQL

**Link of Dashboard**: link

**Link of Code**: link



<br />
<br />



### Research Question 
Which liquidity pools on Uniswap V2 provide the **highest market quality**?

<br />



### Introduction

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


### **Methodology**
Each pool is evaluated across three dimensions.

1. Liquidity Quality
Measures whether a pool provides sufficient and stable liquidity.

2. Trade Activity
Measures whether a pool is consistently used by diverse traders.

3. Price Quality
Measures trading efficiency and price accuracy.

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



