## CI/CD Pipeline Configuration

This project utilizes a CI/CD pipeline to automate the building, testing, pushing, and deployment of Docker images. Below is a detailed configuration used in the pipeline:

### Pipeline Stages

The pipeline is divided into the following stages:
- **Build**: Building the Docker image.
- **Test**: Testing the Docker image.
- **Push**: Pushing the Docker image to Docker Hub.
- **Deploy**: Deploying the Docker image to the production environment.

### Environment Variables

The pipeline uses the following environment variables:
- `DEPLOY_ENV`: Defines the deployment environment (`production`).
- `GITLAB_USER_KEY`: A secret key used for authentication.

### Pipeline Configuration

```yaml
stages: 
    - build
    - test
    - push
    - deploy

variables:
    DEPLOY_ENV: "production"
    GITLAB_USER_KEY: "this is my secret key"

build_job: 
    stage: build
    script:
        - echo "This $CI_PROJECT_NAME build is done using command <docker build -t tag .>"

test_job:
    stage: test
    script:
        - echo "This is testing of our Docker build by $CI_COMMIT_AUTHOR"
        - mkdir -p logs
        - echo "These are my test results" > logs/app.log
    artifacts:
        paths: 
            - logs/   
        expire_in: 1 week

push_job:
    stage: push  
    script: 
        - echo "This is pushing to Docker Hub"

deploy_job:
    stage: deploy  
    script: 
        - echo "Hello, this is deploying the Docker image for $DOCKERHUB_USER"
        - echo "This log is from $CI_JOB_STAGE" >> logs/app.log
    artifacts:
        paths:
            - logs/
        expire_in: 1 week        

dev_test_job:
    stage: test 
    script:
        - echo "Tested for production environment $GITLAB_USER_KEY"

prd_test_job:
    stage: test
    script:
        - echo "Tested for production"


This `README.md` documentation describes the purpose and functionality of each part of your CI/CD pipeline, making it easier for others to understand and use.

