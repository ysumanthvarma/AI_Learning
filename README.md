
# AI for SRE 100-Day Plan

## Goal

Build practical AI skills for SRE work by creating an `ai-sre-assistant` capstone. The assistant should answer runbook questions with citations, summarize alerts and logs safely, call approved read-only tools, expose operational telemetry, and enforce safety controls before any risky action.

## Daily Time Budget

- 10 min: recap yesterday
- 20 min: learn/read
- 50 min: build
- 10 min: test/verify
- 10 min: write notes/update README

Recommended pace: 1.5 hours/day.

## Core Resources

- Python: https://docs.python.org/3/tutorial/
- Python venv: https://docs.python.org/3/library/venv.html
- FastAPI: https://fastapi.tiangolo.com/tutorial/
- FastAPI testing: https://fastapi.tiangolo.com/tutorial/testing/
- pytest: https://docs.pytest.org/en/stable/
- Pydantic: https://docs.pydantic.dev/
- Git book: https://git-scm.com/book/en/v2
- Docker getting started: https://docs.docker.com/get-started/
- Kubernetes probes: https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/
- OpenTelemetry concepts: https://opentelemetry.io/docs/concepts/
- Prometheus docs: https://prometheus.io/docs/introduction/overview/
- Grafana docs: https://grafana.com/docs/grafana/latest/
- OWASP LLM Top 10: https://owasp.org/www-project-top-10-for-large-language-model-applications/
- NIST AI RMF: https://www.nist.gov/itl/ai-risk-management-framework
- vLLM docs: https://docs.vllm.ai/
- KServe docs: https://kserve.github.io/website/
- Ray Serve docs: https://docs.ray.io/en/latest/serve/

## 100-Day Plan

### Day 1: Define the AI SRE Assistant Product Goal
- Learn: What AI can and cannot safely do for SRE workflows.
- Build: Create a one-page product goal: users, use cases, non-goals, risks.
- Output: `docs/product-goal.md`.
- Resources: OWASP LLM Top 10, NIST AI RMF.

### Day 2: Create the Capstone Repo Structure
- Learn: How to structure a small production-style Python service.
- Build: Create `~/Projects/ai-sre-assistant` with app, gateway, rag, tools, policy, telemetry, evals, runbooks, dashboards, manifests, capacity, docs, tests.
- Output: repo skeleton.
- Resources: Python packaging guide, Git book.

### Day 3: Create Python Virtual Environment and Tooling
- Learn: `venv`, `pip`, dependency files, repeatable local setup.
- Build: Add `.venv`, `requirements-dev.txt` or `pyproject.toml`.
- Output: local Python environment.
- Resources: Python venv docs, pytest docs.

### Day 4: Build FastAPI Skeleton
- Learn: FastAPI app, routes, JSON responses.
- Build: Add `app/main.py` and start the API locally.
- Output: running API service.
- Resources: FastAPI tutorial.

### Day 5: Add `/health`
- Learn: Health endpoint purpose.
- Build: Return service status and request ID.
- Output: `GET /health`.
- Resources: Kubernetes liveness probe docs.

### Day 6: Add `/ready`
- Learn: Readiness vs liveness.
- Build: Return dependency readiness for model provider, vector store, tool router.
- Output: `GET /ready`.
- Resources: Kubernetes readiness probe docs.

### Day 7: Add `/version`
- Learn: Why AI systems need app, model, prompt, corpus, and eval versions.
- Build: Return version metadata.
- Output: `GET /version`.
- Resources: OpenTelemetry resource concepts.

### Day 8: Add Request ID and Trace ID Handling
- Learn: Correlation IDs in incident debugging.
- Build: Middleware for request ID and trace ID.
- Output: response headers and JSON request ID.
- Resources: OpenTelemetry concepts.

### Day 9: Add API Tests
- Learn: Testing FastAPI endpoints.
- Build: Tests for `/health`, `/ready`, `/version`.
- Output: passing pytest suite.
- Resources: FastAPI testing, pytest docs.

