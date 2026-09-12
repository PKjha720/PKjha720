# Prabhat Kumar Jha

**Senior Associate, Artificial Intelligence Operations — Bread Financial**
Retrieval systems for domains where a missed document has a cost: aviation safety, regulatory compliance, financial services.

[![Portfolio](https://img.shields.io/badge/Portfolio-1A4FA0?style=flat-square&logoColor=white)](https://pkjha720.github.io/portfolio/)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-1A4FA0?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/prabhat-kumar-jha-46a777100/)
[![Preprint](https://img.shields.io/badge/Preprint-1A4FA0?style=flat-square&logoColor=white)](https://doi.org/10.5281/zenodo.22382810)
[![ORCID](https://img.shields.io/badge/ORCID-1A4FA0?style=flat-square&logoColor=white)](https://orcid.org/0009-0003-0851-2481)
[![Email](https://img.shields.io/badge/prabhatbit2016%40gmail.com-1A4FA0?style=flat-square&logoColor=white)](mailto:prabhatbit2016@gmail.com)

---

## What I work on

I build and operate retrieval pipelines in production. At Bread Financial I work on the Content and Knowledge Management team's enterprise retrieval platform, built on Haystack, Redis and LiteLLM and deployed on AWS EKS, where I am responsible for pipeline reliability, security patching and architectural changes to the retrieval stack.

Before this I spent four years at Airports Authority of India as a Junior Executive (Technical). The production ML infrastructure there was mine end to end: streaming ingestion across more than 50 airport subsystems using Kafka and PySpark, FastAPI services with role-based access control, CI/CD, Prometheus and Grafana monitoring, drift detection with PSI and KS tests, and automated retraining triggers behind the deployed forecasting models.

## AeroRAG — hybrid retrieval over civil aviation regulation

[Code](https://github.com/PKjha720/aviation-rag) · [Live demo](https://aviation-rag-by-prabhat.streamlit.app) · [Preprint](https://doi.org/10.5281/zenodo.22382810)

Retrieval and question answering over 43 DGCA and ICAO regulatory documents: 10,572 chunks, 368 of them derived from tables. BM25 sparse retrieval runs alongside a ChromaDB bi-encoder index, the two are merged by Reciprocal Rank Fusion at k=60, rescored by an ms-marco-MiniLM cross-encoder, and answered with citation-enforced prompting through a Groq-hosted model. There is no retrieval framework underneath it, which is what makes each stage independently ablatable.

Four-way ablation on an 80-question benchmark stratified by evidence type:

| Configuration | Recall@5 | MRR@10 |
|:---|---:|---:|
| Dense only | 0.69 | 0.660 |
| RRF fused, no reranking | 0.76 | 0.655 |
| Full pipeline | 0.80 | 0.725 |
| BM25 + reranking | 0.80 | 0.730 |

Two things came out of this that were worth the work. Reranking earns its keep on ordering rather than coverage: it moves MRR@10 from 0.655 to 0.725 while Recall@5 moves only within sampling noise. And BM25 with the same reranker matched the full pipeline, which turned out to be a limitation of the benchmark rather than a result about retrieval, because synthetic questions reuse their source wording and never properly test the dense branch.

The decisive stage was ingestion, not retrieval architecture. Standard PDF extraction flattens tables into prose, so no table reached the index as a table. After rebuilding ingestion to preserve them, table-evidence queries still retrieve at 0.675 Recall@5 against 0.925 for prose (p=0.010), and 0.500 against 0.875 under dense retrieval alone (p=0.0006). Neither fusion nor reranking closes that gap. Since 21% of the corpus pages carry no text layer at all, a benchmark built from the index cannot see what ingestion discarded, so the paper argues for reporting a coverage audit alongside recall.

Deployed at roughly 2.3 s median end-to-end latency: 120 ms retrieval, 400 ms fusion and reranking, 1.8 s generation. Code, indices and the evaluation set are released under MIT.

## Other work

**Anomaly detection on airport infrastructure telemetry.** LSTM autoencoders against Isolation Forest and statistical baselines on high-frequency sensor data. The autoencoder surfaced failure precursors four to six hours ahead of the threshold-based monitoring in use. Write-up in progress.

**Demand forecasting across 60+ airports.** SARIMA, Prophet and XGBoost with Fourier-encoded seasonality. XGBoost with engineered temporal features reached 15% MAPE on 30-day horizons and held up better than SARIMA on non-stationary traffic.

| Repository | |
|:---|:---|
| [industry-grade-rag-genai](https://github.com/PKjha720/industry-grade-rag-genai) | Production RAG API: containerised FastAPI, multi-stage Docker build, CI/CD gates, Prometheus observability, citation-validated JSON output |
| [Kidney-Disease-Classification-MLflow-DVC](https://github.com/PKjha720/Kidney-Disease-Classification-MLflow-DVC) | Medical image classification with experiment tracking and data versioning |
| [yt-comment-sentiment-analysis](https://github.com/PKjha720/yt-comment-sentiment-analysis) | Sentiment pipeline over noisy real-world comment text |
| [Route-optimization](https://github.com/PKjha720/Route-optimization) | Route optimisation for logistics planning |

## Stack

| | |
|:---|:---|
| **Retrieval** | BM25, dense bi-encoders, hybrid retrieval, Reciprocal Rank Fusion, cross-encoder reranking, ChromaDB, FAISS, Haystack, RAGAS |
| **ML** | PyTorch, TensorFlow, scikit-learn, XGBoost, HuggingFace Transformers, sentence-transformers |
| **Time series** | LSTM/GRU, ARIMA/SARIMA, Prophet, Isolation Forest |
| **Infrastructure** | Docker, Kubernetes, AWS (EKS, SageMaker), Kafka, Spark, MLflow, Redis, LiteLLM |
| **Services** | FastAPI, Prometheus, Grafana, Git, LaTeX |

## Background

B.E. Mechanical Engineering, Birla Institute of Technology, Mesra (2014–18). I trained as a mechanical
engineer and came to machine learning through the problem rather than the other way round: four years of
working with aviation regulatory documents at AAI is what made retrieval interesting to me.

### Competitive examinations

| | |
|:---|:---|
| Airports Authority of India, national recruitment | **All India Rank 3** · 105/120, from 150,000+ candidates |
| GATE CS/IT, 2022 | **99.28 percentile** |
| GATE CS/IT, 2021 | **99.16 percentile** |
| GATE Data Science & AI | Qualified |
| HPCL Graduate Engineer Trainee | 165/170 |

### Standardised tests

| | |
|:---|:---|
| GRE General | **339/340** · Quantitative 170, Verbal 169 · 99th percentile |
| TOEFL iBT | **110/120** |
| JEE Main, 2014 | **99.85 percentile** of 1.36 million candidates |
| JEE Advanced, 2014 | Top **0.7%** of that cohort |

### Academic

| | |
|:---|:---|
| B.E. Mechanical Engineering, BIT Mesra | CGPA **8.32/10** · university batch topper |
| Placement | First student placed in the batch |
| IIT Delhi M.Tech, AI & Data Science | Admitted 2022 (declined) |
| Tata Millennial Scholarship | Four years |

### Formula Student India, 2017

Design lead on the pneumatic gear shifter for BIT Mesra's Formula Student car: a solenoid-actuated shifting
system sized against a measured 250 N shift force, closed in software on an Arduino reading the engine's
gear-position sensor, with the final drive ratio selected by sweeping FDR in OptimumLap across four tracks.

| | |
|:---|:---|
| Design Event | **All India Rank 4** |
| Overall standing | **All India Rank 7** |
| Sponsorship raised | **₹11 lakh**, independently, across two campaigns |
| Students trained | ~40 per year on vehicle design, fabrication and documentation |
