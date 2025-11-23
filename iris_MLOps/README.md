# MLOps Iris Example

This repository contains a minimal MLOps example built around the Iris dataset using scikit-learn and MLflow.

## Project Structure

- `train_model.py` – trains a Logistic Regression classifier on the Iris dataset, logs metrics and the model to an MLflow tracking server.
- `requirements.txt` – Python dependencies.
- `app/` – application code (e.g. FastAPI/Flask) that can load and serve the trained model.
- `mlruns/`, `mlartifacts/`, `models/` – MLflow tracking, artifacts, and registered models output directories (created after running training).
- `mlops/` – local Python virtual environment (created with `python -m venv`).

## Prerequisites

- Python 3.8+
- Linux (tested) or any OS supported by Python & MLflow

## Setup

1. Create and activate a virtual environment (optional):

   ```bash
   python3 -m venv mlops
   source mlops/bin/activate
   ```

2. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

## Running the Training Script

1. Make sure an MLflow tracking server is running at `http://localhost:5000`, for example:

   ```bash
   mlflow server \
     --backend-store-uri sqlite:///mlflow.db \
     --default-artifact-root ./mlartifacts \
     --host 0.0.0.0 --port 5000
   ```

2. Run the training script:

   ```bash
   python train_model.py
   ```

This will:
- Train a Logistic Regression model on the Iris dataset.
- Compute accuracy, macro-averaged precision/recall/F1.
- Log parameters, metrics, and the model to MLflow.
- Register the model as `tracking_quickstart` and write artifacts under `mlruns/` and `mlartifacts/`.

## Serving / Using the Model

The trained model can be loaded via MLflow in your app code using:

```python
import mlflow

loaded_model = mlflow.pyfunc.load_model("models:/tracking_quickstart/Production")
```

(or another stage/version as appropriate.)

The `app/` directory is intended to host an API (e.g. FastAPI/Flask) that loads this model and exposes prediction endpoints.

## Notes

- Local run artifacts (`mlruns/`, `mlartifacts/`, `models/`) and the `mlops/` virtual environment should generally not be committed to version control. See `.gitignore` for details.
