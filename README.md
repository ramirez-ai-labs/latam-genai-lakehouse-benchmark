# LATAM GenAI Lakehouse Benchmark

Lakehouse-native evaluation framework for measuring regional Spanish LLM performance (SV vs PE) using Delta Lake, Spark, and Databricks.

This project demonstrates how to build a reproducible GenAI evaluation pipeline using the Bronze / Silver / Gold architecture pattern.

---

## 🎯 Problem

Most large language models are evaluated primarily in English.

However, real-world users in Latin America:
- Use regional slang (El Salvador vs Perú)
- Mix formal and informal register
- Submit noisy text (OCR artifacts, typos, web copy)

English-only benchmarks fail to capture regional performance gaps.

---

## 💡 Solution

This repository implements a Lakehouse-native evaluation pipeline that:

- Stores dialect test data in Delta tables
- Generates structured evaluation prompts
- Runs model scoring
- Captures metrics per item
- Aggregates performance by region and noise level
- Produces dashboard-ready summary tables

The goal is to detect robustness gaps before deploying GenAI systems into production environments.

---

## 🏗 Architecture Overview

Bronze → Silver → Gold

**Bronze Layer**
- Raw Spanish dialect samples
- Stored in Delta table: `latam_bronze_dialect_raw`

**Silver Layer**
- Structured evaluation items
- Prompt generation and enrichment
- Stored in: `latam_silver_eval_items`

**Gold Layer**
- Model scoring results
- Accuracy and metrics capture
- Stored in: `latam_gold_eval_runs`
- Aggregated summary: `latam_gold_eval_summary`

This mirrors production-grade Lakehouse design patterns.

---

## 🧰 Native Databricks Components Used

- Databricks Notebooks
- Serverless Compute
- Apache Spark
- Delta Lake Tables
- Databricks SQL
- Built-in Display & Visualization

Optional production extensions:
- Databricks Jobs (scheduled evaluation)
- MLflow (experiment tracking)
- Model Registry (versioned models)
- CI/CD deployment gates
- Monitoring & alerts

---

## 📊 Key Evaluation Dimensions

- Accuracy by Region (SV vs PE)
- Robustness (Clean vs OCR Noise)
- Performance Gap Analysis
- Governance-ready metrics

---

## 🚀 From Demo to Production

This notebook represents the offline evaluation layer of a production GenAI system.

In real-world deployments, this architecture would:

- Gate model releases based on evaluation thresholds
- Detect regressions across model versions
- Track performance over time
- Integrate with CI/CD pipelines
- Support monitoring and alerting

The objective is not just to build models —
but to build measurable, reliable, and governable AI systems.

---

## 📁 Repository Structure

```

latam-genai-lakehouse-benchmark/
│
├── notebooks/
│   └── 01_latam_benchmark_pipeline.ipynb
│
├── architecture/
│   └── lakehouse_eval_architecture.png
│
├── sample_data/
│   └── dialect_examples.csv
│
└── docs/
└── production_extension.md

```

---

## 🧠 Author

Victo Ramirez  
AI Architect | GenAI Platform & Evaluation Systems  