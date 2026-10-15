# OracleLens: Time-Series Forecasting Platform

An industry-sponsored capstone exploring how non-technical users can request time-series forecasts and inspect the evidence behind them.

**Context:** OracleLens collaboration, September 2025–April 2026, Toronto.  
**My focus:** applied forecasting, preprocessing and leakage controls, model evaluation, financial-data integration and backend/cloud contributions.  
**Public repository:** technical case study. Application source, model weights and deployment configuration are not included.

## User problem

A forecast is hard to assess when the user sees only a predicted line. OracleLens was designed to pair forecasts with historical testing evidence, data-quality checks and explanations of preprocessing decisions.

Users could work with uploaded CSV data or financial-market data retrieved through Alpaca Markets. The broader design connects ingestion, validation, forecasting, evaluation and reporting through backend APIs.

## End-to-end workflow

1. **Ingest:** accept a time-series CSV or retrieve market observations.
2. **Validate:** check timestamps, target columns, missing data and chronological order.
3. **Audit:** identify conditions that could leak future information.
4. **Preprocess:** prepare causal inputs and fit learned transformations within training boundaries.
5. **Train/evaluate:** benchmark forecasting approaches on chronological partitions.
6. **Predict:** produce a forecast for the requested horizon.
7. **Report:** return predictions with out-of-sample errors, direction metrics and audit information.

## My contributions

My work included:

- Developing and benchmarking time-series forecasting models across multiple horizons.
- Preparing multi-source financial data and integrating Alpaca Markets data.
- Building preprocessing workflows and chronological train/validation/test strategies.
- Contributing controls for missing values, scaling and data-leakage prevention.
- Evaluating forecasts using RMSE, MAE and directional accuracy.
- Designing REST API components and contributing to backend/system integration.
- Supporting AWS deployment and investigating integration/deployment issues.
- Explaining model-performance results in terms useful to non-technical stakeholders.

This was a team collaboration. These contributions describe my work within the project, rather than sole ownership of the complete product.

## Architecture and interfaces

| Component | Responsibility | Important boundary |
|---|---|---|
| Ingestion | CSV inputs and external market-data retrieval | Validate schema and data availability |
| Validation | Timestamp order, target selection, missing observations and duplicates | Reject or explain unsuitable inputs |
| Preprocessing | Causal filling, scaling and window generation | Fit transformations on training history |
| Forecasting | Multiple horizon/model experiments | Model choice requires empirical validation |
| Evaluation | Chronological out-of-sample comparisons | Keep backtests distinct from future forecasts |
| Reporting/API | Predictions, metrics and audit explanations | Avoid presenting uncertainty as certainty |
| Cloud/backend | Model serving and application integration | Deployment details are not published here |

The case study describes design boundaries, not a complete service contract or executable architecture.

## Leakage prevention

Time-series evaluation can look strong when future observations accidentally influence training. The project emphasized:

- Sorting and checking timestamps before constructing windows.
- Chronological train/validation/test separation.
- Forward filling only where appropriate; avoiding backfill from future observations.
- Fitting scalers on training data rather than the full dataset.
- Reviewing lookback windows, forecast horizons and label alignment.
- Checking for suspicious future-looking features and cross-partition contamination.
- Recording problems in an audit output rather than silently accepting invalid inputs.

An audit record can identify the check, status, severity and explanation. The current public repository does not contain the audit implementation or a test suite, so these design descriptions should not be read as independently verified coverage of every leakage scenario.

## Model development and evaluation

The project explored recurrent and transformer-based time-series approaches, including LSTM and PatchTST. Different forecast horizons and configurations were investigated.

Evaluation considered:

| Metric | What it answers |
|---|---|
| MAE | How large is the average absolute forecast error? |
| RMSE | How strongly are larger errors penalized? |
| Directional accuracy | How often does predicted movement match actual movement under the chosen definition? |
| Forecast-versus-actual plots | Where do timing, trend and magnitude diverge? |

A meaningful result needs its dataset, date range, split boundaries, horizon, baseline and preprocessing configuration. No benchmark table is published because this repository does not include the matching logs and artifacts required to substantiate one.

Model selection based on horizon, validation performance and stability is a design direction; this page does not claim a verified automated selector or that every explored model was deployed successfully.

## Reliability and user communication

A useful forecasting interface should show:

- Which observations were used.
- What preprocessing changed.
- Whether validation found data-quality or leakage concerns.
- How the selected configuration behaved on unseen historical observations.
- How future predictions differ from measured historical results.

Financial forecasts remain uncertain. A small numerical error does not necessarily imply useful directional performance, and backtest results do not guarantee future outcomes.

## Technology and engineering skills

Python, pandas, NumPy, PyTorch, time-series modeling, Alpaca Markets, REST APIs, AWS, model evaluation, data validation, Git/GitHub and technical documentation.

My contribution combined modeling with integration: preparing inputs, evaluating outputs and connecting model workflows to a user-facing system.

## What is publicly available

This repository currently contains this case study only. It is **not an installable release or a running public demo**.

A useful next public revision would add a sanitized synthetic example, documented request/response shapes, audit examples, evaluation logs and small validation tests, subject to project-sharing permissions. No confidential data, credentials, private infrastructure identifiers or proprietary model implementation is published.

## Interview discussion points

- How chronological splits differ from random train/test splits.
- Why scaler fitting and backfilling can leak information.
- How lookback length and prediction horizon affect evaluation.
- Why RMSE and directional accuracy answer different questions.
- How backend validation makes model behavior easier to explain.
- What was implemented, evaluated, deployed or left as a design proposal.
