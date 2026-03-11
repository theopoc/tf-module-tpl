# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repository Is

A **Copier template** that scaffolds production-ready Terraform modules. It generates fully functional modules with pre-commit hooks, terraform-docs, semantic versioning, and CI/CD pipelines (GitHub Actions or GitLab CI).

## Commands

### Template development
```bash
uv sync --frozen                          # Install dependencies (copier)
uv run copier copy . /tmp/test-module     # Test template rendering locally
```

### CI testing (what the CI does)
The CI renders the template and validates the generated module. There is no local test runner — testing happens via GitHub Actions workflows.

## Architecture

### Template engine
- **Copier** (Python) renders `template/` using Jinja2
- Configuration and variable prompts are in `copier.yml`
- All template files use `.jinja` extension; conditional files/dirs use Jinja2 in filenames

### Key files
- `copier.yml` — 11 template variables (module name, CI provider, optional features), 11 post-generation tasks
- `template/` — Jinja2 source files that become the generated module
- `renovate.json` — custom regex managers track tool versions inside `template/.mise.toml.jinja` and `copier.yml`

### Template variables and feature flags
Most features are opt-in booleans: `use_tflint`, `use_trivy`, `use_pre_commit`, `use_semantic_release`, `use_examples`, `use_terraform_docs`. These gate entire files and blocks throughout the template.

`ci_provider` (github/gitlab) gates two entire CI pipeline subtrees.

### Generated module structure
The template produces a module with:
- `main.tf`, `variables.tf`, `outputs.tf`, `versions.tf`
- `.mise.toml` with tool versions and tasks (`format`, `validate`, `docs`, `lint`)
- Optional: pre-commit hooks, commitlint, semantic-release, terraform-docs, tflint, trivy, examples/

### Renovate custom managers
`renovate.json` uses regex managers to track versions pinned inside template Jinja files — not regular dependency files. When adding new tool versions to the template, a matching custom manager entry is needed to keep them updated.

**Every change to `renovate.json` must be validated before committing:**
```bash
npx --yes --package renovate@41 -- renovate-config-validator
```
> **Important:** always pin `renovate@41` (or the current major). Without it, `npx` may pull a cached older version (e.g. v37) whose supported manager list differs, producing false errors.

### Release process
This repo uses semantic-release itself (via `package.json` + `.releaserc.json`). Releases are cut automatically on push to `main`. The `chore(deps)` scope triggers a patch release.

### CI workflows
- `.github/workflows/ci.yml` — renders template for both CI providers, then tests the generated pipelines with `act` (GitHub) and `gitlab-ci-local` (GitLab)
- `.github/workflows/release.yml` — runs `npx semantic-release` on main branch pushes
