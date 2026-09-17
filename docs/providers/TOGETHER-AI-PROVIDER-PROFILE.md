# Together AI Provider Profile

**Status:** Proposed governed provider profile
**Owner:** AGENTROPOLIS-SOVEREIGNTY
**Applies to:** Intelligence Grid model/provider routing
**Verified:** 2026-09-17 against official Together AI documentation

## Primary rule

Together AI is a replaceable intelligence and compute supplier. It is not an AGENTROPOLIS control plane, identity authority, memory authority, policy authority, skill authority, or execution authority.

Applications and districts MUST NOT call Together AI directly for governed production workflows. Requests flow through the AGENTROPOLIS Model Gateway under an ATG Execution Envelope.

> Own the coordination layer. Rent replaceable capacity.

## Provider classification

| Field | Value |
|---|---|
| Provider | Together AI |
| Class | External model and compute provider |
| Authority | None beyond the bounded provider call |
| Default posture | Eligible only through Model Gateway policy |
| Secrets | External secret manager / runtime injection only |
| Memory ownership | AGENTROPOLIS |
| Prompt and policy ownership | AGENTROPOLIS |
| Route selection | ATG + sovereignty/economics policy |
| Risk gates | AEGIS |
| Audit | Receipt + immutable audit trail |
| Fallback requirement | Required for critical workflows |

## Verified capability surfaces

The provider adapter may expose only capabilities that are verified in the active provider catalog and pass AGENTROPOLIS evaluation.

Current official Together documentation exposes or documents:

- chat/text inference;
- structured outputs for supported models;
- OpenAI-compatible tool/function schemas for supported models;
- embeddings;
- reranking, including models that require Dedicated Endpoints;
- batch jobs;
- queued asynchronous jobs;
- fine-tuning and fine-tune checkpoints;
- code interpreter execution;
- dedicated deployments/endpoints;
- cluster-backed compute and storage patterns;
- image/video or other generative capabilities where present in the active catalog.

Provider documentation is evidence of product capability, not evidence that a specific model is approved for an AGENTROPOLIS workload.

## Service modes

### Serverless inference
Use for eligible low-to-medium-risk interactive workloads when data policy, latency, quality, and economics permit.

### Dedicated endpoint
Use when a capability requires dedicated serving, stronger isolation is required, or stable capacity/latency is justified.

### Batch / queue
Use for non-interactive work such as evaluation, classification, enrichment, embeddings, synthetic-data jobs, document processing, and other checkpointable workloads.

### Training / fine-tuning
Treat training as a separate governed lifecycle. Training data rights, privacy class, provenance, model license, checkpoint custody, evaluation, and rollback MUST be reviewed before deployment.

### Cluster / custom compute
Treat GPU clusters and custom deployments as compute supply, not as a new authority layer. Checkpoints, model artifacts, datasets, and orchestration state remain portable and recoverable outside the provider.

### Code interpreter
Treat provider-hosted code execution as a sandbox capability with its own AEGIS permission scope. It MUST NOT inherit the permissions, credentials, filesystem scope, or network authority of the requesting agent.

## Data classification

| Class | Description | Together eligibility |
|---|---|---|
| D0 | Public / non-sensitive | Allowed when model/provider is approved |
| D1 | Internal low sensitivity | Allowed with logging and route policy |
| D2 | Confidential | Dedicated/private route preferred; explicit policy required |
| D3 | Regulated / highly sensitive | Deny by default unless a separately approved deployment and jurisdiction policy exists |
| D4 | Sovereign secrets / root credentials / signing material | Never transmit to provider inference |

Provider eligibility never overrides district, jurisdiction, contractual, or user-consent restrictions.

## Mandatory route contract

Every provider call MUST bind to:

1. identity and mandate reference;
2. ATG Execution Envelope reference;
3. capability request;
4. data classification;
5. privacy and jurisdiction constraints;
6. budget ceiling;
7. latency target;
8. tool permission scope;
9. model/provider allowlist state;
10. fallback path;
11. receipt and audit destination.

A provider or model selection can narrow capability. It can never expand capability beyond the envelope.

## Critical-workflow fallback

Every critical Together-backed workflow MUST define:

- primary route;
- secondary external provider;
- local or sovereign fallback where technically possible;
- degraded deterministic mode for essential functions;
- documented migration path.

Identity, access control, audit, emergency messaging, wallet protections, account export, and governance locks MUST retain a no-model path.

## Circuit breaker

Reduce, quarantine, or stop Together traffic when any applicable trigger fires:

- material error-rate increase;
- latency SLO breach;
- unexpected price increase or budget breach;
- model behavior regression;
- provider/model removal;
- model license or terms change;
- security incident;
- geographic or jurisdiction restriction;
- data-use policy change;
- failed AGENTROPOLIS evaluation;
- receipt or provenance failure.

Circuit-breaker actions MUST be receipted.

## Economics

Do not route on token price alone. The economics plane evaluates expected completed-task cost:

`inference + compute + storage + bandwidth + tool_calls + retries + failed_attempts + human_review + switching_cost + settlement_cost`

Cheap provider pricing is an optimization opportunity, not a reason to create architectural dependence.

## Fine-tuning custody rules

Before any fine-tune:

- verify dataset ownership and training rights;
- remove secrets and prohibited sensitive content;
- record source/provenance and dataset hash;
- record base model, revision, license, training configuration, and provider job ID;
- retain validation results and checkpoint metadata;
- export or mirror portable artifacts when license and provider terms allow;
- evaluate the result in the AGENTROPOLIS Evaluation Arena;
- deploy only through normal route and AEGIS approval.

A fine-tuned model does not inherit permission to use the training data at runtime.

## Receipt minimum

A Together execution receipt records at minimum:

- request ID;
- envelope ID;
- provider = `together-ai`;
- provider service mode;
- model ID and version/revision when available;
- capability;
- data class;
- route-decision reason codes;
- input/output token or usage accounting when available;
- measured latency;
- provider-reported cost plus AGENTROPOLIS computed total-cost estimate;
- retry count;
- tool calls requested and allowed;
- policy decision references;
- fallback/circuit-breaker events;
- result hash or artifact reference;
- timestamp.

Do not store raw secrets in receipts.

## Provider adapter disable test

This integration is acceptable only while the following remains true:

> Disabling the Together adapter must not delete AGENTROPOLIS identity, memory, skills, policy, routing rules, evaluation data, audit history, or the ability to move critical workflows to another approved route.

## Official verification sources

- https://docs.together.ai/
- https://docs.together.ai/docs/inference/chat/structured-outputs
- https://docs.together.ai/docs/quickstart-retrieval-augmented-generation-rag
- https://docs.together.ai/reference/batch-list
- https://docs.together.ai/reference/upload-file
- https://docs.together.ai/reference/get-fine-tunes-id-checkpoint
- https://docs.together.ai/reference/tci-execute

## Relationship to canonical sovereignty doctrine

This profile specializes `docs/AI-SOVEREIGNTY-CONTINGENCY-PLAN.md`. Where this profile and the canonical sovereignty plan disagree, the stricter sovereignty rule governs until an explicit architecture change is approved.