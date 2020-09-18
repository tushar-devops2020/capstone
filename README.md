# capstone
Udacity Nanodegree Cloud DevOps Capstone project repo

**Step-1** <br>
Deployment Strategy - Blue Green <br>
CI/CD Tool - Jenkins <br>
Install Jenkins on AWS EC2 Instance. <br>
Plugins - Blue Ocean, AWS <br>
Tools (to be installed on Jenkins server) - Tidy (Lint test for HTML) , Hadolint (Lint test for Dockerfile), eksctl, AWS CLI, kubectl, docker <br>
Application - Default Nginx docker image with our own web app. <br>

**Step-2** <br>
Pipeline 1 - Deploy Kubernetes cluster & Node on AWS EKS using Cloudformation stack via Jenkins pipeline. EC2 Instance will be created. <br>
(Files in ClusterInfra folder) <br>

**Step-3** <br>
Pipeline 2 - Build & Deploye the application End-To-End via Blue Green Deployment Strategy <br>

Stages - Lint HTML & Docker File -> Build Docker Image -> Push Docker image to Docker HUB -> Set kubectl context -> Deploy blue container (blue-controller.json) -> Deploy green container (green-controller.json) -> Create the service in the cluster, redirect to blue (blue-service.json) -> Ask user to approve to switch to Green node -> Create the service in the cluster, redirect to green (green-service.json) <br>

**Final** <br>
Application should be accessible via Load balancer public endpoint on port 8000 <br>
<br>
Files - <br>
blue-controller.json <br>
blue-service.json <br>
Dockerfile <br>
green-controller.json <br>
green-service.json <br>
index.html <br>
Jenkinsfile <br>
README.md <br>
ClusterInfra/Jenkinsfile <br>




