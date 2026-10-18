# Workflow Lab 🔧

> **Reusable GitHub Actions, composite workflows, and automation templates for the Arise GenOps ecosystem.**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

## 📦 Workflows

| Workflow | Description | Usage |
|----------|-------------|-------|
| `python-ci` | Lint, type-check, test Python packages | `uses: abhiachar126-s/workflow-lab/.github/workflows/python-ci.yml@main` |
| `node-ci` | Lint, build, test Node.js packages | `uses: abhiachar126-s/workflow-lab/.github/workflows/node-ci.yml@main` |
| `security-scan` | CodeQL + TruffleHog + Trivy | `uses: abhiachar126-s/workflow-lab/.github/workflows/security-scan.yml@main` |
| `docker-build` | Multi-arch Docker build & push | `uses: abhiachar126-s/workflow-lab/.github/workflows/docker-build.yml@main` |

<!-- X4-APEX-DIAGRAM-START:workflow-lab -->

```mermaid
flowchart LR
    CONSUMER[Consumer Repository] --> SELECT[Choose Reusable Workflow]
    SELECT --> PY[Python CI]
    SELECT --> NODE[Node CI]
    SELECT --> SEC[Security Scan]
    SELECT --> DOCKER[Docker Build and Push]
    PY --> CHECKS[Lint / Typecheck / Tests]
    NODE --> CHECKS
    SEC --> SARIF[Security Findings]
    DOCKER --> ARTIFACT[Build Artifact]
    CHECKS --> STATUS[Workflow Result]
    SARIF --> STATUS
    ARTIFACT --> STATUS
    STATUS --> GATE[Consumer Branch Protection or Review Gate]
```

<!-- X4-APEX-DIAGRAM-END:workflow-lab -->

## 🚀 Quick Start

```yaml
# .github/workflows/ci.yml
name: CI
on: [push, pull_request]
jobs:
  python:
    uses: abhiachar126-s/workflow-lab/.github/workflows/python-ci.yml@main
    with:
      python-version: '3.11'
      working-directory: './packages/my-package'
```

## 🏗️ Structure

```
.github/
  workflows/          # Reusable workflows
  actions/            # Composite actions
  scripts/            # Helper scripts
examples/             # Usage examples
docs/                 # Documentation
```

## 📜 License

MIT © 2026 Arise GenOps

## APEX Architecture Map

> Status: architecture documentation; implementation and deployment claims require independent verification.

```mermaid
flowchart LR
  Consumer[Sample consumer repository] --> Ref[Pin reusable workflow ref]
  Ref --> Workflow[Reusable workflow]
  Workflow --> Inputs[Validate declared inputs]
  Inputs --> Runner[Execute isolated job steps]
  Runner --> Artifact[Upload evidence artifact]
  Artifact --> ConsumerCheck[Consumer contract test]
  ConsumerCheck --> Result{Expected outputs and failure behavior?}
  Result -->|no| Fail[Fail consumer CI]
  Result -->|yes| Pass[Record compatible workflow version]
  Workflow --> Permissions[Least-privilege token permissions]
  Permissions --> Runner
  Ref --> PinCheck{Ref immutable or reviewed tag?}
  PinCheck -->|no| Warn[Flag supply-chain risk]
  PinCheck -->|yes| Inputs
```

**Evidence note:** A reusable workflow is validated only when a real consumer exercises both success and failure paths on the pinned reference.

