# Pipeline Job

- A Pipeline Job defines the entire CI/CD process as code.
- You write a Jenkinsfile to define stages such as Build, Test, Deploy, and others.
- The configuration lives inside your repository, making your build and deployment process version-controlled, repeatable, and automated.

## Difference between Freestyle Job and Pipeline Job

| Freestyle Job         | Pipeline Job              |
| --------------------- | ------------------------- |
| Configured via UI     | Written as code           |
| Hard to track changes | Version controlled        |
| Not scalable          | Perfect for complex CI/CD |
| Manual stage flow     | Structured stages         |

## Types of Pipeline in Jenkins

1. **Declarative Pipeline** (Recommended)
2. **Scripted Pipeline**

### Declarative Pipeline

- Easy to read and write
- Structured and predictable, and recommended for most use cases.
- It is written inside the Jenkins pipeline block.
- To make changes, you need to visit the Jenkins pipeline job and update the script. To avoid this, you can use a Jenkinsfile in the repository.

**Example:**

```groovy
pipeline {
    agent {
        label 'agent'
    }

    tools {
        maven 'maven-3.9.6'
        jdk 'jdk-17'
    }

    stages {
        stage('Compile') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Build') {
            steps {
                sh './deploy.sh'
            }
        }
    }
}
```

**Important Notes:**

- No two stages can have the same name
- If you don't have access to the GitHub repository, go to the build number, click on Replay, and you can make changes to the script

### Scripted Pipeline

Scripted Pipeline is more flexible and powerful, and is recommended for complex scenarios.

**Example:**

```groovy
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

- **agent** — Defines where the pipeline runs (any node, a specific node, or a Docker container)
- **stages** — Logical groupings of work (e.g., Build → Test → Deploy)
- **steps** — The actual commands or actions within a stage
- **post** — Actions that run after the pipeline finishes (e.g., send notifications, clean up)

## How Pipeline Job Works (Flow)

1. Developer pushes code to Git
2. GitHub sends webhook to Jenkins
3. Jenkins triggers pipeline (fetches code and reads Jenkinsfile)
   - Checkout code
   - Install dependencies
   - Build artifact
   - Run tests
   - Deploy
4. **Post:** Send success notification

## Create Pipeline Job using Jenkinsfile

1. Go to **Jenkins Dashboard** → **New Item** → Enter an item name → Select **Pipeline** → Click **OK**
2. In the **Pipeline** section, select **Pipeline script from SCM**
3. **SCM:** Git → **Repository URL:** `<your-repo-url>` → **Credentials:** `<your-credentials>` → **Branch Specifier:** `main`
4. **Script Path:** `Jenkinsfile`
5. Click **Save**

### Using Tools from Jenkins Global Tool Configuration

If you want to use tools defined in Jenkins Global Tool Configuration, you need to add the following to your Jenkinsfile:

```groovy
tools {
    maven 'maven-3.9.6'
    jdk 'jdk-17'
}
```
