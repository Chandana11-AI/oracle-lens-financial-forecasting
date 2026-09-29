# OracleLens Time-Series Forecasting Platform

OracleLens is a B2C machine-learning forecasting platform designed to help non-technical users generate future predictions from time-series data without requiring expertise in machine learning.

Users can upload their own CSV datasets or work with financial market data retrieved through APIs such as Alpaca Markets. The backend handles ingestion, validation, preprocessing, forecasting, model evaluation, and reporting through a modular pipeline.

## Project Goals

OracleLens was designed around four core principles:

- forecasting accuracy
- modularity
- leakage prevention
- customer-facing transparency

The goal is to provide reliable forecasts while keeping the user experience simple and protecting proprietary model logic.

## User Workflow

A typical forecasting request follows this flow:

1. Upload a CSV dataset or retrieve market data from a supported API.
2. Validate timestamps, schema, and target variables.
3. Run data-quality and leakage checks.
4. Apply leakage-safe preprocessing.
5. Select or execute an appropriate forecasting model.
6. Generate out-of-sample evaluation metrics.
7. Produce future forecasts.
8. Return predictions and model-performance evidence to the user.

## Forecasting Architecture

The forecasting layer supports multiple time-series models and is designed to allow additional architectures to be integrated over time.

Models explored include:

- LSTM
- GRU
- PatchTST and other transformer-based time-series models

Rather than requiring customers to select a model manually, the platform can automatically choose an appropriate forecasting approach using factors such as:

- forecast horizon
- validated model performance
- historical behaviour
- model stability

This simplifies the customer experience while allowing the underlying model-selection logic to remain proprietary.

## Data Ingestion

OracleLens supports multiple data-entry paths.

### CSV Uploads

Users can provide their own time-series datasets through CSV files.

The pipeline is designed to validate:

- timestamp columns
- chronological ordering
- target-variable availability
- missing observations
- feature consistency
- training and testing boundaries

### Market Data APIs

The platform can also ingest financial-market data through external APIs such as Alpaca Markets.

This allows forecasts to be generated from live or recently retrieved market data without requiring users to prepare files manually.

## Leakage-Safe Preprocessing

Preventing data leakage is a major design requirement of OracleLens.

Time-series models can appear to perform extremely well if future information accidentally enters the training process. To reduce this risk, preprocessing follows causal time-series principles.

Examples include:

- maintaining chronological order
- separating training and testing data by time
- allowing forward filling where appropriate
- avoiding backfilling that may expose future information
- avoiding two-sided interpolation across future observations
- fitting preprocessing operations only on permitted historical data

## Data-Leakage Detection Layer

OracleLens includes a dedicated leakage-validation layer that runs before forecasting.

The audit can evaluate areas such as:

- timestamp integrity
- chronological train/test separation
- target leakage
- suspicious future-looking features
- lookback-window separation
- forecast-horizon separation
- preprocessing scope
- train/test cross-contamination

Critical leakage failures can block a forecasting request rather than allowing potentially misleading results to continue through the pipeline.

## Leakage Audit Report

The leakage-validation layer produces a structured audit report.

Each check can include:

| Field | Purpose |
|---|---|
| Check | Leakage condition being tested |
| Status | Pass or fail |
| Severity | Relative importance of the issue |
| Explanation | Human-readable description |
| Technical Details | Information useful for debugging or auditing |

This provides an auditable record of data-integrity checks before model predictions are generated.

## Model Evaluation

OracleLens is designed to separate model training performance from out-of-sample testing performance.

Evaluation can include metrics such as:

- RMSE
- MAE
- prediction loss or error
- directional accuracy

Directional accuracy is particularly useful in financial forecasting because it measures whether the model correctly predicts the direction of movement rather than only the absolute numerical error.

The system is designed to show customers historical testing evidence alongside future predictions so they can understand how the model behaved on unseen data.

## Customer-Facing Transparency

A key design goal is to provide meaningful evidence of forecast reliability without exposing proprietary model implementations.

Customers can receive:

- future predictions
- historical forecast-versus-actual comparisons
- training metrics
- out-of-sample testing metrics
- directional accuracy
- data-quality results
- leakage-audit status

This creates a more transparent forecasting experience than presenting a prediction alone.

## Modular Design

OracleLens uses a modular architecture so that individual components can evolve independently.

Conceptually, the system can be separated into:

```text
Data Source
    |
    v
Ingestion
    |
    v
Validation
    |
    v
Leakage Audit
    |
    v
Preprocessing
    |
    v
Model Selection
    |
    v
Forecasting
    |
    v
Evaluation
    |
    v
Reporting / API Response
```

This structure makes it easier to:

- add new forecasting models
- introduce additional data sources
- improve validation rules
- change reporting logic
- scale individual services independently

## Technology Stack

The project involves technologies and concepts including:

- Python
- Pandas
- NumPy
- PyTorch
- TensorFlow
- LSTM
- GRU
- PatchTST
- time-series forecasting
- Alpaca Markets API
- REST APIs
- AWS
- data validation
- model evaluation
- leakage detection
- Git and GitHub

## My Contributions

My work on OracleLens included:

- building and benchmarking time-series forecasting models
- working with LSTM, GRU, and transformer-based forecasting approaches
- developing preprocessing workflows for time-series datasets
- implementing chronological train/validation/test strategies
- helping design controls to prevent data leakage
- contributing to model-evaluation workflows using RMSE, MAE, and directional accuracy
- working with API-based financial-market data ingestion
- contributing to backend and REST API components
- supporting architecture and AWS deployment planning
- translating model-performance results into information that could be understood by non-technical users

## Business Value

OracleLens is designed to reduce the technical barrier between machine-learning forecasting and end users.

Instead of requiring customers to understand:

- model architectures
- hyperparameters
- train/test methodology
- feature engineering
- forecasting libraries

the platform handles those processes internally and returns a simpler output:

- the forecast
- evidence of historical model performance
- data-quality and leakage checks
- enough context for the user to judge the result responsibly

## Current Status

The repository documents the architecture and design principles of the OracleLens forecasting platform.

Future public additions may include:

- sanitized pipeline examples
- sample datasets
- model benchmarking results
- leakage-audit examples
- API request and response examples
- architecture diagrams
- forecast visualizations
- unit and validation tests

Proprietary model logic, production credentials, private datasets, and sensitive deployment configuration are intentionally excluded from this public repository.

## Skills Demonstrated

Time-Series Forecasting | Data Analysis | Machine Learning | Deep Learning | LSTM | GRU | Transformers | PatchTST | Python | Data Pipelines | REST APIs | AWS | Model Evaluation | Data Validation | Data-Leakage Prevention | Financial Data
