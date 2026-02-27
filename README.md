# Awesome Metaflow [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of Metaflow extensions, plugins, integrations, and resources.

[Metaflow](https://metaflow.org) is a human-friendly Python/R framework for real-life ML, AI, and data science. Originally built at Netflix and open-sourced in 2019.

---

## Contents

- [🏗️ Core Infrastructure](#-core-infrastructure)
- [☁️ Infrastructure & IaC](#-infrastructure--iac)
- [📦 Dependency Management](#-dependency-management)
- [🧩 Extension Mechanism & Templates](#-extension-mechanism--templates)
- [🔀 Orchestration & Scheduling](#-orchestration--scheduling)
- [⚡ Distributed Compute & Training](#-distributed-compute--training)
- [💾 Model & Artifact Management](#-model--artifact-management)
- [📊 Observability & Monitoring](#-observability--monitoring)
- [🃏 Cards & Visualization](#-cards--visualization)
- [🔌 Third-Party Integrations](#-third-party-integrations)
- [🛠️ Developer Tooling](#-developer-tooling)
- [🌍 Community Projects](#-community-projects)
- [📚 Examples & Tutorials](#-examples--tutorials)

---

## 🏗️ Core Infrastructure

- [local_metaflow_deployment](https://github.com/outerbounds/local_metaflow_deployment) - Docker-based local stack: metadata service, PostgreSQL, and UI.
- [metaflow](https://github.com/Netflix/metaflow) - Core framework with built-in `@kubernetes`, `@batch`, Argo, Airflow, and Step Functions support.
- [metaflow-local-service](https://github.com/npow/metaflow-local-service) - Track Metaflow runs anywhere without a database — starts on demand, stops when idle.
- [metaflow-service](https://github.com/Netflix/metaflow-service) - Metadata tracking REST API and UI backend.
- [metaflow-ui](https://github.com/Netflix/metaflow-ui) - React web UI for real-time run monitoring with a plugin system.

---

## ☁️ Infrastructure & IaC

- [metaflow-docker-deployment](https://github.com/gabrieltardochi/metaflow-docker-deployment) - Community Docker Compose: metadata service + UI + MinIO + PostgreSQL.
- [metaflow-tools](https://github.com/outerbounds/metaflow-tools) - CloudFormation, Terraform (AWS/Azure/GCP/Nebius), and Helm charts for Kubernetes.
- [metaflow-with-airflow-minio](https://github.com/outerbounds/metaflow-with-airflow-minio) - Metaflow + Airflow + MinIO on Minikube.
- [terraform-aws-metaflow](https://github.com/outerbounds/terraform-aws-metaflow) - Official Terraform module for AWS (Batch, S3, RDS, Step Functions, ECS, optional EKS+Argo).

---

## 📦 Dependency Management

- [metaflow-nflx-extensions](https://github.com/Netflix/metaflow-nflx-extensions) - Netflix's enhanced `@conda`/`@pypi`: named environments, mixed conda+pip, and faster resolving via micromamba. Requires Metaflow ≥ 2.8.3.
- [metaflow_extensions](https://github.com/nestauk/metaflow_extensions) - Adds `@pip` and a `preinstall` shell-hook for system-level deps on remote nodes. ⚠️ Built against Metaflow 2.7.x; verify compatibility.

---

## 🧩 Extension Mechanism & Templates

- [config-examples](https://github.com/outerbounds/config-examples) - Examples using Metaflow's `Config` object for flow-level configuration.
- [custom-decorator-examples](https://github.com/outerbounds/custom-decorator-examples) - Examples of user-defined decorators and mutators, including `@memoize` and `BaseFlow` patterns.
- [metaflow-extensions-template](https://github.com/Netflix/metaflow-extensions-template) - Official template for building `metaflow_extensions` namespace packages.

---

## 🔀 Orchestration & Scheduling

- [metaflow-dagster](https://github.com/npow/metaflow-dagster) - Dagster scheduling, observability, and UI for Metaflow pipelines.
- [metaflow-flyte](https://github.com/npow/metaflow-flyte) - Schedule and monitor Metaflow pipelines through Flyte without rewriting them.
- [metaflow-kestra](https://github.com/npow/metaflow-kestra) - Kestra scheduling, triggers, and UI for Metaflow pipelines.
- [metaflow-kubeflow](https://github.com/outerbounds/metaflow-kubeflow) - Deploy Metaflow flows to Kubeflow Pipelines with no infra changes required.
- [metaflow-prefect](https://github.com/npow/metaflow-prefect) - Prefect scheduling, deployments, and UI for Metaflow pipelines.
- [metaflow-slurm](https://github.com/outerbounds/metaflow-slurm) - Run steps on HPC Slurm clusters via SSH + `sbatch`. Beta.
- [metaflow-temporal](https://github.com/npow/metaflow-temporal) - Temporal scheduling and durable workflows for Metaflow pipelines.
- [metaflowbot](https://github.com/outerbounds/metaflowbot) - Slack bot for real-time flow monitoring with CloudFormation deploy. ⚠️ Older; verify against current Metaflow.

---

## ⚡ Distributed Compute & Training

- [metaflow-deepspeed](https://github.com/outerbounds/metaflow-deepspeed) - `@deepspeed` for multi-node DeepSpeed training with S3/Azure checkpoint uploads. Experimental.
- [metaflow-mpi](https://github.com/outerbounds/metaflow-mpi) - `@mpi` for multi-node MPI programs (C/Fortran/mpi4py). Experimental.
- [metaflow-pyspark](https://github.com/outerbounds/metaflow-pyspark) - PySpark decorator for Metaflow steps. Experimental, low adoption.
- [metaflow-ray](https://github.com/outerbounds/metaflow-ray) - Ephemeral Ray clusters on AWS Batch or Kubernetes. Supports Ray Core, Train, Tune, and Data.
- [metaflow-sandbox](https://github.com/npow/metaflow-sandbox) - Metaflow steps in millisecond-start sandboxes with cloud-scale fanout and consistent deps.
- [metaflow-tensorflow](https://github.com/outerbounds/metaflow-tensorflow) - `@tensorflow` that auto-configures `TF_CONFIG` for `tf.distribute.Strategy`. Experimental.
- [metaflow-torchrun](https://github.com/outerbounds/metaflow-torchrun) - Run tasks as nodes in a `torchrun` DDP job on Batch or Kubernetes.

---

## 💾 Model & Artifact Management

- [metaflow-checkpoint](https://github.com/outerbounds/metaflow-checkpoint) - `@checkpoint`, `@model`, and `@huggingface_hub` for fault-tolerant training and model lineage. APIs may change.
- [metaflow-checkpoint-examples](https://github.com/outerbounds/metaflow-checkpoint-examples) - Examples covering PyTorch, Keras, Lightning, and distributed DDP.

---

## 📊 Observability & Monitoring

- [metaflow-gpu-profile](https://github.com/outerbounds/metaflow-gpu-profile) - `@gpu_profile` decorator that renders GPU utilization as a Metaflow card.
- [metaflow-measure](https://github.com/outerbounds/metaflow-measure) - Emit step metrics to Datadog and other backends via a `measure` API.
- [metaflow-sentry-logger](https://github.com/rsmith013/metaflow-sentry-logger) - Sentry logging via `@sentry`. ⚠️ Relies on an unsupported extension API; broken as of Metaflow 2.7.20.
- [resource-tracker](https://github.com/SpareCores/resource-tracker) - Zero-dependency CPU/memory/GPU tracker with Metaflow card output and cloud cost recommendations.

---

## 🃏 Cards & Visualization

- [dynamic-card-examples](https://github.com/outerbounds/dynamic-card-examples) - Live cards with progress bars, Altair/Vega charts, maps, and custom JS.
- [metaflow-card-altair](https://github.com/outerbounds/metaflow-card-altair) - Render Altair charts in Metaflow cards.
- [metaflow-card-html](https://github.com/outerbounds/metaflow-card-html) - Render raw HTML as a card. Reference implementation for custom card authors. ⚠️ Community reports of breakage.
- [metaflow-card-notebook](https://github.com/outerbounds/metaflow-card-notebook) - Render Jupyter Notebooks as Metaflow cards. ⚠️ Last commit 2022.
- [metaflow-card-scatter3d](https://github.com/outerbounds/metaflow-card-scatter3d) - Live 2D and 3D scatter plot card.
- [metaflow-card-template](https://github.com/outerbounds/metaflow-card-template) - Starter template for building new card types.

---

## 🔌 Third-Party Integrations

- [airflow-metaflow-demo](https://github.com/astronomer/airflow-metaflow-demo) - Metaflow + Airflow in Docker Compose with `KubernetesPodOperator` steps.
- **Comet ML** - `@comet_flow` and `@comet_step` ship in the `comet_ml` package, including automatic Card export. [Docs](https://www.comet.com/docs/v2/integrations/third-party-tools/metaflow/)
- [hamilton-metaflow](https://github.com/outerbounds/hamilton-metaflow) - Hamilton as a feature engineering layer inside Metaflow steps.
- **SAP AI Core** - `sap-ai-core-metaflow` generates Argo Workflow Templates from Metaflow flows.
- **Weights & Biases** - `@wandb_log` ships in the `wandb` package. [Docs](https://docs.wandb.ai/models/integrations/metaflow)
- [zdatasets](https://github.com/zillow/zdatasets) - Zillow's Dataset SDK with a `DatasetParameter` integration for Metaflow flows.

---

## 🛠️ Developer Tooling

- [gha-metaflow](https://github.com/outerbounds/gha-metaflow) - GitHub Actions workflows that trigger Metaflow runs on push/PR.
- [metaflow-dev-vscode](https://github.com/outerbounds/metaflow-dev-vscode) - VS Code extension with shortcuts for running flows and steps from the editor.
- [metaflow-diff](https://github.com/outerbounds/metaflow-diff) - Diff your working directory against a past Metaflow run.
- [metaflow-mcp-server](https://github.com/npow/metaflow-mcp-server) - MCP server for inspecting runs, logs, and artifacts from any AI agent.
- `metaflow-stubs` - Type stubs for IDE autocompletion. `pip install metaflow-stubs`

---

## 🌍 Community Projects

- [metaflow-transformers-tutorials](https://github.com/chiphuyen/metaflow-transformers-tutorials) - HuggingFace DistilBERT fine-tuning tutorials by Chip Huyen.
- [post-modern-stack](https://github.com/jacopotagliabue/post-modern-stack) - Modern data stack + ML stack using dbt, SageMaker, and Metaflow.
- [recs-at-reasonable-scale](https://github.com/jacopotagliabue/recs-at-reasonable-scale) - Recommendations at scale with dbt, NVIDIA Merlin, and Metaflow.
- [you-dont-need-a-bigger-boat](https://github.com/jacopotagliabue/you-dont-need-a-bigger-boat) - End-to-end RecSys with Metaflow, Snowflake, SageMaker, dbt, and W&B.

---

## 📚 Examples & Tutorials

- [diffusion-metaflow](https://github.com/outerbounds/diffusion-metaflow) - Stable Diffusion text-to-image and text-to-video pipelines.
- [dsbook](https://github.com/outerbounds/dsbook) - Code for *Effective Data Science Infrastructure* by Ville Tuulos.
- [full-stack-ML-metaflow-tutorial](https://github.com/outerbounds/full-stack-ML-metaflow-tutorial) - Workshop: prototype to production ML with dbt, Great Expectations, W&B, and SageMaker.
- [hacker-news-sentiment](https://github.com/outerbounds/hacker-news-sentiment) - LLM-powered topic and sentiment analysis on Hacker News data.
- [metaflow-checkpoint-examples](https://github.com/outerbounds/metaflow-checkpoint-examples) - Checkpointing examples covering PyTorch, Keras, Lightning, and distributed DDP.
- [metaflow-instruction-tuning](https://github.com/outerbounds/metaflow-instruction-tuning) - LLM instruction tuning (Alpaca-LoRA, LLaMA 7B) with `@torchrun`.
- [metaflow-trainium](https://github.com/outerbounds/metaflow-trainium) - AWS Trainium examples: LLaMA-2 pretraining, BERT fine-tuning.
- [rag-demo](https://github.com/outerbounds/rag-demo) - End-to-end RAG pipeline with LlamaIndex and LanceDB/Pinecone.
- [triton-metaflow-starter-pack](https://github.com/outerbounds/triton-metaflow-starter-pack) - NVIDIA Triton Inference Server starter pack.
- [tutorials](https://github.com/outerbounds/tutorials) - Official tutorials on workflow graphs, versioning, data access, and scheduling.
- [user2020-metaflow-tutorial](https://github.com/Netflix/user2020-metaflow-tutorial) - R tutorial from useR! 2020.

---

## Contributing

1. Project must be Metaflow-related with a clear install path
2. One-line description only
3. Flag experimental/broken items with ⚠️
4. No item without a working link

---

## License

[![CC0](https://mirrors.creativecommons.org/presskit/buttons/88x31/svg/cc-zero.svg)](https://creativecommons.org/publicdomain/zero/1.0/)
