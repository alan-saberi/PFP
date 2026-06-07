# Predicting Data Pipeline Failures using Spark ML & Databricks

## Problem Statement

Data pipelines in large-scale Spark environments often fail due to factors such as high data volume, transformation complexity, data skew, and resource pressure.

This project builds a machine learning model to **predict pipeline failures before execution**, enabling proactive monitoring and intervention — shifting from reactive firefighting to preventive engineering.

---

## Dataset

- **100,000 simulated pipeline runs**
- Noise-injected failure logic to reflect real-world unpredictability

| Feature | Description |
|---------|------------|
| rows_processed | Volume of data in the pipeline run |
| num_partitions | Level of Spark parallelism |
| num_joins | Number of join operations (complexity) |
| skew_flag | Whether data skew was detected (0/1) |
| execution_time | Total runtime in seconds |
| **failed** | **Target — 1 = failure, 0 = success** |

### Class Distribution
- ~70% success / ~30% failure
- Reflects real-world behavior where most pipelines succeed

---

## Approach

1. **Data Generation** — 100k pipeline runs with realistic noise injection
2. **Feature Engineering** — VectorAssembler to create Spark ML-compatible feature vectors
3. **Train/Test Split** — 80/20 split with seed for reproducibility
4. **Model Training** — Logistic Regression (binary classification)
5. **Evaluation** — Accuracy, AUC, Precision, Recall
6. **Experiment Tracking** — MLflow for parameters and metrics
7. **Real-World Demo** — Predict failure probability on new unseen pipelines

---

## Results

| Metric | Value |
|--------|-------|
| Accuracy | 0.7868 |
| AUC | 0.8691 |
| Precision | 0.7150 |
| Recall | 0.6419 |

### Key Findings

- **Data skew** is the strongest predictor of pipeline failure
- **Recall (0.64)** indicates room for improvement — 36% of real failures are missed
- AUC of 0.87 confirms strong class separation despite noise

### Prediction Demo

| Scenario | Failure Probability | Recommended Action |
|----------|--------------------|--------------------|
| Low Risk | ~8% | ✅ No action needed |
| Medium Risk | ~35% | ⚠️ Monitor closely |
| High Risk | ~92% | 🔴 Investigate before execution |

---

## Future Improvements

- Incorporate real pipeline logs (Spark metrics, shuffle stats, retry counts)
- Test stronger models (Random Forest, Gradient Boosted Trees)
- Adjust classification threshold to optimize for recall
- Deploy model via MLflow Model Registry for batch inference
- Connect to live Databricks job metadata for real-time scoring

---

## Technologies

![PySpark](https://img.shields.io/badge/PySpark-E25A1C?style=flat&logo=apachespark&logoColor=white)
![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=flat&logo=databricks&logoColor=white)
![MLflow](https://img.shields.io/badge/MLflow-0194E2?style=flat&logo=mlflow&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)

- PySpark (Spark ML)
- Databricks (Community Edition)
- MLflow (Experiment Tracking)
- Python

---

## How to Run

1. Import the notebook into your Databricks workspace
2. Attach to a cluster with Spark ML support
3. Run all cells sequentially
4. View MLflow experiment in the Experiments tab

---

## Author

**Alan Saberi**


---

## License

This project is open source and available under the [MIT License](LICENSE).