### Day 10: Week 1 Foundation Review
- Learn: How to demo a small platform increment.
- Build: README, architecture note, ADR for control-plane-first design.
- Output: Week 1 demo script.
- Resources: Git book, FastAPI docs.

### Day 11: Create Sample Runbook Corpus
- Learn: What makes a runbook useful to AI retrieval.
- Build: Add 5 sample runbooks for common SRE issues.
- Output: `runbooks/*.md`.
- Resources: your team runbooks, Kubernetes troubleshooting docs.

### Day 12: Create Sample Alert Documents
- Learn: Alarm metadata: severity, query, owner, service, runbook.
- Build: Add alert docs or YAML examples.
- Output: `runbooks/alerts/*.md` or `.yaml`.
- Resources: Prometheus alerting docs.

### Day 13: Create Sample Incident Timeline Documents
- Learn: Incident timeline structure.
- Build: Add 3 realistic incident timelines.
- Output: `runbooks/incidents/*.md`.
- Resources: Google SRE incident management chapters, internal incident notes if allowed.

### Day 14: Create Service Metadata Files
- Learn: Service ownership, dependencies, dashboards, runbooks.
- Build: Add `services/*.yaml`.
- Output: service catalog seed.
- Resources: Backstage service catalog concepts, Kubernetes labels docs.

### Day 15: Build Corpus Loader
- Learn: Reading local docs safely.
- Build: Python loader for runbooks, alerts, incidents, services.
- Output: parsed document list.
- Resources: pathlib docs, Pydantic docs.

### Day 16: Add Document Chunking
- Learn: Why chunk size matters for retrieval.
- Build: Split docs into chunks with metadata.
- Output: chunked corpus JSON.
- Resources: LangChain text splitter concepts or LlamaIndex chunking docs.

### Day 17: Add Corpus Version Metadata
- Learn: Why retrieval answers need corpus versions.
- Build: Generate corpus hash/version.
- Output: `corpus_version` in `/version`.
- Resources: Python hashlib docs.

### Day 18: Add Citation Data Model
- Learn: Source citation requirements.
- Build: Models for source file, title, section, line/chunk ID.
- Output: citation schema.
- Resources: Pydantic docs.

### Day 19: Add Unknown-When-Unsupported Contract
- Learn: Why AI assistants must say unknown.
- Build: Response contract with answer, citations, confidence, unknown reason.
- Output: answer response schema.
- Resources: OWASP LLM Top 10.

### Day 20: Corpus Seed Capstone
- Learn: Review corpus quality.
- Build: Demo corpus loading, chunking, and versioning.
- Output: corpus seed report.
- Resources: all Week 2 resources.

### Day 21: Add Hosted LLM Client Wrapper
- Learn: Why model calls need a wrapper, not direct calls everywhere.
- Build: `model_client` interface with provider stub.
- Output: controlled model client.
- Resources: chosen provider docs, Pydantic docs.

### Day 22: Add Timeout Handling
- Learn: Timeout behavior and user-facing errors.
- Build: Timeout config and tests.
- Output: model timeout handling.
- Resources: httpx timeout docs.

### Day 23: Add Retry and Error Taxonomy
- Learn: Retryable vs non-retryable errors.
- Build: error classes for timeout, rate limit, bad response, provider unavailable.
- Output: model error taxonomy.
- Resources: Google SRE handling overload/retries, httpx docs.

### Day 24: Add Model Allowlist
- Learn: Model governance basics.
- Build: allowlist config for approved models.
- Output: rejected unapproved model request.
- Resources: OWASP LLM Top 10.

### Day 25: Add Prompt Versioning
- Learn: Prompt changes are releases.
- Build: prompt templates with version IDs.
- Output: prompt version in `/version`.
- Resources: prompt management articles from provider docs.

