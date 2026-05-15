---
name: ci-cd-pipeline-architecture
description: When configuring automated build, test, and deployment workflows for a repository.
version: 1.0.0
tags: [dev-tools, ci-cd, automation, devops]
---

# CI/CD Pipeline Architecture

## When to use
- Setting up a new GitHub Actions, GitLab CI, or Jenkins workflow.
- Automating manual deployment processes.
- Enforcing code quality checks on Pull Requests.

## What it does
Creates an automated, deterministic pipeline that ensures code integrates smoothly, passes all quality gates, and is deployed safely via immutable artifacts.

## Workflow
1. **Trigger Definition**: Define strict triggers. Run tests/linters on `pull_request`. Run builds/deployments on `push` to `main` or upon `release` tags.
2. **Fail Fast**: Order jobs sequentially by speed. Run Linters, Formatters, and Type Checkers first. If they fail, halt the pipeline before running expensive test suites.
3. **Automate Testing**: Run unit and integration tests inside isolated, ephemeral containers (e.g., Docker).
4. **Build Immutable Artifacts**: Compile code or build a Docker image exactly *once*. Tag the artifact with the Git commit SHA.
5. **Promote the Artifact**: Deploy the *exact same artifact* from Staging to Production. Do not rebuild the code for the production deployment.

## Rules
- Secrets/API keys must be injected via the CI/CD platform's secret manager, never hardcoded in pipeline files.
- The pipeline must fail immediately if any step returns a non-zero exit code.
- Artifacts must be immutable.

## Anti-patterns
- **Rebuilding for Environments**: Running `npm run build` in the staging pipeline, and then running `npm run build` again in the production pipeline.
- **Flaky Test Tolerance**: Ignoring failing tests by adding `continue-on-error: true` instead of fixing or isolating the test.
- **Deploying from Local**: A developer running `deploy.sh` from their laptop rather than pushing code to trigger the CI/CD pipeline.

## Output format
A declarative pipeline YAML file structured with isolated jobs, explicit dependency mapping (e.g., `needs: [build]`), and secure environment variable injection.
