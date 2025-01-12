# Gitlab


## Continuous Integration (CI) Pipeline

This project uses a CI pipeline to automate the processes of building, testing, pushing, and deploying Docker images. Below is the structure of the CI pipeline configuration:

### Stages

The pipeline consists of the following stages:

1. **Build**: Creates the Docker image using a specified tag.
2. **Test**: Verifies the Docker build to ensure everything is functioning correctly.
3. **Push**: Pushes the Docker image to the Docker Hub.
4. **Deploy**: Deploys the Docker image to the specified environment.

### Pipeline Configuration

```yaml
stages: 
    - build
    - test
    - push
    - deploy

build_job: 
    stage: build
    script:
        - echo "This build is done using command <docker build -t tag .>"

test_job:
    stage: test
    script:
        - echo "This is testing of our Docker build"

push_job:
    stage: push  
    script: 
        - echo "This is pushing to Docker Hub"

deploy_job:
    stage: deploy  
    script: 
        - echo "Hello, this is deploying the Docker image"
