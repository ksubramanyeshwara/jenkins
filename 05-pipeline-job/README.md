# Pipeline Job

- It defines entire CI/CD process as code.
- You will write Jenkinsfile for Build, Test, Deploy, and other stages.
- The configuration lives inside your repository
- It makes your build and deployment process version-controlled, repeatable, and automated.

## Difference between Pipeline and Freestyle Job

| Freestyle Job         | Pipeline Job              |
| --------------------- | ------------------------- |
| Configured via UI     | Written as code           |
| Hard to track changes | Version controlled        |
| Not scalable          | Perfect for complex CI/CD |
| Manual stage flow     | Structured stages         |

## Types of Pipeline in Jenkins

1. Declarative Pipeline (Recommended)
2. Scripted Pipeline

### Declarative Pipeline

- easy to read and write
- structured and predictable
- recommended for most use cases

```
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                sh './deploy.sh'
            }
        }
    }
}
```

### Scripted Pipeline

- more flexible and powerful
- recommended for complex scenarios

```
node {
    stage('Build') {
        sh 'mvn clean package'
    }
    stage('Test') {
        sh 'mvn test'
    }
    stage('Deploy') {
        sh './deploy.sh'
    }
}
```

## Key Concepts

- agent — defines where the pipeline runs (any node, a specific node, or a Docker container).
- stages — logical groupings of work (e.g., Build → Test → Deploy).
- steps — the actual commands or actions within a stage.
- post — actions that run after the pipeline finishes (e.g., send notifications, clean up).

## How Pipeline Job Works (Flow)

- Developer pushes code to Git
- GitHub sends webhook to Jenkins
- Jenkins triggers pipeline (fetches code + reads Jenkinsfile)
  - Checkout code
  - Install dependencies
  - Build artifact
  - Run tests
  - Deploy
- Post: Send success notification



## Create Pipeline Job

- Go to Jenkins Dashboard → New Item → Enter an item name → Select Pipeline → Click OK
- In the Pipeline section, select Pipeline script from SCM
- SCM: Git → Repository URL: <your-repo-url> → Credentials: <your-credentials> → Branch Specifier: main
- Script Path: Jenkinsfile
- Click Save

If you want to use tools defined in Jenkins Global Tool Configuration, you need to add the following to your Jenkinsfile:

```
tools {
    maven 'maven-3.9.6'
    jdk 'jdk-17'
}
```
