# GitLab CI/CD Configuration Examples

This repository includes two examples of GitLab CI/CD configuration files (``.gitlab-ci.yml``) for different scenarios. Below is an overview of each configuration:


## Example 1: Build, Test, and Deploy Pipeline
```
# .gitlab-ci.yml
# Define stages of the pipeline
stages:
  - build
  - test
  - deploy

# Job to build the project
build_job:
  stage: build
  script:
    - echo "Building the project..."

# Job to run tests
test_job:
  stage: test
  script:
    - echo "Running tests..."

# Job to deploy to production
deploy_production:
  stage: deploy
  script:
    - echo "Deploying to production..."
  environment:
    name: production
    url: https://example.com
  only:
    - master  # Deploy only on changes to the master branch
```
 
### Explanation:
- **Stages Definition**: Defines three stages: `build`, `test`, and `deploy`.
- **Build Job (`build_job`)**: Executes a script to build the project.
- **Test Job (`test_job`)**: Executes a script to run tests.
- **Deploy Job (`deploy_production`)**: Deploys to the `production` environment with a specified URL (`https://example.com`). Runs only when changes are made to the `master` branch.

## Example 2: Dockerized Build and Test Pipeline

```
# .gitlab-ci2.yml
# Define stages of the pipeline
stages:
  - build
  - test

# Define variables (optional)
variables:
  DOCKER_DRIVER: overlay2

# Job to build the Docker image
build_job:
  stage: build
  image: docker:stable  # Use Docker in a Docker image
  services:
    - docker:dind  # Enable Docker-in-Docker
  script:
    - docker build -t my-app .  # Build Docker image named my-app

# Job to run tests with Node.js
test_job:
  stage: test
  image: node:14  # Use Node.js 14 image
  script:
    - npm install  # Install dependencies
    - npm test  # Run tests
``` 


### Explanation:
- **Stages Definition**: Defines two stages: `build` and `test`.
- **Variables Definition**: Sets a Docker driver variable (`DOCKER_DRIVER`) to `overlay2`.
- **Build Job (`build_job`)**: Uses the `docker:stable` image to build a Docker image named `my-app`.
- **Test Job (`test_job`)**: Uses the `node:14` image to install dependencies and run tests with npm.
