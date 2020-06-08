# Udacity Cloud DevOps Capstone Project

This is final project of Udacity Cloud DevOps Engineer Nanodegree.

## Project Setup

-   Create Jenkins server using cloud formation template.

```
$ sh scripts/create.sh jenkins-stack infrastructure/jenkins-server.yml infrastructure/jenkins-server-parameters.json
```

-   Following resources are created after executing above command:
    -   VPC
    -   Subnet
    -   Route Table
    -   Route
    -   Internet Gateway
    -   Security Group
    -   Launch Configuration
    -   Auto Scaling Group
-   Following tools are automatically installed in the server using Launch Configuration:
    -   Jenkins
    -   Docker
    -   AWS CLI
    -   eksctl CLI
    -   kubectl CLI
    -   Tidy
-   Once the stack creation is complete, access the Jenkins UI using `http://<EC2_PUBLIC_IP>:8080`
-   Login using admin account and complete the initial setup of Jenkins.
-   Install the following plugins in Jenkins:
    -   [CloudBees AWS Credentials](https://plugins.jenkins.io/aws-credentials/)
    -   [Pipeline: AWS Steps](https://plugins.jenkins.io/pipeline-aws/)
    -   [Blue Ocean](https://plugins.jenkins.io/blueocean/)
-   Add AWS credentials in Jenkins.
-   Create new item in Jenkins of type `Pipeline` of name let's say `infra-pipeline`
-   In the configuration page of `infra-pipeline`, provide the GitHub repository as `https://github.com/sourabhgupta385/udacity-cloud-devops-capstone-project` and script path as `infrastructure/Jenkinsfile`
-   Apply and save the pipeline.
-   Click on `Build Now` to trigger the pipeline.
-   `infra-pipeline` does the following steps:
    -   Creates a EKS cluster
    -   Configures kubectl so that we can connect to EKS cluster
    -   Note: This pipeline will take around 15-20 minutes to complete.
-   Add Docker Hub credentials in Jenkins so that we can push docker image to Docker Hub.
-   Create new item in Jenkins of type `Pipeline` of name let's say `udacity-capstone-website-pipeline`
-   In the configuration page of `udacity-capstone-website-pipeline`, provide the GitHub repository as `https://github.com/sourabhgupta385/udacity-cloud-devops-capstone-project` and script path as `Jenkinsfile`
-   Apply and save the pipeline.
-   Click on `Build Now` to trigger the pipeline
-   Once the pipeline passes with stage name `Create Service Pointing to Blue Replication Controller`, go to Load Balancer page in AWS console and look for DNS name
-   DNS name will be something like `a009764aca96411ea97070ad08595ea3-2077112107.us-east-1.elb.amazonaws.com`
-   In the browser, open a new tab and hit link as `http://<DNS_NAME>:8000/`. It will show the capstone project website.
-   Approve the pipeline to proceed to next stage
-   Once the pipeline is complete, service will be pointing to pods that has label as `app=green`
