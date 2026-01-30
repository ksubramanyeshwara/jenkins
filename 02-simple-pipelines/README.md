# Jenkins pipeline using Docker agents to run Node.js builds in isolated, reproducible containers.

## Overview

This project demonstrates the Jenkins pipeline using Docker agents to verify Node.js is installed correctly and verifies the Node version.

- Tech stack: Node.js 16 (Alpine), Jenkins Declarative Pipeline.
- Purpose: Basic test to confirm Docker agent works and Node.js environment is correct.

## Prerequisites

- Docker plugin installed on Jenkins
- Docker host accessible from Jenkins agent
- Jenkins user added to docker group

## Jenkinsfile

```groovy
pipeline {
  agent {
    docker { image 'node:16-alpine' }
  }
  stages {
    stage('Test') {
      steps {
        sh 'node --version'
      }
    }
  }
}
```

## Jenkins Pipeline Configuration

### Pipeline Behavior

- Jenkins controller reads the Jenkinsfile
- A Docker container (`node:16-alpine`) is started as the pipeline agent
- Pipeline steps run inside the container
- Container is removed after the pipeline completes

### Stages

**Test Stage**

- Runs inside `node:16-alpine` Docker container
- Executes: `node --version`
- Purpose: Prints Node.js version to console (verifies environment)

## Why Docker Agent?

- Docker agent provides isolated, reproducible Node.js environment.
- No need to install Node.js on Jenkins server.
-

## Outcome

The pipeline prints the Node.js version from inside the Docker container,
confirming successful containerized execution.

# Multi Stage Multi Agent Pipeline

## Overview

This project demonstrates a multi-stage, multi-agent Jenkins pipeline that builds and maven and node.js applications in isolated Docker containers. The pipeline uses Docker agents to ensure consistent build environments and demonstrates parallel execution of stages.

- Tech stack: Maven, Node.js, Jenkins Declarative Pipeline
- Purpose: Showcase multi-stage pipeline with different agents

## Prerequisites

- Docker plugin installed on Jenkins
- Docker host accessible from Jenkins agent
- Jenkins user added to docker group

## Jenkinsfile

```groovy
pipeline {
  agent none # no global agent, each stage defines its own
  stages {
    stage('Back-end') {
      agent {
        docker { image 'maven:3.8.1-adoptopenjdk-11' }
      }
      steps {
        sh 'mvn --version'
      }
    }
    stage('Front-end') {
      agent {
        docker { image 'node:16-alpine' }
      }
      steps {
        sh 'node --version'
      }
    }
  }
}
```

### Pipeline Behavior

- No global agent (agent none)
- The pipeline has two stages.
- Each stage defines its own Docker agent
- Back-end stage uses Maven container
- Front-end stage uses Node.js container

### Stages

**Back-end Stage**

- Uses `maven:3.8.1-adoptopenjdk-11` Docker image
- Executes: `mvn --version`
- Purpose: Verify Maven installation

**Front-end Stage**

- Uses `node:16-alpine` Docker image
- Executes: `node --version`
- Purpose: Verify Node.js installation

## Why Multi-Agent Pipeline?

- Isolated build environments for different technologies
- Parallel execution of independent stages
- Consistent build environments using Docker containers
- No need to install tools on Jenkins server

## Outcome

The pipeline demonstrates:

- Multi-stage pipeline with different agents
- Parallel execution of stages
- Isolated build environments using Docker containers
- Verification of both Maven and Node.js installations