### Day 26: Add Basic SRE Question Endpoint
- Learn: API contract for AI responses.
- Build: `POST /ask` using stubbed model.
- Output: question-answer endpoint.
- Resources: FastAPI request body docs.

### Day 27: Add Runbook Q&A Prompt Template
- Learn: How to constrain answer style.
- Build: prompt for SRE runbook Q&A.
- Output: versioned prompt file.
- Resources: OWASP LLM Top 10.

### Day 28: Add Token Usage Tracking
- Learn: Tokens as capacity and cost unit.
- Build: track input/output token counts, stub if needed.
- Output: usage metadata in response.
- Resources: provider token/cost docs.

### Day 29: Add Cost Tracking Stub
- Learn: Cost/request and cost/hour.
- Build: cost calculator from configured model rates.
- Output: cost metrics in logs.
- Resources: provider pricing docs.

### Day 30: Controlled LLM Client Capstone
- Learn: Review model wrapper reliability.
- Build: demo timeout, allowlist, version, usage, cost.
- Output: LLM client demo note.
- Resources: Week 3 resources.

### Day 31: Add Embedding Client Wrapper
- Learn: Embeddings for semantic search.
- Build: embedding interface with stub/local option.
- Output: embedding client.
- Resources: vector search overview, provider embedding docs.

### Day 32: Build Local Vector Index
- Learn: vector index basics.
- Build: in-memory or local FAISS/Chroma index.
- Output: searchable chunk index.
- Resources: FAISS or Chroma docs.

### Day 33: Ingest Runbooks into Vector Store
- Learn: ingestion pipeline.
- Build: load, chunk, embed, index.
- Output: indexed runbook corpus.
- Resources: selected vector DB docs.

### Day 34: Retrieve Top-K Runbook Chunks
- Learn: top-k retrieval and relevance.
- Build: retrieval function with metadata.
- Output: retrieved chunks for query.
- Resources: vector search docs.

### Day 35: Generate Answers with Citations
- Learn: grounding and citation enforcement.
- Build: retrieve, prompt, answer, cite.
- Output: cited answers.
- Resources: OWASP LLM Top 10.

### Day 36: Add Citation Validation Tests
- Learn: tests for answer contracts.
- Build: fail answer if citations missing when context used.
- Output: citation tests.
- Resources: pytest docs.

### Day 37: Add Weak-Context Unknown Tests
- Learn: hallucination control.
- Build: tests for unrelated questions returning unknown.
- Output: unknown behavior tests.
- Resources: OWASP LLM Top 10.

### Day 38: Add RAG Evaluation Questions
- Learn: golden question set.
- Build: 20 runbook questions with expected sources.
- Output: `evals/golden_questions.yaml`.
- Resources: pytest parametrization docs.

### Day 39: Track Embedding and Corpus Versions
- Learn: retrieval reproducibility.
- Build: response includes embedding model and corpus version.
- Output: RAG version metadata.
- Resources: hashlib docs.

### Day 40: RAG v1 Capstone
- Learn: evaluate RAG behavior.
- Build: demo runbook Q&A with citations and unknown behavior.
- Output: RAG v1 report.
- Resources: Week 4 resources.

### Day 41: Design Tool-Calling Contract
- Learn: tool calls as controlled operations.
- Build: tool request/response schema.
- Output: tool contract ADR.
- Resources: OWASP LLM Top 10.

### Day 42: Add Read-Only Healthcheck Tool
- Learn: safe read-only operational tools.
- Build: tool returns service health from sample data.
- Output: healthcheck tool.
- Resources: FastAPI dependency docs.

### Day 43: Add Show Alerts Tool
- Learn: alert summaries and severity.
- Build: sample alert query tool.
- Output: `show_alerts` tool.
- Resources: Prometheus alerting docs.

### Day 44: Add Fetch Logs Tool
- Learn: logs as untrusted input.
- Build: sample log retrieval tool.
- Output: `fetch_logs` tool.
- Resources: OpenTelemetry logs concepts.

