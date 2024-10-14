# Basic CI/CD Pipeline

This repository demonstrates a Continuous Integration and Continuous Deployment (CI/CD) pipeline using GitHub Actions. It includes a basic pipeline that builds, tests, and deploys a Python application, containerizes it with Docker, and deploys it to a Kubernetes cluster.

## Pipeline Overview

The pipeline is triggered on:

- Pushes to the `main` branch.
- Pull requests targeting the `main` branch.

### Jobs and Steps:

1. **Checkout Code**: The pipeline checks out the code from the GitHub repository.
2. **Set Up Python**: Installs Python version `3.9` to ensure the environment is ready for Python-based projects.
3. **Install Dependencies**: Installs the required Python dependencies from the `requirements.txt` file.
4. **Run Tests**: Executes tests using `pytest` to ensure code quality.
5. **Set Up Docker Buildx**: Sets up Docker Buildx to build multi-platform Docker images.
6. **Cache Docker Layers**: Uses caching to speed up Docker image builds by reusing previous layers.
7. **Build and Push Docker Image**: Builds and pushes the Docker image to the Docker registry with tags `latest` and a unique Git commit hash.
8. **Deploy to Kubernetes**: Deploys the Docker image to a Kubernetes cluster using the `kubectl` tool. The deployment context is set to `staging`, and the image for the application deployment is updated.

## Repository Structure

```
.github/
  workflows/
    ci-cd.yml       # GitHub Actions workflow for CI/CD pipeline
src/                 # Source code of the application
public/              # Static assets like images, stylesheets, etc.
terraform/           # Terraform configurations for infrastructure
Dockerfile           # Dockerfile for building the application container
package.json         # Node.js package configuration
package-lock.json    # Node.js package lock file
terraform.tfstate    # Terraform state file tracking infrastructure resources
```

## Requirements

- **Python**: Make sure to have Python 3.9 installed to run the tests.
- **Docker**: Docker should be installed and configured to build and push images.
- **Kubernetes**: Set up a Kubernetes cluster with the necessary permissions to deploy the application. The `KUBECONFIG` should be stored as a secret in the GitHub repository.

## Usage

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/Python-Docker-K8S-Infra.git
cd Python-Docker-K8S-Infra
```

### 2. Running Locally

To run the application locally, ensure you have Python, Docker, and Kubernetes set up:

```bash
# Install dependencies
pip install -r requirements.txt

# Run tests
pytest

# Build Docker image
docker build -t myapp:latest .

# Deploy to Kubernetes
kubectl apply -f k8s/deployment.yaml
```

### 3. CI/CD Workflow

The CI/CD pipeline will automatically:

- Run the tests.
- Build the Docker image.
- Push the image to a Docker registry.
- Deploy the image to your Kubernetes cluster.

### 4. Secrets Configuration

Ensure that the following GitHub secrets are configured in your repository:

- `KUBE_CONFIG`: The Kubernetes configuration file to connect and deploy to your cluster.

## Suggested Repo Name

You can name this repository **"Python-Docker-K8S-CICD"** or **"Automated-DevOps-Pipeline"** to reflect the integration of CI/CD, Docker, and Kubernetes.

---
