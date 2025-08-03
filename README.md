# 📈 Long High Beta Strategy – IDX Quant Backtest

This project explores a long-only quantitative equity strategy inspired by the rumored **"Long High Beta, Short Low Beta"** setup speculated to be part of **RenTech** multifactor framework.

Since **shorting isn't fully available** in the Indonesian equity market, this model focuses purely on **long exposure to high beta stocks**, aiming to assess if the strategy holds water on its own without the short leg.

---

### 🧠 Strategy Concept

The strategy selectively goes **long on high beta stocks**, operating under the assumption that stocks with higher sensitivity to market moves may offer **enhanced upside in risk on regimes**.

We don’t touch fundamentals; no earnings and no balance sheet filters. The model is strictly **market behavior driven**, relying only on liquidity and beta.

This is **not a stock picker’s strategy**, we trust the system. If a company is a zombie with negative equity but meets the quantitative criteria, it gets included. No human override.

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

This ensures **heavier exposure to the highest beta & most liquid names**, and progressively less to lower ranked selections.

---

### 📈 Backtest Performance Summary

(📷 *Backtest chart here*)

| Metric                    | Value              |
|---------------------------|--------------------|
| **Period**       | 2010-08-01 to 2025-08-01 |
| **Initial Capital**       | Rp1,000,000         |
| **Final Balance**         | RpXX,XXX,XXX        |
| **Total Return**          | XX,XXX%             |
| **Annualized Return**     | XX.XX%              |
| **Annualized Volatility** | XX.XX%              |
| **Sharpe Ratio**          | X.XX                |
| **Max Drawdown**          | -XX.XX%             |
| **Benchmark**             | Jakarta Composite Index (JCI) |
| **Annualized Alpha**      | ~12.47%             |

> 📌 *Alpha is calculated against JCI over a 5-year backtest.*

---

### 🔍 Strategic Observations

- The **long-only beta tilt** works surprisingly well in a market where shorting isn't fully enabled.
- Even though this is a one-legged strategy (no hedging), it **consistently outperformed the index**.
- There's anecdotal alignment with **certain EM index movements**, possibly reflecting similar structural exposures.
- The **beta premium** seems alive and well in IDX — at least for liquid names.

---

### 🛠️ Realism Adjustments

- **Slippage accounted for** via average execution between week-close and next-week open  
- **No survivorship bias** — delisted names remain in the universe if they had sufficient liquidity  
- **No manual screening** — model output is respected regardless of business fundamentals  

---

### 🎯 Objective

To test whether **a simplified version of a hedge fund beta-tilt strategy** can still deliver alpha in a restricted market environment like Indonesia, using only long positions.

---

📁 **Note:**  
The full Jupyter notebook with all code, functions, and chart outputs is currently **private**.  
For access or discussion, feel free to reach out via email.  
📧 [ariefauliaa@gmail.com]
"""

# Save to a file
readme_path = Path("/mnt/data/README.md")
readme_path.write_text(readme_content.strip())

readme_path