### Day 45: Add Incident Notes Tool
- Learn: incident context and timeline summaries.
- Build: retrieve incident timeline notes.
- Output: `incident_notes` tool.
- Resources: SRE incident management references.

### Day 46: Add Service Metadata Tool
- Learn: service ownership and dependency lookups.
- Build: service metadata lookup tool.
- Output: `service_metadata` tool.
- Resources: service catalog docs.

### Day 47: Add Tool Router
- Learn: routing approved tool calls.
- Build: tool registry and dispatcher.
- Output: tool router.
- Resources: Python protocols/typing docs.

### Day 48: Add Tool Allowlist Policy
- Learn: least privilege for AI tools.
- Build: reject unapproved tool names.
- Output: policy-enforced tool calls.
- Resources: OWASP LLM Top 10.

### Day 49: Log Tool Authorization Decisions
- Learn: auditability.
- Build: structured logs for allowed/blocked tools.
- Output: authorization logs.
- Resources: Python logging docs.

### Day 50: Read-Only Tooling Capstone
- Learn: tool safety review.
- Build: demo health, alerts, logs, incident notes, service metadata.
- Output: tools demo report.
- Resources: Week 5 resources.

### Day 51: Treat Tool Output as Untrusted Input
- Learn: prompt injection via tool output.
- Build: mark tool output as data in prompt.
- Output: untrusted tool output prompt section.
- Resources: OWASP LLM Top 10.

### Day 52: Add Prompt Injection Test from Alert Text
- Learn: malicious alert payloads.
- Build: alert text says "ignore instructions"; assistant refuses.
- Output: safety test.
- Resources: OWASP LLM Top 10.

### Day 53: Add Prompt Injection Test from Logs
- Learn: malicious logs.
- Build: log text tries to override system behavior.
- Output: safety test.
- Resources: OWASP LLM Top 10.

### Day 54: Add Prompt Injection Test from Runbooks
- Learn: poisoned documentation.
- Build: retrieved runbook contains unsafe instruction.
- Output: safety test.
- Resources: OWASP LLM Top 10.

### Day 55: Add Risk Classes for Actions
- Learn: read-only, write, destructive, privileged action classes.
- Build: risk classifier for tool/action requests.
- Output: action risk model.
- Resources: NIST AI RMF.

### Day 56: Add Human Approval Required Contract
- Learn: approval gates.
- Build: response requiring approval for risky actions.
- Output: approval-required response.
- Resources: OWASP LLM Top 10.

### Day 57: Block Destructive Actions by Default
- Learn: safe defaults.
- Build: policy blocks destructive actions.
- Output: blocked action tests.
- Resources: NIST AI RMF.

### Day 58: Add Audit Log for AI Decisions
- Learn: audit trail for AI-assisted ops.
- Build: decision log with request ID, prompt version, tool decision.
- Output: audit log.
- Resources: OpenTelemetry logs concepts.

### Day 59: Add Safe Incident Summary Endpoint
- Learn: summarization without action-taking.
- Build: summarize alert/log/incident bundle with citations.
- Output: `POST /incident/summary`.
- Resources: FastAPI docs.

### Day 60: Safety and Policy Capstone
- Learn: safety demo.
- Build: demo prompt injection defense, tool allowlist, approval gate.
- Output: safety report.
- Resources: Week 6 resources.

### Day 61: Add Structured Application Logs
- Learn: JSON logs for operations.
- Build: structured logs with request ID.
- Output: JSON log events.
- Resources: Python logging docs.

### Day 62: Add OpenTelemetry Trace IDs
- Learn: traces across service components.
- Build: basic tracing setup or trace ID propagation.
- Output: trace ID in responses/logs.
- Resources: OpenTelemetry Python docs.

### Day 63: Add Prometheus Metrics Endpoint
- Learn: metrics exposition.
- Build: `/metrics` endpoint.
- Output: Prometheus-compatible metrics.
- Resources: Prometheus Python client docs.

