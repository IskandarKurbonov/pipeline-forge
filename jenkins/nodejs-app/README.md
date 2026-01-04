# Node.js Application Pipeline

Complete Jenkins pipeline for Node.js applications with testing, building, Docker containerization, and deployment.

## Features

- ✅ Automated dependency installation
- ✅ Code linting with ESLint
- ✅ Unit testing with coverage reports
- ✅ Security scanning with npm audit
- ✅ Docker image building and pushing
- ✅ Automated deployment
- ✅ Health checks
- ✅ Slack/Email notifications

## Prerequisites

- Jenkins with Docker support
- Node.js 18+ installed on Jenkins agent
- Docker registry credentials configured in Jenkins
- Git repository access

## Setup

### 1. Jenkins Credentials

Create the following credentials in Jenkins:

- **docker-registry-credentials**: Username/password for Docker registry
- **git-credentials**: (Optional) Git repository access

### 2. Project Structure

Your Node.js project should have:

```
your-project/
├── Jenkinsfile (copy from this template)
├── package.json
├── Dockerfile
├── .eslintrc.js (optional)
└── src/
```

### 3. package.json Scripts

Add these scripts to your `package.json`:

```json
{
  "scripts": {
    "lint": "eslint src/",
    "test:unit": "jest --ci --coverage",
    "build": "npm run compile"
  }
}
```

### 4. Jenkins Job Configuration

1. Create new Pipeline job in Jenkins
2. Configure SCM (Git repository)
3. Set branch to build (e.g., `main`, `develop`)
4. Pipeline definition: "Pipeline script from SCM"
5. Script path: `Jenkinsfile`

## Customization

### Environment Variables

Edit these in the Jenkinsfile:

```groovy
environment {
    NODE_VERSION = '18'              // Node.js version
    APP_NAME = 'your-app-name'       // Your application name
    DOCKER_REGISTRY = 'docker.io'    // Your Docker registry
    DEPLOY_ENV = 'production'        // Deployment environment
}
```

### Deployment Stage

Replace the placeholder deployment script with your actual deployment:

```groovy
stage('Deploy') {
    steps {
        script {
            // Kubernetes deployment
            sh 'kubectl apply -f k8s/deployment.yaml'

            // OR Docker Compose
            sh 'docker-compose -f docker-compose.prod.yml up -d'

            // OR SSH to remote server
            sh 'ssh user@server "docker pull ${DOCKER_IMAGE} && docker-compose up -d"'
        }
    }
}
```

### Notifications

Uncomment and configure Slack notifications:

```groovy
post {
    success {
        slackSend(
            color: 'good',
            channel: '#deployments',
            message: "Build #${BUILD_NUMBER} succeeded for ${APP_NAME}"
        )
    }
    failure {
        slackSend(
            color: 'danger',
            channel: '#deployments',
            message: "Build #${BUILD_NUMBER} failed for ${APP_NAME}"
        )
    }
}
```

## Pipeline Stages Explained

### 1. Checkout
Retrieves source code from Git repository

### 2. Environment Setup
Verifies Node.js and npm versions

### 3. Install Dependencies
Runs `npm ci` for clean, reproducible builds

### 4. Code Linting
Runs ESLint to check code quality

### 5. Unit Tests
Executes tests and generates coverage reports

### 6. Build Application
Compiles/bundles the application

### 7. Security Scan
Checks for vulnerable dependencies

### 8. Build Docker Image
Creates Docker container image (main branch only)

### 9. Push to Registry
Uploads image to Docker registry (main branch only)

### 10. Deploy
Deploys to target environment (main branch only)

### 11. Health Check
Verifies application is running correctly

## Troubleshooting

### Build Fails at npm install

```bash
# Clear npm cache on Jenkins agent
npm cache clean --force
```

### Docker build fails

```bash
# Check Docker daemon is running
systemctl status docker

# Verify Dockerfile exists
ls -la Dockerfile
```

### Tests timeout

Increase timeout in Jenkinsfile:

```groovy
options {
    timeout(time: 60, unit: 'MINUTES')
}
```

## Best Practices

1. **Use npm ci instead of npm install** - Faster, more reliable builds
2. **Enable branch protection** - Only allow merges with passing builds
3. **Cache node_modules** - Speed up subsequent builds
4. **Run tests in parallel** - Reduce build time
5. **Use semantic versioning** - Tag Docker images properly
6. **Implement rollback strategy** - Keep previous working images

## Example Dockerfile

```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

COPY . .

EXPOSE 3000

CMD ["node", "src/index.js"]
```

## Support

For issues or questions, contact:
- **Email**: kurbonoviskandar23@gmail.com
- **Telegram**: [@iskandar2318](https://t.me/iskandar2318)
