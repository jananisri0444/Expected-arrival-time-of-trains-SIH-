# Tools & Libraries Referenced in the Model / System Design

## Machine Learning

- **LightGBM** — gradient boosting framework, primary model choice for the delay-propagation regression (fast on tabular data, native quantile-regression objective for uncertainty bands).
  https://lightgbm.readthedocs.io/

- **XGBoost** — alternative/comparison gradient boosting framework.
  https://xgboost.readthedocs.io/

- **scikit-learn** — baseline models (linear regression, random forest) and standard train/test/evaluation utilities.
  https://scikit-learn.org/

- **PyTorch** — recommended framework if/when the project extends to the stretch-goal sequence model (LSTM/GRU/Temporal Fusion Transformer).
  https://pytorch.org/

## Data Engineering / Pipeline

- **Apache Airflow** — suggested scheduler/orchestrator for the NTES polling pipeline and periodic model retraining.
  https://airflow.apache.org/

- **PostgreSQL / TimescaleDB** — suggested structured storage for cleaned, time-stamped train-running records.
  https://www.postgresql.org/ · https://www.timescale.com/

## Serving / API

- **FastAPI** — suggested framework for the ETA prediction REST API layer.
  https://fastapi.tiangolo.com/

- **Docker / Docker Compose** — containerization and MVP-scale orchestration for the poller, ETL, model server, and API components.
  https://docs.docker.com/compose/

## Dashboard / Frontend

- **Streamlit** — suggested for a fast MVP/demo dashboard (train search, live progress, predicted vs. scheduled ETA).
  https://streamlit.io/
- **React** — suggested for a production-grade dashboard if the project extends beyond demo stage.
  https://react.dev/