### Day 64: Track Request Latency
- Learn: p50/p95/p99 latency.
- Build: histogram for API latency.
- Output: request latency metrics.
- Resources: Prometheus histogram docs.

### Day 65: Track LLM Latency and Timeout Rate
- Learn: provider reliability metrics.
- Build: model latency, timeout, error counters.
- Output: model metrics.
- Resources: Prometheus docs.

### Day 66: Track Token and Cost Metrics
- Learn: cost observability.
- Build: token and cost counters.
- Output: cost/request metrics.
- Resources: provider pricing docs.

### Day 67: Track RAG Quality Metrics
- Learn: quality observability.
- Build: citation present, unknown returned, retrieved chunk count.
- Output: RAG quality metrics.
- Resources: evaluation notes.

### Day 68: Track Safety Metrics
- Learn: safety observability.
- Build: prompt injection detected, tool blocked, approval required counters.
- Output: safety metrics.
- Resources: OWASP LLM Top 10.

### Day 69: Create Grafana Dashboard JSON
- Learn: dashboard design for AI ops.
- Build: dashboard panels for latency, errors, cost, quality, safety.
- Output: `dashboards/ai-sre-assistant.json`.
- Resources: Grafana dashboard docs.

### Day 70: Observability Capstone
- Learn: operational review.
- Build: demo logs, metrics, dashboard JSON.
- Output: observability report.
- Resources: Week 7 resources.

### Day 71: Create Golden Incident Question Set
- Learn: eval data design.
- Build: 30 golden questions across runbooks, alerts, logs, incidents.
- Output: eval dataset.
- Resources: pytest parametrization docs.

### Day 72: Add Eval Runner
- Learn: repeatable AI evaluation.
- Build: script to run golden questions.
- Output: eval runner.
- Resources: Python argparse docs.

### Day 73: Score Citation Presence
- Learn: citation quality gates.
- Build: citation score.
- Output: eval score field.
- Resources: pytest docs.

### Day 74: Score Unknown-on-Weak-Context Behavior
- Learn: hallucination guardrail evaluation.
- Build: unknown score.
- Output: weak-context eval.
- Resources: OWASP LLM Top 10.

### Day 75: Score Tool-Use Correctness
- Learn: tool selection evaluation.
- Build: expected tool vs actual tool score.
- Output: tool eval.
- Resources: tool contract docs.

### Day 76: Add Bad Retrieval Regression Test
- Learn: stale/bad retrieval incidents.
- Build: test wrong runbook does not produce confident answer.
- Output: regression test.
- Resources: RAG notes.

### Day 77: Add Provider Outage Regression Test
- Learn: model provider outage behavior.
- Build: test fallback/error response.
- Output: outage test.
- Resources: Google SRE reliability patterns.

### Day 78: Add Tool Failure Regression Test
- Learn: malformed/failed tool output.
- Build: test assistant handles failed tool response safely.
- Output: tool failure test.
- Resources: OWASP LLM Top 10.

### Day 79: Add Eval Report Artifact
- Learn: release evidence.
- Build: markdown/JSON eval report.
- Output: `evals/reports/latest.md`.
- Resources: Python JSON docs.

### Day 80: Evaluation Capstone
- Learn: quality gate review.
- Build: run evals and write release gate result.
- Output: eval capstone report.
- Resources: Week 8 resources.

### Day 81: Create Dockerfile
- Learn: containerizing FastAPI.
- Build: Dockerfile for the app.
- Output: local container image.
- Resources: Docker docs.

### Day 82: Add Docker Compose
- Learn: local service composition.
- Build: compose file for app and optional metrics dependencies.
- Output: `docker-compose.yml`.
- Resources: Docker Compose docs.

### Day 83: Add Container Healthcheck
- Learn: Docker healthchecks.
- Build: healthcheck calling `/health`.
- Output: healthy container.
- Resources: Dockerfile HEALTHCHECK docs.

