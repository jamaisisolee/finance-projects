# Finance with Big Data: PC Labs

Four empirical finance projects from **20598 Finance with Big Data** (Bocconi University, 2026). They move from classic portfolio theory and asset pricing to NLP on social media and machine-learning return prediction. Each lab is a self-contained Jupyter notebook with a written analysis. Each folder's README summarizes the question, the method and the main findings.

| # | Lab | Question | Main methods | Headline finding |
|---|---|---|---|---|
| 1 | [Markowitz Portfolio Optimization](lab1-markowitz-portfolio/) | Can a mean–variance portfolio of 8 US stocks beat the S&P 500? | Monte Carlo portfolios, efficient frontier (SLSQP), out-of-sample test, annual rebalancing | In-sample Sharpe 1.46 falls to 1.12 out of sample; a naive 1/N portfolio beats yearly re-optimization |
| 2 | [Testing the CAPM](lab2-capm/) | Does beta explain returns? | OLS + HAC errors, residual diagnostics, rolling betas, Fama–French (2004) beta deciles, Fama–MacBeth, GRS test | Beta is precise and higher-beta portfolios earn more, but the CAPM misses single-stock annual returns by about 25 pp |
| 3 | [StockTwits Sentiment & Attention](lab3-stocktwits-sentiment/) | Do 5.5M StockTwits messages tell us anything about returns? | FinBERT / Twitter-RoBERTa / FinTwitBERT / LLM (gpt-oss-120b), text cleaning, word clouds, abnormal-attention factor, FF5 | Sentiment tracks same-day returns (ρ = 0.27) but not next-day returns; abnormal attention does not predict returns |
| 4 | [ML Return Prediction](lab4-ml-return-prediction/) | Can price and volume signals predict 5–60-day returns, and is the resulting portfolio profitable? | OLS, Ridge, logit, gradient boosting, random forest, neural network, GAM, ensembles; purged chronological split; backtest with costs | Predictability is tiny (< 1 pp R²<sub>OOS</sub>); the AI portfolio does not beat the market on a risk-adjusted basis |

## Common themes

- **In-sample vs out-of-sample.** Every lab tests whether a result estimated on one period survives on another. Usually it shrinks, and sometimes it reverses (Lab 1 weights, Lab 4 validation winners).
- **Estimation error.** Noisy inputs such as expected returns, betas and model hyperparameters drive many of the failures. Simple, diversified or heavily regularized choices tend to win.
- **Statistical honesty.** We use HAC/Newey–West standard errors, non-overlapping test dates, placebo and random-portfolio benchmarks, and survivorship-free CRSP data, and we report negative results explicitly.

## Repository structure

```
.
├── lab1-markowitz-portfolio/
│   ├── PCLab1_Markowitz_Portfolio.ipynb
│   ├── README.md
│   └── figures/
├── lab2-capm/
│   ├── PCLab2_CAPM.ipynb
│   ├── README.md
│   └── figures/
├── lab3-stocktwits-sentiment/
│   ├── PCLab3_StockTwits_Sentiment.ipynb
│   ├── README.md
│   └── figures/
├── lab4-ml-return-prediction/
│   ├── PCLab4_ML_Return_Prediction.ipynb
│   ├── README.md
│   └── figures/
├── requirements.txt
└── .gitignore
```

## Data policy

**No data is included in this repository.**

- The course datasets (stock prices and volumes, StockTwits messages) are course material and are not redistributed.
- CRSP data comes from WRDS under a university licence and cannot be shared.
- The notebooks for Labs 3 and 4 are published **with outputs cleared**. In Lab 2, outputs that displayed raw CRSP rows were removed. The `figures/` folders contain only aggregate results.
- Public sources used by the notebooks (Yahoo Finance via `yfinance`, the Fama–French factors from Ken French's data library, and the StockEmotions dataset) are downloaded at run time.

Each lab README lists the exact files a notebook expects. To re-run a lab, place those files next to its notebook. `.gitignore` blocks common data formats so they cannot be committed by accident.

## Running the notebooks

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter lab
```

Lab 3 runs transformer models (a GPU helps but is not required). Its LLM steps need a free Groq API key, which the notebook asks for with a hidden prompt; you can also set it beforehand with `export GROQ_API_KEY=...`. API keys are never stored in the notebooks.

## Team

Group 7: **Cecilia Lo Cicero, Sara Pulidori, Alissa Sharuda, Nico Visentin**

Course: 20598 Finance with Big Data, Bocconi University.

## License

The code and written analysis are released under the [MIT License](LICENSE). This does not cover any data: the datasets keep their original terms (see [Data policy](#data-policy)).
