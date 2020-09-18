# capstone
Udacity Nanodegree Cloud DevOps Capstone project repo

**Step-1** 
Deployment Strategy - Blue Green <br>
CI/CD Tool - Jenkins <br>
Install Jenkins on AWS EC2 Instance.
Plugins - Blue Ocean, AWS
Tools (to be installed on Jenkins server) - Tidy (Lint test for HTML) , Hadolint (Lint test for Dockerfile), eksctl, AWS CLI, kubectl, docker
Application - Default Nginx docker image with our own web app.

**Step-2**
Pipeline 1 - Deploy Kubernetes cluster & Node on AWS EKS using Cloudformation stack via Jenkins pipeline. EC2 Instance will be created.
(Files in ClusterInfra folder)

**Step-3**
Pipeline 2 - Build & Deploye the application End-To-End via Blue Green Deployment Strategy

Stages - Lint HTML & Docker File -> Build Docker Image -> Push Docker image to Docker HUB -> Set kubectl context -> Deploy blue container (blue-controller.json) -> Deploy green container (green-controller.json) -> Create the service in the cluster, redirect to blue (blue-service.json) -> Ask user to approve to switch to Green node -> Create the service in the cluster, redirect to green (green-service.json)

**Final**
Application should be accessible via Load balancer public endpoint on port 8000

Files -
blue-controller.json
blue-service.json
Dockerfile
green-controller.json
green-service.json
index.html
Jenkinsfile
README.md
ClusterInfra/Jenkinsfile




