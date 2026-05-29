# nba_analysis
Goal: Predict result of NBA Western Conference Finals (May 30)

*CODE WAS GENERATED ENTIRLY WITH CLAUDE*

# 🏀 NBA 2026 WCF Game 7 — Win Probability Analysis

**San Antonio Spurs vs. Oklahoma City Thunder**  
*May 30, 2026 | Paycom Center, Oklahoma City*

---

## Overview

This Databricks notebook builds a composite win probability model for Game 7 of the 2026 NBA Western Conference Finals. After the Spurs forced a winner-take-all game with a dominant 118–91 road win in Game 6, this analysis applies a multi-factor model and renders an analytics dashboard — all in pure Python with no API key required.

---

## Output

![NBA Game 7 Win Probability Dashboard](nba_game7_analysis.png)

The dashboard includes:
- **Composite win probability** donut chart (OKC vs. SAS)
- **Model component breakdown** — how each factor contributes
- **Top scorers** bar chart (series averages through Game 6)
- **Game-by-game score margins** across all 6 games
- **Prediction summary** with spread, total, and key narrative factors

---

## Model

Win probability is a weighted average of four components:

| Component | Weight | Description |
|---|---|---|
| Market odds | 40% | DraftKings moneyline, vig-adjusted to true probability |
| Series performance | 30% | Avg point differential + logistic scaling; SGA slump penalty applied |
| Home court | 20% | Blended all-time G7 home win % (73.6%) with recent conf finals trend |
| Momentum | 10% | Last-3-game win rate + road record for the current playoffs |

**Result: OKC ~59% | SAS ~41%**

---

## Referee Record: Tony Brothers (Section 8)

Section 8 displays OKC's playoff record in games officiated by Tony Brothers across the 2025 and 2026 postseasons (8 games, sourced from ESPN box scores).

> ⚠️ **This is descriptive only and plays no role in the win probability model.**
>
> The 7-1 record is a raw observation, not a validated finding. It has not been tested for statistical significance and should not be interpreted as evidence of referee bias or causal effect. OKC is a dominant team that wins most of its playoff games regardless of who is officiating. Brothers is assigned to high-stakes games between strong teams, which inflates OKC's expected win rate in his games independent of any referee effect.
>
> A valid analysis would require a multivariate regression controlling for team quality, opponent strength, home/away context, and game stakes across a much larger sample — ideally several full seasons of regular season data. Foul differential or free throw disparity would be a more appropriate dependent variable than win/loss outcome. The record is shown here for interest only.

---

## Structure

```
nba_game7_wcf_2026.py
│
├── Section 1  — Install & Import
├── Section 2  — Configuration (CONFIG dict, team colors)
├── Section 3  — Series player averages (hardcoded, NBA.com/ESPN verified)
├── Section 4  — Series results & score margins
├── Section 5  — Win probability model (4 components)
├── Section 6  — Projected scorers & key narrative factors
├── Section 7  — Matplotlib dashboard (5-panel figure)
├── Section 8  — Tony Brothers record (descriptive only, see disclaimer above)
├── Section 9  — Delta table output (Spark write, optional)
└── Section 10 — Summary & interpretation markdown
```

---

## Requirements

```
requests
pandas
numpy
matplotlib
seaborn
```

Install in Databricks:
```python
%pip install requests pandas matplotlib seaborn
dbutils.library.restartPython()
```

---

## Key Storylines Encoded

- **Wembanyama** averaging 28.2 pts / 11.8 reb / 3.0 blk in the series
- **SGA shooting slump** — 4 consecutive games under 40% FG
- **OKC home court** — 6-1 at Paycom Center in the 2026 playoffs; all-time G7 home win rate 73.6%
- **Spurs road momentum** — won 4 of their last 5 road games, including a 27-point blowout in Game 6
- **Jalen Williams healthy** — returned for Game 6 after missing Games 3–5
- **Stephon Castle** — 8th game this postseason with 15+ pts / 5+ reb / 5+ ast

---

## Disclaimer

This notebook is built for educational and portfolio purposes. Win probabilities are illustrative outputs of a simplified model — not financial advice, not betting recommendations.

*Built with Python on Databricks | Data: NBA.com, ESPN, DraftKings, Basketball Reference*
