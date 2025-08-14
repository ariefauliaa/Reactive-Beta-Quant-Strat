# 📈 📦 Long Reactive Beta - Quantitative Strategy

This project explores long only quantitative equity strategy inspired by the rumored **"Long Reactive Beta, Short Low Beta"** setup speculated to be part of **RenTech** multifactor framework.

Now, here in Indonesia, since short selling isn't fully available yet, we decided to test the strategy from just the long side, basically going Long on Reactive Beta stocks only, to see if it's still promising.

Also, we’ve been closely studying several EM country sub indices and their rebalancing methodologies. Interestingly, some seem to mimic a similar approach, even if not explicitly stated. Since this setup appears effective in other emerging markets, we’re testing it on Indonesian stocks, hence this repo!

---

### 🧠 Strategy Concept

- Strategy takes top n stocks ranked by a 50/50 weighted score: reactive beta (50%) and value traded (50%). The core assumption is market movements are stationary: high-beta stocks this week/month/quarter likely remain high-beta next week/month/quarter. Stocks don’t abruptly lose momentum; decay is gradual.

- No earnings growth, no ROE, no balance sheets. We ask only two questions:

1. ***Easy to buy?***

2. ***Easy to sell?***

If the answer is yes to both, and the stock meets the beta threshold, we buy it. Even if it has negative equity or other red flags, we still buy it. For example, if tickers A, B, and C qualify, and C has negative equity, we still buy A, B, and C.

- Use a simple stop loss rule: 10% below the entry price. Let’s say today is day x, and ticker is flagged for entry on day x+1. If we enter at 100 IDR, and next day’s low hits 90 or below, we exit at 90.

- **No hyperparameter tuning. We don't game backtests.** Adjustments are minimal, focused only on:

1. Interval granularity (daily / weekly / monthly / quarterly)

2. Turnover thresholds (to ensure tradeability)

These tweaks are practical, not optimized for historical performance. It’s about making the strategy scalable, especially if used by larger capital pools. A small-cap fund might not face slippage, but a big fund will. The longer the interval, the more time to accumulate or exit.

---

### 🔧 Setup
- **Market**:  Jakarta Composite Index (JCI) 
- **Filter**:  Median turnover & tradable stocks with continuous price data  
- **Beta Calculation**: Rolling beta to JCI (Jakarta Composite Index), using specific windows  
- **Weighting Scheme**: Linear decayed weight by beta score (50%) + liquidity adjustment (50%)  
- **Data Source**: Bloomberg Finance LP, Arief Aulia Rakhman  
---

### 📊 Portfolio Construction Logic

When a basket of stocks is selected, weights are distributed **gradually and linearly**, as shown below:

| Rank | Weight (%) |
|------|------------|
| 1    | 18.18%     |
| 2    | 16.36%     |
| 3    | 14.55%     |
| 4    | 12.73%     |
| 5    | 10.91%     |
| 6    | 9.09%      |
| 7    | 7.27%      |
| 8    | 5.45%      |
| 9    | 3.64%      |
| 10   | 1.82%      |
| **Total** | **100%** |

This ensures **heavier exposure to the highest reactive beta & most liquid names**, and progressively less to lower ranked selections.

---

### 📈 Backtest Performance Summary

![Backtest Preview](Backtest%20-%20Preview.png)

**Results** 
| Metric                    | Value            |
|---------------------------|------------------|
| **Period**                | 2010-01-01 to 2025-08-01 |
| **Initial Balance**       | Rp1      |
| **Final Balance**         | Rp679    |
| **Total Return**          | 64,534.34%        |
| **Annualized Return**     | 53.94%            |
| **Annualized Volatility** | 46.59%            |
| **Sharpe Ratio**          | 1.16              |
| **Max Drawdown**          | -27.25%           |
|                           |                  |
| **Benchmark Return**      | 142.36%         |
| **Benchmark Max Drawdown**| -31.29%           |
| **Total Alpha**           | 64,391.98%        |
| **Annualized Alpha**      | 53.92%            |

---

### 📈 Live Result

Some of you might be wondering "Is this backtest performance even realistic? Could it be overfitting? Data leakage?" We had the same doubts.

To challenge our own assumptions, we rebuilt the strategy **6 separate times from scratch, ran the backtests again, and then took it live.**

The live results were remarkable: over 16 live data points, the strategy delivered +49.72% cumulative performance.

![Live Result Preview](Live%20Result%20-%20Preview.png)

Left chart → live overall performance, right table → current live holdings performance

Note: The live and backtest curves won’t perfectly match. The backtest chart is resampled to yearly performance, while the live result is displayed at a shorter time horizon.

---

### 🔮 Stress Test - Monte Carlo Simulation

![Monte Carlo Preview](Monte%20Carlo%20-%20Preview.png)

We conducted **Monte Carlo simulation** to forecast performance over the **next 3 years (36 months)** using historical monthly returns and volatility as inputs. This provides a probabilistic view of potential future outcomes for the strategy.

**Parameters**  
| Parameter                         | Value         |
|----------------------------------|---------------|
| Simulation periods               | 36 months     |
| Number of simulations            | 500           |

**Results**  
| Metric                            | Value         |
|----------------------------------|---------------|
| Mean final cumulative return     | 358.22%       |
| Median final cumulative return   | 250.73%       |
| Top 5% outcome                   | 1006.95%      |
| Bottom 5% outcome                | -0.31%        |
| Probability of positive return   | 94.8%         |

**Monte Carlo Interpretation:**

The simulation paints a very optimistic picture. Over a 3-year horizon:

- You have **94.8% probability** of finishing with **positive return**.
- The **average return** is **358.22%**, implying **CAGR of ~65.4%**, which is extraordinarily aggressive.
- Even in the bottom 5% of outcomes, the loss is negligible at just **-0.31%**, while the top 5% result exceeds **1000%**, suggesting significant upside potential.

**Monte Carlo: Metaphorical Visualization**

You face 100 doors. 95 hide treasure; 5 hold nothing.  

**Rule 1:** Open as many as you can. Expected value = 95% success.  

Then the room master offers: *"Want another round? 1 more door? 5? 50?"*  

**Answer:** Always yes.  
- *1 extra door*: 95% → 95.05% EV (100 → 101 doors).  
- *50 extra doors*: 95% → 95.45% EV (100 → 150 doors).  

**Why?**  
- The base rate (95%) dominates. More trials = convergence to true odds.  
- Even with diminishing returns (95/100 → 142/150), the marginal gain is *always positive*.  

---

### 🔍 Observations

- The **long-only reactive beta** works surprisingly well in a market where shorting isn't fully enabled.
- Even though this is a one legged strategy, it **consistently outperformed the index**.

---

### 🎯 Objective

To test whether **a simplified version of a RenTech beta-tilt strategy** can still deliver alpha in a restricted market environment like Indonesia, using only long positions.

---

📁 **Note:**  
The Jupyter notebook containing the full backtest is private.  
Feel free to reach out via email for access.  
📧 [ariefauliaa@gmail.com]
