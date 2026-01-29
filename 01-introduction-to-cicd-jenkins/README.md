# Continuos Integration / Continuos Delivery/Deployment

## Continuos Integration

- Developers frequently push code to a shared repository.
- Each push triggers an automated build and test process to detect errors early.
- The goal of CI is to ensure that the codebase is always in a working state, reducing integration issues.

## Continuos Delivery

- Every code change that passes tests is automatically prepared to deploy (manual approval).

## Continuos Deployment

- Continuous Deployment: Every code change that passes tests is automatically deployed to production.

> CI/CD automates code building, testing, and releasing.

## Why CI/CD?

- Speed up software delivery: More frequent releases
- Improve software quality: Catch bugs early.
- Reduced errors: Smaller changes are easier to debug, No manual errors.
- Team collaboration: Through quick feedback.

## Before CI/CD (Traditional)

Code → Manual Testing → Wait → Manual Build → Wait → Manual Deploy → Failures = Rollback

- Slow (weeks/months per release)
- Error-prone (manual steps)
- Hard to debug (big changes)
- Team friction (dev vs ops)

## After CI/CD (Modern DevOps)

Code → Auto Build → Auto Test → Auto Deploy → Monitor → Feedback

- Fast (minutes/hours per release)
- Reliable (automated, repeatable)
- Easy to debug (small changes)
- Team synergy (dev + ops = DevOps)

> The goal of DevOps is automation, speed, and reliability. CI/CD is the engine that makes it happen.

# Jenkins

- Jenkins is an open-source automation server used for CI/CD pipelines.
- It automates software development lifecycle by building, testing, and deploying software.

## Why is Jenkins used?

- Automates the repetitive tasks: Building, Testing, Reporting and Deploying
- Intigrate with most of the tools: Git, Docker, AWS, Kubernetes, etc
- Extensibility: It has vast ecosystem of plugins that supports various tools and technologies.

## Jenkins Architecture

1. Controller(Master)
   - Manages configuration, UI, job scheduling.
   - Orchestrates(Arrange) builds and stores job history/artifacts.
   - Handles security and plugins.
2. Agent(Slave)
   - Executes the build, test, and deployment tasks.
   - Can be physical or virtual machines.
   - Connect to the Controller via SSH, JNLP, or WebSocket.
3. Execution Flow
   - Code change triggers webhook(e.g., GitHub, GitLab).
   - Controller queues and assigns job to an Agent.
   - Agent runs pipeline stages (build → test → deploy).
   - Results reported back to Controller and stored in database
   - Notifications are sent (e.g., Slack, Email)

> Plugins: Core of extensibility.
> Pipelines: Declarative (simple, recommended)

## Installation

- update your linux repositories
- Install Java 17 on your machine `sudo apt install openjdk-17-jdk`
- Install the LTS release
  ```bash
      sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
      https://pkg.jenkins.io/debian-stable/jenkins.io-2026.key
      echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
      https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
      /etc/apt/sources.list.d/jenkins.list > /dev/null
      sudo apt update
      sudo apt install jenkins
  ```

1. Install Docker on same machine