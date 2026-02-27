# Awesome Metaflow [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of Metaflow extensions, plugins, integrations, and resources.

[Metaflow](https://metaflow.org) is a human-friendly Python/R framework for building and managing real-life ML, AI, and data science projects. Originally built at Netflix, now maintained by [Outerbounds](https://outerbounds.com).

Items are included only if they have a clear install path and are either actively maintained or historically significant. Risk flags are shown explicitly where relevant.

---

## Contents

- [Core Infrastructure](#core-infrastructure)
- [Extension Mechanism & Templates](#extension-mechanism--templates)
- [Dependency Management](#dependency-management)
- [Orchestration & Scheduling](#orchestration--scheduling)
- [Distributed Compute & Training](#distributed-compute--training)
- [Model & Artifact Management](#model--artifact-management)
- [Observability & Monitoring](#observability--monitoring)
- [Cards & Visualization](#cards--visualization)
- [Third-Party Integrations](#third-party-integrations)
- [Infrastructure & IaC](#infrastructure--iac)
- [Developer Tooling](#developer-tooling)
- [Community Projects](#community-projects)
- [Examples & Tutorials](#examples--tutorials)

---

## Core Infrastructure

The foundational services required to run Metaflow in production.

- [Netflix/metaflow](https://github.com/Netflix/metaflow) - Core framework. Built-in support for `@kubernetes`, `@batch`, Argo Workflows, Airflow, and Step Functions. `pip install metaflow`
- [Netflix/metaflow-service](https://github.com/Netflix/metaflow-service) - Metadata tracking REST API and UI backend. PostgreSQL-backed; records all flow/run/step/task/artifact metadata.
- [Netflix/metaflow-ui](https://github.com/Netflix/metaflow-ui) - React/TypeScript web UI for real-time run monitoring. Supports a plugin system for custom UI extensions.
- [outerbounds/local_metaflow_deployment](https://github.com/outerbounds/local_metaflow_deployment) - Spin up a local Metadata service, PostgreSQL, and UI with Docker. Fastest way to test production-grade features locally.

---

## Extension Mechanism & Templates

How to build your own Metaflow extensions using the `metaflow_extensions` namespace package mechanism.

- [Netflix/metaflow-extensions-template](https://github.com/Netflix/metaflow-extensions-template) - Official template explaining how to create extensions. Covers custom decorators, CLI commands, config overrides, and "flavors." Start here if building your own extension.
- [outerbounds/custom-decorator-examples](https://github.com/outerbounds/custom-decorator-examples) - Gallery of user-defined decorators and mutators. Includes `@memoize`, `@stats_profile`, and org-policy patterns using `BaseFlow`.
- [outerbounds/config-examples](https://github.com/outerbounds/config-examples) - Examples of configuration management using Metaflow's `Config` object (released Dec 2024).

---

## Dependency Management

Extensions that replace or enhance Metaflow's `@conda` and `@pypi` decorators.

- [Netflix/metaflow-nflx-extensions](https://github.com/Netflix/metaflow-nflx-extensions) - Netflix's production extensions. Significantly enhanced `@conda`/`@pypi`: named environments, mixed conda+pip, `requirements.txt`/`environment.yml` support, parallel resolving with micromamba, cross-platform packages. Requires Metaflow ≥ 2.8.3. `pip install metaflow-netflixext`
- [nestauk/metaflow_extensions](https://github.com/nestauk/metaflow_extensions) - Adds `@pip` decorator and a `preinstall` shell-hook mechanism for injecting system-level dependencies on remote nodes before task execution. **Note:** uses an extension API that was unstable as of Metaflow 2.7.x; verify compatibility before using.

---

## Orchestration & Scheduling

Extensions that add new execution backends and orchestration targets.

- [outerbounds/metaflow-kubeflow](https://github.com/outerbounds/metaflow-kubeflow) - Deploy and run Metaflow flows on Kubeflow Pipelines. No changes needed to existing Kubeflow infrastructure. Feature set is actively evolving. `pip install metaflow-kubeflow`
- [outerbounds/metaflow-slurm](https://github.com/outerbounds/metaflow-slurm) - Run Metaflow steps on HPC Slurm clusters via SSH + `sbatch`. Adds `@slurm` decorator. Runs natively (no containers required). `pip install metaflow-slurm` **[Beta]**
- [outerbounds/metaflowbot](https://github.com/outerbounds/metaflowbot) - Slack bot for real-time flow monitoring. Delivers run notifications via DM or channel. Includes a CloudFormation template for AWS deployment. **[Older; verify against current Metaflow]**

---

## Distributed Compute & Training

Extensions that enable multi-node, distributed ML training and compute.

- [outerbounds/metaflow-ray](https://github.com/outerbounds/metaflow-ray) - Ephemeral Ray clusters on AWS Batch (multi-node parallel jobs) or Kubernetes (JobSets). Supports Ray Core, Train, Tune, and Data. Just call `ray.init()` inside the step. `pip install metaflow-ray`
- [outerbounds/metaflow-torchrun](https://github.com/outerbounds/metaflow-torchrun) - Run parallel Metaflow tasks as nodes in a `torchrun` job (DDP). Works on Batch or Kubernetes. No changes to existing PyTorch training code. `pip install metaflow-torchrun`
- [outerbounds/metaflow-deepspeed](https://github.com/outerbounds/metaflow-deepspeed) - `@deepspeed` decorator for Microsoft DeepSpeed training. Auto-configures SSH between nodes. Checkpoint uploads to S3 or Azure Blob. `pip install metaflow-deepspeed` **[Experimental; check activity]**
- [outerbounds/metaflow-mpi](https://github.com/outerbounds/metaflow-mpi) - `@mpi` decorator for multi-node MPI programs. Auto-configures SSH. Exposes `current.mpi.exec/run/cc`. Works with C/Fortran MPI programs and mpi4py. **[Experimental]**
- [outerbounds/metaflow-tensorflow](https://github.com/outerbounds/metaflow-tensorflow) - `@tensorflow` decorator that auto-configures `TF_CONFIG` for `tf.distribute.Strategy`. Supports single-node multi-GPU (`MirroredStrategy`) and multi-worker (`MultiWorkerMirroredStrategy`). **[Experimental; check activity]**
- [outerbounds/metaflow-pyspark](https://github.com/outerbounds/metaflow-pyspark) - EXPERIMENTAL PySpark decorator for Metaflow steps. **[Low adoption; use with caution]**

---

## Model & Artifact Management

Extensions for checkpointing, model versioning, and HuggingFace model handling.

- [outerbounds/metaflow-checkpoint](https://github.com/outerbounds/metaflow-checkpoint) - Adds `@checkpoint` (resume training from last save on retry), `@model` (model identity/lineage tracking), and `@huggingface_hub` (efficient local caching for large HF models). **Note:** not part of core Metaflow yet; APIs may change. `pip install metaflow-checkpoint`
- [outerbounds/metaflow-checkpoint-examples](https://github.com/outerbounds/metaflow-checkpoint-examples) - Examples for `@checkpoint` and `@model` covering PyTorch, Keras, Lightning, and distributed DDP training.

---

## Observability & Monitoring

Extensions and tools for metrics, profiling, and operational visibility.

- [outerbounds/metaflow-measure](https://github.com/outerbounds/metaflow-measure) - Instrument Metaflow steps with a `measure` API. Emit metrics to Datadog (`dogstatsd`) and other backends. Works locally and on Kubernetes/Batch without code changes. `pip install metaflow-measure`
- [outerbounds/metaflow-gpu-profile](https://github.com/outerbounds/metaflow-gpu-profile) - `@gpu_profile` decorator that monitors GPU utilization and memory via `nvidia-smi` and renders results as a Metaflow card. Essential for GPU workload optimization.
- [SpareCores/resource-tracker](https://github.com/SpareCores/resource-tracker) - Lightweight zero-dependency tracker for CPU, memory, GPU, network, and disk usage. Generates a Metaflow card with visualizations and cloud cost recommendations. `pip install resource-tracker`
- [rsmith013/metaflow-sentry-logger](https://github.com/rsmith013/metaflow-sentry-logger) - Sentry logging plugin via `--with sentry` or `@sentry`. **[High risk: relies on unsupported extension APIs; built against Metaflow 2.7.18; API changed in 2.7.20. Do not use without testing against your Metaflow version.]**

---

## Cards & Visualization

Extensions for the Metaflow Cards system. Cards attach HTML visualizations to flow runs.

- [outerbounds/metaflow-card-notebook](https://github.com/outerbounds/metaflow-card-notebook) - Render and execute Jupyter Notebooks as Metaflow cards via `@card(type='notebook')`. `pip install metaflow-card-notebook` **[Last commit 2022; verify compatibility]**
- [outerbounds/metaflow-card-html](https://github.com/outerbounds/metaflow-card-html) - Render raw HTML strings as Metaflow cards. Reference implementation for custom card authors. `pip install metaflow-card-html` **[Community reports of breakage; verify before use]**
- [outerbounds/metaflow-card-altair](https://github.com/outerbounds/metaflow-card-altair) - Render Altair interactive charts in Metaflow cards.
- [outerbounds/metaflow-card-scatter3d](https://github.com/outerbounds/metaflow-card-scatter3d) - Dynamic card for live 2D and 3D scatter plots.
- [outerbounds/metaflow-card-template](https://github.com/outerbounds/metaflow-card-template) - Template for building new Metaflow card types.
- [outerbounds/dynamic-card-examples](https://github.com/outerbounds/dynamic-card-examples) - Examples of live/dynamic Metaflow cards: progress bars, Altair/Vega charts, maps, and custom JS widgets.

---

## Third-Party Integrations

Integrations with external ML tools and platforms. Most ship as part of the external tool's package.

- **Weights & Biases** - `@wandb_log` decorator (ships in `wandb` package). Auto-logs `Parameter` objects as W&B config and step artifacts as W&B artifacts. Groups runs by `{flow_name}/{run_id}`. [Docs](https://docs.wandb.ai/models/integrations/metaflow)
- **Comet ML** - `@comet_flow` and `@comet_step` decorators (ships in `comet_ml` package). Automatically exports Metaflow Cards as HTML assets attached to Comet experiments. [Docs](https://www.comet.com/docs/v2/integrations/third-party-tools/metaflow/)
- [outerbounds/hamilton-metaflow](https://github.com/outerbounds/hamilton-metaflow) - Use Hamilton as a feature engineering / micro-orchestration layer inside Metaflow steps. Supports DAG visualization via Metaflow cards.
- [zillow/zdatasets](https://github.com/zillow/zdatasets) - Zillow's Dataset SDK for consistent batch/online/streaming data access. Provides `DatasetParameter` for typed dataset parameters in Metaflow flows.
- [astronomer/airflow-metaflow-demo](https://github.com/astronomer/airflow-metaflow-demo) - Demo by Astronomer: Metaflow + Airflow in Docker Compose with Metaflow steps running as `KubernetesPodOperator` tasks.
- **SAP AI Core** - `sap-ai-core-metaflow` generates Argo Workflow Templates from Metaflow flows for SAP AI Core. `pip install sap-ai-core-metaflow`

---

## Infrastructure & IaC

Terraform, CloudFormation, and Helm resources for deploying Metaflow at scale.

- [outerbounds/terraform-aws-metaflow](https://github.com/outerbounds/terraform-aws-metaflow) - Official Terraform module for AWS: Batch, S3, RDS, Step Functions, API Gateway, ECS/Fargate, optional EKS+Argo. Published on Terraform Registry as `outerbounds/metaflow/aws`.
- [outerbounds/metaflow-tools](https://github.com/outerbounds/metaflow-tools) - Multi-cloud ops toolkit: CloudFormation (AWS Batch + Step Functions), Terraform (AWS, Azure/AKS, GCP/GKE, Nebius), Helm charts for Kubernetes. Central hub for production deployments.
- [outerbounds/metaflow-with-airflow-minio](https://github.com/outerbounds/metaflow-with-airflow-minio) - Guide for Metaflow + Airflow + MinIO on Minikube.
- [gabrieltardochi/metaflow-docker-deployment](https://github.com/gabrieltardochi/metaflow-docker-deployment) - Community Docker Compose: Metaflow metadata service + UI + MinIO + PostgreSQL. Quick self-hosted setup.

---

## Developer Tooling

Tools that improve the Metaflow development experience.

- [outerbounds/metaflow-dev-vscode](https://github.com/outerbounds/metaflow-dev-vscode) - VS Code extension with keyboard shortcuts for running flows and individual steps directly from the editor.
- [outerbounds/metaflow-diff](https://github.com/outerbounds/metaflow-diff) - `git diff` between your working directory and a past Metaflow run. Pull code from a run or produce a patch file.
- `metaflow-stubs` - Type stubs for OSS Metaflow. IDE autocompletion for all Metaflow APIs. `pip install metaflow-stubs`
- [outerbounds/gha-metaflow](https://github.com/outerbounds/gha-metaflow) - GitHub Actions workflows for CI/CD with Metaflow. Trigger runs on push/PR; link namespaces to branches.

---

## Community Projects

High-quality community contributions that demonstrate Metaflow in real-world production contexts.

- [jacopotagliabue/you-dont-need-a-bigger-boat](https://github.com/jacopotagliabue/you-dont-need-a-bigger-boat) (~870 stars) - End-to-end intent prediction with Metaflow, Snowflake, SageMaker, dbt, W&B, and Great Expectations. Based on RecSys 2021 paper. The most-starred community Metaflow project.
- [jacopotagliabue/recs-at-reasonable-scale](https://github.com/jacopotagliabue/recs-at-reasonable-scale) (~241 stars) - Recommendation systems at scale with dbt, NVIDIA Merlin, and Metaflow.
- [jacopotagliabue/post-modern-stack](https://github.com/jacopotagliabue/post-modern-stack) (~201 stars) - Modern data stack + modern ML stack using dbt, SageMaker, and Metaflow with pluggable experiment trackers.
- [chiphuyen/metaflow-transformers-tutorials](https://github.com/chiphuyen/metaflow-transformers-tutorials) (~65 stars) - HuggingFace DistilBERT fine-tuning tutorials by Chip Huyen (author of *Designing Machine Learning Systems*).

---

## Examples & Tutorials

Official and community examples for specific use cases.

- [outerbounds/dsbook](https://github.com/outerbounds/dsbook) (~116 stars) - Code samples for *Effective Data Science Infrastructure* by Ville Tuulos. The conceptual companion to the framework.
- [outerbounds/full-stack-ML-metaflow-tutorial](https://github.com/outerbounds/full-stack-ML-metaflow-tutorial) (~82 stars) - Workshop: prototype to production ML, covering dbt, Great Expectations, W&B, and SageMaker.
- [outerbounds/tutorials](https://github.com/outerbounds/tutorials) - Official Metaflow tutorials on workflow graphs, versioning, data access, and scheduling.
- [outerbounds/metaflow-checkpoint-examples](https://github.com/outerbounds/metaflow-checkpoint-examples) - Beginner to advanced checkpointing examples (PyTorch, Keras, Lightning, distributed DDP).
- [outerbounds/diffusion-metaflow](https://github.com/outerbounds/diffusion-metaflow) (~33 stars) - Stable Diffusion text-to-image and text-to-video pipelines with Metaflow.
- [outerbounds/hacker-news-sentiment](https://github.com/outerbounds/hacker-news-sentiment) (~22 stars) - LLM-powered topic and sentiment analysis pipeline on Hacker News data.
- [outerbounds/metaflow-instruction-tuning](https://github.com/outerbounds/metaflow-instruction-tuning) (~12 stars) - LLM instruction tuning (Alpaca-LoRA, LLaMA 7B) with `@torchrun` and event-triggered Argo.
- [outerbounds/metaflow-trainium](https://github.com/outerbounds/metaflow-trainium) - AWS Trainium examples: LLaMA-2 pretraining, BERT fine-tuning, allreduce tests on trn1.32xlarge.
- [outerbounds/triton-metaflow-starter-pack](https://github.com/outerbounds/triton-metaflow-starter-pack) - NVIDIA Triton Inference Server integration with Metaflow.
- [outerbounds/rag-demo](https://github.com/outerbounds/rag-demo) - End-to-end RAG pipeline with LlamaIndex, LanceDB/Pinecone, and Metaflow.
- [Netflix/user2020-metaflow-tutorial](https://github.com/Netflix/user2020-metaflow-tutorial) (~27 stars) - R tutorial from useR! 2020.

---

## Contributing

Contributions welcome. To add an entry:

1. The project must be directly related to Metaflow (extension, integration, or high-quality reference)
2. Include: repo URL, one-line description, install method (if applicable)
3. Flag status explicitly if the project is experimental, beta, or has known compatibility issues
4. Place deprecated/unmaintained items with a clear **[Archived]** or **[Unmaintained]** label

See [awesome list guidelines](https://github.com/sindresorhus/awesome/blob/main/contributing.md) for formatting conventions.

---

## License

[![CC0](https://mirrors.creativecommons.org/presskit/buttons/88x31/svg/cc-zero.svg)](https://creativecommons.org/publicdomain/zero/1.0/)
