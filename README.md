# Pipeline Forge

> Production-ready CI/CD pipeline templates for Jenkins, GitLab CI, and GitHub Actions

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

## Overview

Pipeline Forge is a collection of battle-tested CI/CD pipeline templates that you can use to accelerate your DevOps workflow. Each pipeline is designed following industry best practices with security, performance, and maintainability in mind.

## Features

- **Multi-Platform Support**: Jenkins, GitLab CI, GitHub Actions
- **Production Ready**: Battle-tested configurations
- **Security First**: Built-in security scanning and best practices
- **Easy to Use**: Copy, customize, and deploy in minutes
- **Well Documented**: Clear instructions for each pipeline

## Pipeline Templates

### Jenkins Pipelines

- **Node.js Application** - Build, test, and deploy Node.js apps
- **Python Application** - Complete Python CI/CD with testing
- **Docker Build & Push** - Container image pipeline
- **Multi-Stage Pipeline** - Development → Staging → Production
- **Backup & Restore** - Automated backup pipelines

### GitLab CI

- **Microservices Pipeline** - Multi-service deployment
- **Kubernetes Deployment** - K8s integration
- **Auto DevOps** - Automated security and testing
- **Monorepo Pipeline** - Handle multiple projects

### GitHub Actions

- **Auto Release** - Automated versioning and releases
- **Code Quality** - Linting, testing, coverage
- **Container Registry** - Build and push to GHCR
- **Multi-Environment** - Deploy to multiple environments

## Quick Start

### Jenkins Example

```groovy
// Copy Jenkinsfile from templates/jenkins/nodejs-app/Jenkinsfile
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Deploy') {
            steps {
                sh './deploy.sh'
            }
        }
    }
}
```

### GitLab CI Example

```yaml
# Copy from templates/gitlab-ci/python-app/.gitlab-ci.yml
stages:
  - build
  - test
  - deploy

build:
  stage: build
  script:
    - pip install -r requirements.txt
    - python setup.py build
```

### GitHub Actions Example

```yaml
# Copy from templates/github-actions/docker-build/.github/workflows/build.yml
name: Docker Build and Push

on:
  push:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Build Docker image
        run: docker build -t myapp:latest .
```

## Directory Structure

```
pipeline-forge/
├── jenkins/
│   ├── nodejs-app/
│   ├── python-app/
│   ├── docker-build/
│   ├── multi-stage/
│   └── backup-pipeline/
├── gitlab-ci/
│   ├── microservices/
│   ├── kubernetes/
│   ├── auto-devops/
│   └── monorepo/
├── github-actions/
│   ├── auto-release/
│   ├── code-quality/
│   ├── container-registry/
│   └── multi-environment/
└── docs/
    ├── best-practices.md
    ├── security-guide.md
    └── troubleshooting.md
```

## Installation

1. Clone this repository:
```bash
git clone https://github.com/IskandarKurbonov/pipeline-forge.git
```

2. Choose the pipeline template you need

3. Copy the template to your project

4. Customize variables and settings

5. Commit and push to trigger the pipeline

## Customization

Each pipeline template includes:
- **Configuration variables** - Easily customize for your project
- **Environment setup** - Development, staging, production
- **Notification settings** - Slack, email, webhook integrations
- **Security scanning** - SAST, DAST, dependency scanning

## Best Practices

- Always use environment variables for sensitive data
- Implement proper secret management (HashiCorp Vault, AWS Secrets Manager)
- Enable branch protection rules
- Use pipeline caching for faster builds
- Implement automated rollback mechanisms
- Monitor pipeline metrics and performance

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingPipeline`)
3. Commit your changes (`git commit -m 'Add amazing pipeline'`)
4. Push to the branch (`git push origin feature/AmazingPipeline`)
5. Open a Pull Request

## Support

- **Issues**: Report bugs or request features via [GitHub Issues](https://github.com/IskandarKurbonov/pipeline-forge/issues)
- **Telegram**: [@iskandar2318](https://t.me/iskandar2318)
- **Email**: kurbonoviskandar23@gmail.com

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Author

**Iskandar Kurbonov**
- DevOps Engineer
- Location: Tashkent, Uzbekistan
- Specialization: CI/CD, Docker, Linux Administration

---

⭐ If you find this project useful, please give it a star!
