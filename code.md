stages: 
    - build
    - test
    - push
    - deploy

variables:
    DEPLOY_ENV: "production"
    GITLAB_USER_KEY: "this is my-secret-key"

build_job: 
    stage: build
    script:
        - echo "This $CI_PROJECT_NAME build is done using command <docker build -t tag .>"
    tags:
        - dev

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
    tags:
            - dev

push_job:
    stage: push  
    script: 
        - echo "this"
        - echo "This is pushing to Docker Hub for $DEPLOY_ENV"
    tags:
            - dev

deploy_job:
    stage: deploy  
    script: 
        - "this"
        - echo "Hello, this is deploying  to EC2 instances for  $DOCKERHUB_USER"
        - echo "This log is from $CI_JOB_STAGE" >> logs/app.log
    artifacts:
        paths:
            - logs/
        expire_in: 1 week   
    tags:
            - dev     
 
dev_test_job:
    stage: test 
    script:
        - echo "Tested for  dev using $GITLAB_USER_KEY"
    tags:
         - dev   

prd_test_job:
    stage: test
    script:
        - echo "Tested for  prd $GITLAB_USER_KEY"
    tags:
        - dev
