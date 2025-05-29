# 🧬 NGS Pipeline MVP

A minimal viable product (MVP) for a clinical-grade Next-Generation Sequencing (NGS) variant calling pipeline built using **FastAPI**, **Nextflow**, and **AWS Batch**.

## 🚀 Project Overview

This MVP provides an end-to-end API-driven system for:

- Uploading FASTQ files to S3
- Submitting NGS analysis pipelines
- Tracking job progress and retrieving results
- Running scalable workflows on AWS Batch via Nextflow

## 📁 Project Structure

```
ngs-pipeline-mvp/
├── src/ngs_pipeline/   # Main application code
│ ├── main.py           # FastAPI app
│ ├── models.py         # Pydantic models
│ ├── pipeline.py       # Pipeline orchestration logic
│ ├── storage.py        # S3 interaction layer
│ └── utils.py          # Helper functions
├── nextflow/           # Nextflow pipeline
│ ├── main.nf           # Main pipeline script
│ └── modules/          # Workflow modules (QC, alignment, etc.)
├── containers/         # Dockerfiles for pipeline tools
├── tests/              # Unit and integration tests
├── scripts/            # AWS and deployment helper scripts
├── Dockerfile          # API service container
├── docker-compose.yml  # Local dev environment
├── requirements.txt    # Python dependencies
├── .env.example        # Sample environment variables
└── README.md
```

## 📦 Requirements

- Python 3.10+
- Docker + Docker Compose
- AWS CLI & credentials
- Nextflow (locally or in Docker) <- Requires java 17?

## 🛠️ Setup Instructions

### 1. Clone the Repository

```bash
git clone https://git@github.com:joelcrouch/ngs_pipeline.git
cd ngs_pipeline

2. Configure Environment

Copy and modify the example environment file:

cp .env.example .env <--fix this

3. Start Local Dev Server

Use Docker Compose to bring up the FastAPI app:

docker-compose up --build

Visit: http://localhost:8000/docs for the interactive API docs.
4. Run Tests

docker-compose exec api pytest

Or locally:

pip install -r requirements.txt
pytest
```

🌐 API Endpoints

```
Method Endpoint Description
GET / HTML upload form (optional UI)
GET /health Health check
POST /files/upload Upload FASTQ files
POST /pipeline/submit Submit pipeline job
GET /pipeline/{job_id} Check job status
GET /pipelines List all jobs
GET /pipeline/{job_id}/results Retrieve job results
POST /pipeline/{job_id}/cancel Cancel a running job
GET /pipeline/{job_id}/logs View pipeline logs
```

⚙️ Pipeline Execution

    Workflows are defined using Nextflow and run on AWS Batch

    Output results are uploaded back to S3 and exposed via API

    Logging and job status tracking via SQLite for MVP simplicity

✅ Testing Strategy

    Unit tests for core components: models, storage, pipeline logic

    Mocked AWS services for local development

    Integration tests for full API and pipeline submission flow

📦 Deployment (MVP Scope)

    Use docker-compose for local development and test

    Production setup can evolve to ECS/EKS + RDS + real Batch queues

🧪 Sample Test FASTQ File

A tiny test FASTQ is included under:

tests/test_data/small_sample.fastq.gz

🔐 Secrets

Do not commit .env or AWS credentials. Use .env.example to scaffold required values.
📄 License

MIT License (or replace with your org’s preferred license)
👥 Contributors

    Joel Crouch

    Future collaborators

```

```