### Day 84: Add Graceful Shutdown
- Learn: shutdown behavior.
- Build: app lifespan hooks/logs.
- Output: graceful stop behavior.
- Resources: FastAPI lifespan docs.

### Day 85: Add Kubernetes Deployment
- Learn: basic Kubernetes workload.
- Build: deployment manifest.
- Output: `manifests/k8s/deployment.yaml`.
- Resources: Kubernetes deployment docs.

### Day 86: Add Kubernetes Service
- Learn: service exposure.
- Build: service manifest.
- Output: `service.yaml`.
- Resources: Kubernetes service docs.

### Day 87: Add Liveness and Readiness Probes
- Learn: probe configuration.
- Build: probes for `/health` and `/ready`.
- Output: probe-ready manifest.
- Resources: Kubernetes probe docs.

### Day 88: Add ConfigMap and Secret Placeholders
- Learn: config separation.
- Build: config map and secret examples with no real secrets.
- Output: config manifests.
- Resources: Kubernetes ConfigMap and Secret docs.

### Day 89: Add Helm Chart Skeleton
- Learn: packaging Kubernetes apps.
- Build: minimal Helm chart.
- Output: `manifests/helm/ai-sre-assistant`.
- Resources: Helm docs.

### Day 90: Deployable App Capstone
- Learn: deployment review.
- Build: run container locally, validate manifests.
- Output: deployment report.
- Resources: Week 9 resources.

### Day 91: Incident Drill - Bad Retrieval
- Learn: operating AI retrieval failures.
- Build: drill doc and test evidence.
- Output: bad retrieval incident drill.
- Resources: SRE incident management references.

### Day 92: Incident Drill - LLM Provider Outage
- Learn: provider failure handling.
- Build: drill with outage/fallback behavior.
- Output: provider outage drill.
- Resources: SRE reliability patterns.

### Day 93: Incident Drill - Latency Spike
- Learn: latency debugging.
- Build: inject slow model/tool response and observe metrics.
- Output: latency spike drill.
- Resources: Prometheus/Grafana docs.

### Day 94: Incident Drill - Prompt Injection
- Learn: security incident response for AI.
- Build: prompt injection drill.
- Output: safety incident drill.
- Resources: OWASP LLM Top 10.

### Day 95: Incident Drill - Tool Failure
- Learn: tool failure containment.
- Build: malformed tool output drill.
- Output: tool failure drill.
- Resources: tool contract docs.

### Day 96: Add Rollback Plan
- Learn: rollback for app, prompt, model, embedding, corpus.
- Build: rollback plan document.
- Output: `docs/rollback-plan.md`.
- Resources: Git, deployment docs.

### Day 97: Capstone Part 1 - Runbook Q&A
- Learn: demo flow.
- Build: polished demo for cited runbook answers.
- Output: demo script section.
- Resources: project README.

### Day 98: Capstone Part 2 - Alert and Log Summarization
- Learn: operational assistant workflow.
- Build: polished demo for alert/log/incident summary.
- Output: demo script section.
- Resources: project docs.

### Day 99: Capstone Part 3 - Safety, Evals, Observability
- Learn: production readiness evidence.
- Build: run safety tests, evals, metrics demo.
- Output: readiness evidence.
- Resources: project evals and dashboards.

### Day 100: Final Demo - AI SRE Assistant Production Readiness Review
- Learn: presenting engineering work.
- Build: final README, architecture, demo script, known gaps, next roadmap.
- Output: final capstone review.
- Resources: all project docs.

## Milestone Summary

- Day 10: API skeleton foundation
- Day 20: operational corpus seed
- Day 30: controlled LLM client
- Day 40: RAG v1 with citations
- Day 50: read-only SRE tools
- Day 60: safety and policy layer
- Day 70: observability package
- Day 80: evaluation package
- Day 90: deployable app
- Day 100: final AI SRE Assistant demo

