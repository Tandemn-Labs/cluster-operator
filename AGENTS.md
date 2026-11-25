# AGENTS.md

This file is for coding agents. It is laid out as organization wide rules followed by repo-specific information.

## Organization guide

Context about Tandemn software is at tandemn.md

### Overall coding style
- Avoid clever one-liners that hurt readability.
- Use comments only for non-obvious operational logic. Do not comment what the code already says.
- Follow the existing local patterns before inventing a new one.
- Simplicity first. No features beyond what was asked. No abstractions for single-use code. No "flexibility" or "configurability" that wasn't requested. No error handling for impossible scenarios. Do not add unnecessary complexity in order to attain goals like scalability and security.
- Make only surgical changes. Touch only what is needed, don't improve or refractor anything that is not absolutely necessary.
- Ask questions for everything that is not clear from the prompt instead of assuming.

### Repository Boundaries
- Do not commit credentials, .env files, generated caches, local Docker volumes, or large artifacts.

## Repo-specific guide

This repo is for Tandemn's per-cluster Kubernetes operator. The main CRD that this operator will reconcile is ClusterPlan, and the operator will reconcile this into inference framework CRDs (e.g. Dynamo DGD, AIBrix StormService) or direct engine Pod / Deployments. There are 2 key responsibilities for this operator - (1) Reconcile ClusterPlan into inference-related resources; (2) Produce the ClusterResourceMap type and submit it to the control plane's resource map service periodically.