# Project Overview: CICD with Kubernetes

## Overview
This project focuses on facilitating Continuous Deployment (CD) for Docker containers on Kubernetes (K8s). This README provides an overview of the project's objectives, workflow, code repositories, infrastructure setup, and necessary configurations.

### Summary
The primary objective of this project is to streamline the deployment process by automating various stages, including code changes, testing, analysis, Docker image building, and deployment onto a Kubernetes cluster. The workflow involves using Jenkins pipelines to orchestrate these tasks seamlessly.

### Workflow
The workflow consists of the following steps:
1. Making code changes and pushing them to the repository triggers a Jenkins pipeline.
2. Jenkins pipeline fetches the code and performs testing and analysis using SonarQube.
3. Test results are uploaded to SonarQube for analysis.
4. A Docker image is built and pushed to DockerHub.
5. Helm charts are used for Kubernetes deployment.
6. Jenkins pipeline deploys the Helm chart onto the Kubernetes cluster.

### Infrastructure
The project utilizes the following EC2 instances:
- **kops**: Used for managing the Kubernetes cluster.
- **sonar**: Hosts the SonarQube instance for code analysis.
- **jenkins**: Jenkins server orchestrating the CI/CD pipeline.

### Configuration
- Security Group Configurations:
  - Allow traffic between Jenkins and SonarQube within their security groups.
  - Permit SSH from the Jenkins EC2 instance to the Kops (Jenkins slave) security group.

- Jenkins Pipeline Configuration:
  - Helm charts are created, and Docker image details are set as Helm variables.
  - During the pipeline execution, Helm upgrade is performed, passing Docker image name and tag as values.
  - Jenkins EC2 instance is accessed via SSH to install Docker and restart Jenkins processes.
  - Necessary plugins such as Docker Pipeline and Pipeline Utility Steps are installed on Jenkins.

- Kubernetes Cluster Configuration:
  - Kops EC2 instance is accessed via SSH to create the Kubernetes cluster.
  - Helm and Java are installed on the Kubernetes cluster.
  - Two namespaces, namely 'test' and 'prod', are created on Kubernetes.
  - Jenkins slave is added to Jenkins for pipeline execution.

### Additional Steps
- Creation of new jobs on Jenkins for specific tasks.

## Getting Started
To begin using this project, follow these steps:
1. Clone the relevant code repositories mentioned above.
2. Configure the necessary infrastructure, including EC2 instances and security groups.
3. Set up Jenkins pipelines according to the workflow mentioned.
4. Ensure proper configuration of Kubernetes clusters and namespaces.
5. Execute Jenkins jobs for desired tasks.
