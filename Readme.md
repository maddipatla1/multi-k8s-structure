# GitHub Actions Workflow: Deploy to ECR and Kubernetes

This GitHub Actions workflow automates the process of building Docker images, pushing them to Amazon Elastic Container Registry (ECR), and deploying the updated images to a Kubernetes cluster. The workflow is triggered whenever changes are pushed to the `main` branch.

## Workflow Overview

1. **Checkout Code**: The workflow starts by checking out the source code from your repository.

2. **Configure AWS Credentials**: AWS credentials are configured using secrets stored in your GitHub repository. These credentials are necessary for logging into Amazon ECR.

3. **Login to Amazon ECR**: The workflow logs into Amazon ECR to authenticate the Docker image push.

4. **Build, Tag, and Push Docker Images to ECR**: Docker images for your application components (client, server, worker) are built, tagged with the latest commit hash, and pushed to Amazon ECR. The images are tagged and pushed using secrets stored in your GitHub repository.

5. **Set kubeconfig from Secret**: The Kubernetes configuration (`kubeconfig`) is set from a GitHub secret named `KUBECONFIG`. This allows the workflow to access your Kubernetes cluster.

6. **Deploy to Kubernetes**: The workflow deploys your application to Kubernetes using `kubectl`. It applies Kubernetes configuration files located in the `k8s` directory and updates the image versions to the newly pushed Docker images. The `kubeconfig` file is used for authentication.

## Secrets Required

Ensure you have the following secrets configured in your GitHub repository settings:

- `AWS_ACCESS_KEY_ID`: AWS Access Key ID for ECR authentication.
- `AWS_SECRET_ACCESS_KEY`: AWS Secret Access Key for ECR authentication.
- `AWS_REGION`: AWS region where your ECR repository is located.
- `DOCKER_REGISTRY`: Docker registry URL for storing your Docker images.
- `KUBECONFIG`: The `kubeconfig` file content for authenticating with your Kubernetes cluster.

## Workflow Customization

You may need to customize this workflow to fit your project's specific requirements. Here are some considerations:

- Modify the `branches` section in the `on` block to trigger the workflow on different branches if needed.
- Update the paths to your Dockerfiles and Kubernetes configuration files in the workflow as per your project structure.
- Adjust the names of Docker images and Kubernetes resources as needed.
- Uncomment and customize any additional steps or actions specific to your deployment process.

By using this GitHub Actions workflow, you can automate the deployment process of your application to Amazon ECR and Kubernetes whenever changes are pushed to your `main` branch.
