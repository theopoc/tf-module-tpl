# tf-module-tpl

[![GitHub Release](https://img.shields.io/github/v/release/theopoc/tf-module-tpl?style=flat-square)](https://github.com/theopoc/tf-module-tpl/releases)
[![License](https://img.shields.io/badge/license-Apache--2.0-blue?style=flat-square)](LICENSE)
[![Release](https://img.shields.io/github/actions/workflow/status/theopoc/tf-module-tpl/release.yml?style=flat-square&label=release)](https://github.com/theopoc/tf-module-tpl/actions/workflows/release.yml)
[![Copier](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/copier-org/copier/master/img/badge/badge-grayscale-inverted-border-orange.json)](https://github.com/copier-org/copier)

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

## License

This template is licensed under Apache-2.0. Generated modules inherit this license.

## Contributing

Found an issue or want to improve the template? Feel free to open an issue or pull request on [GitHub](https://github.com/theopoc/tf-module-tpl).
