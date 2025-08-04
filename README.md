# 📈 📦 Long Reactive Beta - Quantitative Strategy

This project explores long only quantitative equity strategy inspired by the rumored **"Long Reactive Beta, Short Low Beta"** setup speculated to be part of **RenTech** multifactor framework.

Now, here in Indonesia, since short selling isn't fully available yet, we decided to test the strategy from just the long side, basically going Long on Reactive Beta stocks only, to see if it's still promising.

---

### 🧠 Strategy Concept

The strategy selectively goes **long on reactive beta stocks**, operating under the assumption that stocks with higher sensitivity to market moves may offer **enhanced upside in risk on regimes**.

No fundamentals enter the equation. That means no earnings reports, no financials, no projections, no margins, no ROI, nothing from statements. Our model is purely behavioral, operating on liquidity and beta alone.

This is **not a stock picker’s strategy**, we trust the system. If a company is a zombie with negative equity but meets the quantitative criteria, it gets included. No human override at all.

We use basic risk management, 10% stop-loss. The logic spans two dates: current date (x) and next date (x+1). If a stock is flagged on x for entry on x+1, we model the buy price as x close + x+1 open. If that’s 100 and next date low price hits below 90, we close the trade on 90.

**No hyperparameter games. No tuning for backtest glory. We’re here to validate one idea: Is beta reactivity a reliable upside signal during bullish phases?**

---

### 🔧 Setup
- **Market**:  Jakarta Composite Index (JCI) 
- **Universe Filter**:  
  - Median turnover > IDR 10B (last 1800 daily bars)  
  - Tradable stocks with continuous price data  
- **Beta Calculation**: Rolling beta to JCI (Jakarta Composite Index), using specific windows  
- **Weighting Scheme**: Linear decayed weight by beta score (50%) + liquidity adjustment (50%)  
- **Tools**: Python / Jupyter Notebook  
- **Data Source**: Bloomberg Finance LP, Arief Aulia Rakhman  
- **Execution Assumption**: Average of this week’s close and next week’s open (to account for slippage)

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

(📷 *Backtest chart here*)

**Results** 
| Metric                    | Value            |
|---------------------------|------------------|
| **Period**                | 2010-01-01 to 2025-08-01 |
| **Initial Balance**       | Rp1,000,000       |
| **Final Balance**         | Rp697,941,450     |
| **Total Return**          | 66,371.49%        |
| **Annualized Return**     | 54.23%            |
| **Annualized Volatility** | 46.58%            |
| **Sharpe Ratio**          | 1.16              |
| **Max Drawdown**          | -27.25%           |
|                           |                  |
| **Benchmark Return**      | 144.59%         |
| **Benchmark Max Drawdown**| -31.29%           |
| **Total Alpha**           | 66,226.89%        |
| **Annualized Alpha**      | 54.21%            |

---

### 🔍 Strategic Observations

- The **long-only reactive beta** works surprisingly well in a market where shorting isn't fully enabled.
- Even though this is a one legged strategy (no hedging), it **consistently outperformed the index**.

---

### 🛠️ Realism Adjustments

- **Slippage accounted for** via average execution between week-close and next-week open  
- **No survivorship bias** — delisted names remain in the universe if they had sufficient liquidity  
- **No manual screening** — model output is respected regardless of business fundamentals  

---

### 🎯 Objective

To test whether **a simplified version of a RenTech beta-tilt strategy** can still deliver alpha in a restricted market environment like Indonesia, using only long positions.

---

📁 **Note:**  
The Jupyter notebook containing the full backtest is private.  
Feel free to reach out via email for access.  
📧 [ariefauliaa@gmail.com]
"""
