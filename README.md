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
-   Once the stack creation is complete, access the Jenkins UI using `http://<EC2_PUBLIC_IP>:8080`
-   Login using admin account and complete the initial setup of Jenkins.
-   Install the following plugins in Jenkins:
    -   [CloudBees AWS Credentials](https://plugins.jenkins.io/aws-credentials/)
    -   [Pipeline: AWS Steps](https://plugins.jenkins.io/pipeline-aws/)
    -   [Blue Ocean](https://plugins.jenkins.io/blueocean/)
-   Add AWS credentials in Jenkins.
-   Create new item in Jenkins of type `Pipeline` of name let's say `infra-pipeline`.
-   In the configuration page of `infra-pipeline`, provide the GitHub repository as `https://github.com/sourabhgupta385/udacity-cloud-devops-capstone-project` and script path as `infrastructure/Jenkinsfile`
-   Apply and save the pipeline.
