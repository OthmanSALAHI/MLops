# MLOps Learning Playground

This repository is a personal space to **learn and practice MLOps** concepts end to end. It will host multiple small projects, starting with a simple Iris classifier tracked and managed with MLflow.

## Repository Structure

- `iris_MLOps/`  
  First project in this repo. Uses the Iris dataset to explore:
  - Training and evaluating a scikit-learn model
  - Tracking experiments and models with MLflow
  - Registering models for later serving

- `requirements.txt`  
  Base Python dependencies shared across projects.

- `mlops/`  
  Local Python virtual environment (created with `python -m venv mlops`). This folder is ignored in `.gitignore`.

- `mlruns/`, `mlartifacts/`, `models/`  
  MLflow tracking and artifact directories created automatically when you run experiments. These are not meant to be committed to Git.

As you add more projects, they can live in separate folders at this level (e.g. `wine_MLOps/`, `images_MLOps/`, `fraud_MLOps/`, etc.).

## Goals of This Repo

- Practice core MLOps topics on small, focused examples:
  - Reproducible experiments & versioning
  - Model and data tracking
  - Packaging models for serving (APIs, batch jobs)
  - CI/CD for ML
  - Monitoring and retraining workflows
- Keep projects **simple and readable**, so you can revisit them later as reference.

## Getting Started

1. **Clone the repo and enter the directory**:

   ```bash
   git clone https://github.com/othmansalahi/MLOps MLOps
   cd MLOps
   ```

2. **Create and activate a virtual environment** (optional but recommended):

   ```bash
   python3 -m venv mlops
   source mlops/bin/activate
   ```

3. **Install dependencies**:

   ```bash
   pip install -r requirements.txt
   ```

4. **(Optional) Start an MLflow tracking server**:

   ```bash
   mlflow server \
     --backend-store-uri sqlite:///mlflow.db \
     --default-artifact-root ./mlartifacts \
     --host 0.0.0.0 --port 5000
   ```

5. **Run the first project (Iris)**:

   ```bash
   cd iris_MLOps
   python train_model.py
   ```

   Then open the MLflow UI at http://localhost:5000 to inspect runs, metrics, and models.

## Adding New MLOps Projects

When you start a new learning project, you can:

1. Create a new folder at the repo root, e.g.:

   ```bash
   mkdir churn_MLOps
   ```

2. Add:
   - A dedicated `README.md` describing the project goal and MLOps focus.
   - Scripts or notebooks for data preparation, training, evaluation, and serving.
   - Any project-specific configs (YAML/JSON) and tests.

3. Reuse the same virtual environment and `requirements.txt`, or extend it as needed.

Over time this repo becomes a **portfolio of small, focused MLOps experiments** you can refer back to when building real-world systems.