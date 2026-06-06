# Deep Reinforcement Learning for Quantitative Trading using Sentiment Analysis and Volatility

## Project Overview

This repository explores the application of Deep Reinforcement Learning (DRL) algorithms to optimize stock trading strategies. Specifically, it investigates how integrating financial news sentiment and sentiment-derived volatility can influence the learning process and profitability of DRL agents.

The core objective is to evaluate whether providing structural sentiment signals as part of the state space enhances the decision-making capabilities of trading agents in simulated environments.

## Trading Agents Evaluated

We benchmarked three distinct continuous-action reinforcement learning algorithms:
- **Advantage Actor-Critic (A2C)**
- **Proximal Policy Optimization (PPO)**
- **Twin Delayed Deep Deterministic Policy Gradient (TD3)**

## Experimental Configurations

To isolate the impact of sentiment features, we structured the evaluation into four progressive scenarios:

1. **Baseline Environment**: Utilizing only standard technical indicators and historical price data.
2. **Raw Sentiment Integration**: Appending unprocessed news sentiment scores directly into the state space.
3. **Refined Sentiment Integration**: Applying Exponential Moving Average (EMA) and normalization to smooth out the sentiment signals before providing them to the agent.
4. **Sentiment & Volatility Integration**: Combining refined sentiment scores with calculated sentiment standard deviation (volatility) to reflect market uncertainty.

---

## Dataset and Environment

- **Historical Market Data**: Sourced from Yahoo Finance.
- **Financial News Corpus**: Utilized a comprehensive financial news dataset.
- **Sentiment Extraction**: FinBERT was employed to generate sentiment polarity scores.
- **RL Framework Setup**: The environments and agents are built utilizing stable-baselines3 and custom trading environment wrappers.
- **Initial Capital**: $1,000,000 simulated account balance.

---

## Key Performance Indicators (KPIs)

### Portfolio Value Comparison (Final Values)

| Algorithm | Baseline (No SA) | Raw SA | Refined SA | Refined SA + Volatility |
|-----------|------------------|--------|------------|-------------------------|
| **A2C**   | $1,528,590       | $2,040,000 | $1,640,656 | $1,554,927 |
| **PPO**   | $1,196,072       | $1,344,424 | $1,172,948 | $996,754   |
| **TD3**   | $1,457,936       | $1,730,000 | **$1,791,986** | $1,384,668 |
| **DJIA Baseline** | $1,138,028 | $1,138,028 | $1,138,028 | $1,138,028 |

### Risk-Adjusted Returns (Cumulative Return / Sharpe Ratio)

| Algorithm | Baseline (No SA) | Raw SA      | Refined SA  | Refined SA + Volatility |
|-----------|------------------|-------------|-------------|-------------------------|
| **A2C**   | 0.53 / 1.52      | 0.67 / 2.38 | 0.64 / 2.36 | 0.55 / 1.71             |
| **PPO**   | 0.20 / 1.42      | 0.34 / 1.56 | 0.17 / 1.69 | 0.00 / –0.11            |
| **TD3**   | 0.46 / 1.69      | 0.72 / 2.42 | **0.79 / 2.82** | 0.38 / 1.88         |
| **DJIA Baseline** | 0.14 / 1.20 | 0.14 / 1.20 | 0.14 / 1.20 | 0.14 / 1.20 |

---

## Core Findings

- The **TD3 agent** consistently demonstrated the most reliable improvement when augmented with refined sentiment data, yielding the highest risk-adjusted returns.
- The **A2C agent** exhibited improved cumulative returns when sentiment was introduced, although it struggled to effectively leverage the volatility signal.
- The **PPO agent** proved to be highly sensitive to the added dimensionality and noise of sentiment and volatility, often resulting in degraded stability and performance.
- Interestingly, the addition of **sentiment volatility** generally acted as detrimental noise across all evaluated models, leading to suboptimal policy convergence compared to purely refined sentiment.

---

## Repository Structure

```
├── README.md
├── baseline_agents/                          # Experiments with purely technical data
│   ├── Baseline_RL_Trading_Agent.ipynb
│   └── ...
├── sentiment_aware_agents/                   # Experiments incorporating raw sentiment
│   ├── Sentiment_Aware_RL_Agent.ipynb
│   └── ...
├── refined_sentiment_models/                 # Experiments with smoothed and normalized sentiment
│   ├── Refined_Sentiment_RL_Agent.ipynb
│   └── ...
├── volatility_sentiment_models/              # Experiments integrating sentiment standard deviation
│   ├── Volatility_Sentiment_RL_Agent.ipynb
│   └── ...
└── report/
    └── [Visualizations and Results]
```

---

## References

1. FinBERT: A Pretrained Language Model for Financial Communications
2. Stable-Baselines3: Reliable Reinforcement Learning Implementations
3. Giving Content to Investor Sentiment: The Role of Media in the Stock Market
4. Deep Reinforcement Learning for Automated Stock Trading
