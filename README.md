# GitHub Actions Workflow Control Demo

This repository demonstrates advanced GitHub Actions workflow control techniques including job dependencies, conditional execution, and environment protection.

## 🚀 Features

- **Job Dependency Management**: Control execution order with `needs` keyword
- **Conditional Workflows**: Run jobs based on specific conditions
- **Manual Triggers**: Support for workflow_dispatch with custom inputs
- **Matrix Strategies**: Parallel execution across multiple configurations
- **Environment Protection**: Production deployment approval requirements
- **Scheduled Workflows**: Automated daily maintenance tasks

## 📁 Workflow Structure

### CI Pipeline (.github/workflows/ci.yml)
```yaml
name: CI Pipeline
on: [push, pull_request, workflow_dispatch]
```

**Jobs:**
- **lint**: ESLint code quality checks
- **test**: Parallel testing across Node.js versions (16.x, 18.x, 20.x)
- **security**: npm audit vulnerability scanning
- **build**: Project compilation and artifact creation

### CD Pipeline (.github/workflows/cd.yml)
```yaml
name: CD Pipeline
on:
  workflow_dispatch:
    inputs:
      environment:
        description: 'Deployment environment'
        required: true
        default: 'staging'
```

**Jobs:**
- **deploy-staging**: Automated deployment to staging
- **deploy-production**: Manual approval required for production
- **verify-deployment**: Health checks and verification

### Scheduled Workflow (.github/workflows/scheduled.yml)
```yaml
name: Scheduled Maintenance
on:
  schedule:
    - cron: '0 0 * * *'  # Daily at midnight
```

## 🛠️ Usage

### Manual Deployment
```bash
# Navigate to Actions → CD Pipeline → Run workflow
# Select environment (staging/production)
# Approve production deployment when prompted
```

### Local Development
```bash
npm test      # Run tests
npm run lint  # Code quality check
npm audit     # Security audit
```

## ⚙️ Configuration

### Required Secrets
- `STAGING_DEPLOY_KEY`: SSH key for staging environment
- `PRODUCTION_DEPLOY_KEY`: SSH key for production environment

### Environment Settings
Production environment requires:
- ✅ Deployment approval
- ✅ Reviewers
- ✅ Protected branches

## 📋 Example Usage

```yaml
# Example job dependency
deploy-production:
  needs: [test, build]
  environment: production
  if: github.ref == 'refs/heads/main'
```

## 🤝 Contributing

1. Fork this repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request



## 🔗 Resources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Workflow Syntax Guide](https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions)
- [Environments Documentation](https://docs.github.com/en/actions/reference/environments)

---

⭐ Star this repo if you found it helpful!
