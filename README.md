# 📈 📦 Long Reactive Beta - Quantitative Strategy

This project explores long only quantitative equity strategy inspired by the rumored **"Long Reactive Beta, Short Low Beta"** setup speculated to be part of **RenTech** multifactor framework.

We’ve observed that one of the EM country indices may be quietly applying a similar methodology. It’s not publicly confirmed, but the structure and character of that index seem to mimic this approach too closely to ignore.

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
- **Filter**:  
  - Median turnover > IDR 10B (last 1800 daily bars)  
  - Tradable stocks with continuous price data  
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

### 🔮 Stress Test - Monte Carlo Simulation

![Monte Carlo Preview](Monte%20Carlo%20-%20Preview.png)

We conducted a **Monte Carlo simulation** to forecast performance over the **next 3 years (36 months)** using historical monthly returns and volatility as inputs. This provides a probabilistic view of potential future outcomes for the strategy.

**Parameters**  
| Parameter                         | Value         |
|----------------------------------|---------------|
| Historical mean monthly return   | 4.3721%       |
| Historical monthly volatility    | 13.4502%      |
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

- You have a **94.8% probability** of finishing with a **positive return**.
- The **average return** is **358.22%**, implying a **CAGR of ~65.4%**, which is extraordinarily aggressive.
- Even in the bottom 5% of outcomes, the loss is negligible at just **-0.31%**, while the top 5% result exceeds **1000%** — suggesting significant upside potential.

To visualize it metaphorically:

> Imagine flipping a coin where **it lands in your favor 95 out of 100 times**. That’s what this strategy's forward outlook looks like — skewed heavily toward success.
"""

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
