# O que faz um AI Harness Engineer?

Embora o nome varie entre empresas (AI Harness Engineer, AI Platform Engineer, AI Infrastructure Engineer, AI Systems Engineer), o trabalho é construir a infraestrutura que permite que modelos de IA funcionem de forma confiável.

Em vez de treinar modelos, esse profissional responde perguntas como:

* Como servir um LLM para milhares de usuários?
* Como distribuir requisições entre várias GPUs?
* Como monitorar latência?
* Como reduzir custos de inferência?
* Como atualizar modelos sem interromper o serviço?
* Como conectar agentes de IA com bancos de dados e APIs?
* Como garantir escalabilidade?

É uma mistura de:

* Engenharia de Software
* Backend
* DevOps
* Cloud
* MLOps
* Sistemas Distribuídos
* IA

# Roadmap

## Etapa 1 — Domine Python (1 mês)

Aprenda muito bem:

* orientação a objetos
* async/await
* multiprocessing
* typing
* generators
* decorators

Depois:

* Pandas
* NumPy
* requests
* FastAPI

Objetivo:

Construir APIs de IA.

## Etapa 2 — Backend (1 mês)

Aprenda:

* FastAPI
* REST
* WebSocket
* autenticação JWT
* PostgreSQL
* Redis

Projeto:

Criar uma API que recebe um prompt e responde usando um LLM.


## Etapa 3 — Docker (2 semanas)

Aprenda:

* Dockerfile
* docker-compose
* volumes
* networking

Projeto:

Containerizar sua aplicação.

## Etapa 4 — Kubernetes (1 a 2 meses)

Aprenda:

* Pods
* Deployments
* Services
* ConfigMaps
* Secrets
* Ingress
* Helm

Projeto:

Executar sua API de IA em um cluster Kubernetes.

# Etapa 5 — LLMs

Aprenda:

* Transformers
* Tokens
* Context Window
* Embeddings
* Attention
* Fine-tuning
* LoRA
* RAG

Depois:

* LangChain
* LlamaIndex
* OpenAI SDK
* Anthropic SDK

Projeto:

Criar um chatbot com RAG.

# Etapa 6 — Bancos Vetoriais

Aprenda:

* Qdrant
* Milvus
* Weaviate
* pgvector

Projeto:

Construir um sistema que consulta documentos usando embeddings.

# Etapa 7 — Serving

Essa é uma das áreas mais importantes para um Harness Engineer.

Aprenda:

* vLLM
* NVIDIA Triton
* Ollama
* SGLang
* Ray Serve

Projeto:

Hospedar um modelo localmente e criar uma API de inferência.

# Etapa 8 — MLOps

Aprenda:

* MLflow
* DVC
* Kubeflow
* Airflow

Entenda:

* versionamento de modelos
* pipelines
* deploy automatizado
* monitoramento

# Etapa 9 — Cloud

Escolha uma:

* AWS
* Azure
* GCP

Aprenda:

* máquinas virtuais
* armazenamento
* Kubernetes gerenciado
* GPUs na nuvem

# Etapa 10 — Observabilidade

Aprenda:

* Prometheus
* Grafana
* Loki
* OpenTelemetry

Você deve conseguir responder:

* Quanto tempo um modelo leva para responder?
* Qual GPU está sobrecarregada?
* Quantas requisições por segundo o sistema suporta?

# Etapa 11 — GPUs

Aprenda:

* CUDA
* VRAM
* Tensor Cores
* quantização
* FP16
* INT8
* GGUF
* ONNX

Entenda por que um modelo pode usar 24 GB de VRAM e como reduzir esse consumo.

# Etapa 12 — Sistemas Distribuídos

Aprenda:

* Kafka
* RabbitMQ
* Redis Streams

Depois:

* Ray
* Celery

# Etapa 13 — Benchmark

Aprenda a medir:

* throughput
* latency
* tokens/s
* requests/s
* utilização da GPU
* consumo de memória

# Etapa 14 — CI/CD

Aprenda:

* GitHub Actions
* Terraform
* Helm
* ArgoCD

Tudo deve ser automatizado.


# Etapa 15 — Projetos

Monte um portfólio público com projetos como:

1. ChatGPT local usando Llama + vLLM.
2. Sistema RAG para consultar PDFs.
3. API FastAPI com streaming de tokens.
4. Deploy em Kubernetes.
5. Dashboard com Grafana e Prometheus.
6. Banco vetorial (Qdrant ou pgvector).
7. Cluster com múltiplas GPUs.
8. Pipeline automatizado de deploy.


## Um plano de 18 meses

1. **Meses 1–3:** Python avançado, FastAPI, Git, Docker.
2. **Meses 4–6:** LLMs, RAG, LangChain/LlamaIndex, bancos vetoriais.
3. **Meses 7–9:** Kubernetes, cloud (AWS ou GCP), Terraform.
4. **Meses 10–12:** vLLM, Triton, Ray Serve, MLflow, observabilidade.
5. **Meses 13–18:** projetos completos, contribuições open source e preparação para entrevistas.