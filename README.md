# tf-module-tpl

[![GitHub Release](https://img.shields.io/github/v/release/theopoc/tf-module-tpl?style=flat-square)](https://github.com/theopoc/tf-module-tpl/releases)
[![License](https://img.shields.io/badge/license-Apache--2.0-blue?style=flat-square)](LICENSE)
[![Release](https://img.shields.io/github/actions/workflow/status/theopoc/tf-module-tpl/release.yml?style=flat-square&label=release)](https://github.com/theopoc/tf-module-tpl/actions/workflows/release.yml)
[![Copier](https://img.shields.io/badge/copier-template-blueviolet?style=flat-square)](https://copier.readthedocs.io/)

A production-ready [Copier](https://copier.readthedocs.io/) template for scaffolding Terraform modules with best practices, pre-commit hooks, semantic versioning, and automated documentation generation.

## Features

✨ **Fully Automated Bootstrap**
- Git initialization and initial commit
- Terraform module structure with best practices
- Pre-commit hooks for code quality (fmt, docs, validate, tflint)
- Husky and commitlint for commit message validation
- Mise for reproducible tool management

📚 **Automated Documentation**
- terraform-docs integration for auto-generating documentation
- README template with usage examples
- Complete example module included

🚀 **Semantic Versioning**
- Semantic-release configured for automated versioning
- GitHub Actions workflow for automated releases
- Changelog generation

🔧 **Developer Experience**
- Optional AWS provider configuration
- Customizable module settings (name, description, author)
- Example with complete module usage

## Requirements

### Prerequisites

- **Python 3.10+** - Required by Copier
- **Git 2.27+** - For version control
- **Copier** - Project template engine

### Installation Methods

Choose one of the following installation methods for Copier:

#### Option 1: Using `pipx` (Recommended)

```bash
pipx install copier
```

#### Option 2: Using `uv`

```bash
uv tool install copier
```

#### Option 3: Using `pip`

```bash
pip install copier
```

## Quick Start

### Generate a New Terraform Module

```bash
copier copy https://github.com/theopoc/tf-module-tpl my-terraform-module
cd my-terraform-module
```

Copier will prompt you for the following information:

- **Module name** (e.g., `terraform-aws-mymodule`)
- **Module description** - Short description of your module
- **Terraform minimum version** (default: `1.9`)
- **Null provider version** (default: `~> 3.0`)
- **Author name** - Your name
- **GitHub repository** (e.g., `myorg/terraform-aws-mymodule`)
- **Use AWS provider?** - Whether to include AWS provider (yes/no)
  - If yes, you'll be prompted for:
    - AWS provider version (default: `~> 5.0`)
    - Default AWS region (default: `eu-west-1`)

### Example Usage

```bash
copier copy https://github.com/theopoc/tf-module-tpl my-module \
  --data module_name="terraform-aws-vpc" \
  --data module_description="AWS VPC Terraform module" \
  --data author_name="Your Name" \
  --data github_repo="myorg/terraform-aws-vpc" \
  --data use_aws_provider=true
```

## Generated Module Structure

```
my-terraform-module/
├── .github/workflows/
│   ├── lint.yml              # Terraform validation and linting
│   └── release.yml           # Semantic-release automation
├── .pre-commit-config.yaml   # Pre-commit hooks configuration
├── .commitlintrc.json        # Commit message validation
├── .mise.toml                # Tool version management
├── .env.example              # Environment variables template
├── main.tf                   # Main module code
├── variables.tf              # Input variables
├── outputs.tf                # Module outputs
├── versions.tf               # Terraform and provider versions
├── README.md                 # Auto-generated documentation
├── CHANGELOG.md              # Release changelog
├── package.json              # Node.js dependencies (commitlint, husky)
├── .gitignore                # Git ignore rules
├── examples/
│   └── complete/             # Complete usage example
└── .git/                      # Initialized git repository
```

## Features Explained

### Pre-commit Hooks

Automatically run on every commit:
- `terraform fmt` - Format Terraform files
- `terraform docs` - Generate documentation
- `terraform validate` - Validate Terraform syntax
- `terraform tflint` - Lint Terraform code
- `check-merge-conflict` - Detect merge conflicts
- `end-of-file-fixer` - Fix file endings
- `trailing-whitespace` - Remove trailing whitespace

### Commit Message Validation

Uses commitlint with conventional commits:
- `feat:` - New features
- `fix:` - Bug fixes
- `docs:` - Documentation
- `chore:` - Build and tooling
- `refactor:` - Code refactoring
- `perf:` - Performance improvements
- `test:` - Tests

### Tool Management with Mise

All development tools are managed via Mise:
```bash
mise install          # Install all configured tools
mise trust            # Trust .mise.toml file
mise run validate     # Run validation task
mise run format       # Format code
mise run docs         # Generate documentation
mise run lint         # Run linting
```

### GitHub Actions

**Lint Workflow** - Runs on every push and pull request:
- Terraform fmt check
- Terraform init
- Terraform validate
- tflint

**Release Workflow** - Runs on push to main:
- Analyzes conventional commits
- Determines version bump
- Creates GitHub release
- Updates CHANGELOG.md
- Pushes tags

## Customization

### Changing Tool Versions

Edit `.mise.toml`:
```toml
[tools]
terraform = "1.9"      # Change Terraform version
tflint = "0.52"        # Change tflint version
node = "20"            # Change Node.js version
```

### Modifying Pre-commit Hooks

Edit `.pre-commit-config.yaml` to add/remove hooks.

### Custom Release Configuration

Edit `.releaserc.json` to customize semantic-release behavior.

## Development

After module generation, start developing:

```bash
# Initialize Terraform
terraform init

# Format code
mise run format

# Validate module
mise run validate

# Generate/update documentation
mise run docs

# Run all linting
mise run lint

# Make changes and commit
git add .
git commit -m "feat: add new variable"

# Push to trigger release
git push origin main
```

## Template Versioning

This template itself is versioned using semantic-release. Check [releases](https://github.com/theopoc/tf-module-tpl/releases) for updates.

To update your module template to the latest version:

```bash
copier update
```

## Requirements for Generated Modules

Generated modules require:
- Terraform 1.9+ (or your configured minimum version)
- Null provider 3.0+ (or your configured version)
- AWS provider 5.0+ (if AWS provider is enabled)
- Git for version control
- Pre-commit framework (installed via npm)

## Troubleshooting

### Mise trust prompt

If you see "Config files are not trusted", run:
```bash
mise trust
```

### Pre-commit hook failures

Ensure all tools are installed:
```bash
mise install
pre-commit install
```

### Terraform validation errors

Check the Terraform syntax:
```bash
terraform fmt -recursive
terraform validate
```

## License

This template is licensed under Apache-2.0. Generated modules inherit this license.

## Contributing

Found an issue or want to improve the template? Feel free to open an issue or pull request on [GitHub](https://github.com/theopoc/tf-module-tpl).
