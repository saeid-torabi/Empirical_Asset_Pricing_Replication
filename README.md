📈 Machine Learning in Asset Pricing: A LightGBM Implementation
Author: Saeid Torabi

This repository contains my first major project in the field of Empirical Asset Pricing, one of the most complex and high-stakes applications of Machine Learning in Finance. The project implements a high-dimensional cross-sectional equity strategy based on the methodology of Gu, Kelly, and Xiu (2020), adapted for modern gradient boosting frameworks.


🚀 Project Overview
The goal of this project is to capture the non-linear risk premia of individual stocks by interacting 94 firm-level characteristics with 8 macroeconomic state variables. Unlike traditional linear models (OLS), this approach allows the model to capture how stock features (like Momentum or Value) behave differently across various economic regimes (e.g., high inflation or low interest rates).

Key Technical Achievements:
    ⦿ Massive Feature Engineering: Expanded the base characteristic set into over 1,000 interaction features.
    ⦿ Memory-Efficient Ranking: Implemented a monthly cross-sectional ranking system to ensure all features are stationary and mapped to a $[-1, 1]$ interval.
    ⦿ Walk-Forward Validation: Built an expanding window training loop from 1962 to 2021 to ensure strictly out-of-sample testing.


🛠️ Data Strategy & Challenges
Finding clean, institutional-grade data without access to CRSP/Compustat was the most significant hurdle of this project.
    ⦿ The Source: Fundamental characteristics were sourced from the original authors' website.
    ⦿ The Pivot: Since I did not have CRSP access, I developed a custom pipeline to pull stock price information via the Yahoo Finance API.
    ⦿ The Pruning: Merging disparate datasets is notoriously difficult in finance. After calculating excess returns, handling delistings, and pruning for data quality, the dataset was reduced from nearly 4 million rows to a high-quality subset of ~135,000 observations.


🤖 The Model: LightGBM
While the original paper explores various architectures (including Neural Networks), I chose LightGBM for its efficiency and ability to handle high-dimensional, low signal-to-noise data.

The Learning Curve Challenge
One of the hardest parts of financial ML is getting a model to converge. Because stock returns are incredibly noisy, learning curves often appear "flat" or "underfit." Despite these challenges, I managed to extract a kind of stable signal (tried Optuna for hyperparameter tuning; but sadly wasn't successful like those projects I did in credit risk analysis and fraud detection).


📊 Results
The model achieved a significant monotonic spread across predicted deciles, mostly successfully separating the winners from the losers in the cross-section.

Annualized Sharpe Ratio: 2.05 (for the 2021 test year).

Monthly Long-Short Spread: 3.15%.

Note: While I am satisfied with achieving these results in my first project, I am still refining the model and do not consider these results "final."

🧠 Lessons Learned
This project was an immense learning experience that taught me:
    ⦿ Data is 90% of the Work: The time spent on cleaning, merging, and shifting macro features far outweighed the time spent training models.
    ⦿ Stationarity is Non-Negotiable: Without cross-sectional ranking ($[-1, 1]$), the model fails to converge because the scale of macro variables overwhelms the firm characteristics.
    ⦿ The Perils of Over-Regularization: In finance, there is a fine line between a model that ignores noise and a model that is "strangled" by penalties and fails to learn anything at all.


🔮 Future Directions
This is just the beginning. While I am leaving the project in its current state for now, I plan to explore much bigger things in the future, including:

    ⦿ Integrating SHAP values for deeper economic interpretability.
    ⦿ Exploring Neural Networks (MLP/Transformers) for time-series forecasting.
    ⦿ Developing more robust liquidity filters to account for real-world transaction costs.