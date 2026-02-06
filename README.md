# JENKINS CI/CD PIPELINE

This repository contains documentation, examples, and pipeline configurations documenting my journey of learning Jenkins and implementing Continuous Integration and Continuous Deployment workflows.

## 🎯 Learning Objectives

- Understand CI/CD principles and Jenkins architecture
- Set up and configure Jenkins master and agents
- Create and manage pipelines using Jenkinsfile
- Implement automated testing, building, and deployment
- Integrate Jenkins with Docker, Kubernetes, and cloud platforms
- Apply security best practices in Jenkins
- Implement monitoring and notifications for CI/CD pipelines

## 🧠 Prerequisites

- Git fundamentals and version control
- Linux command-line proficiency
- Basic understanding of networking (ports, IPs, HTTP/HTTPS)
- Basic understanding of build tools (Maven, npm, pip, etc.)
- Docker and containerization concepts.

## 🗂️ Table of Contents

- [Introduction to CI/CD: Concepts, benefits, and Jenkins overview]()

## Useful Commands

- `sudo systemctl status jenkins` - Check Jenkins status
- `sudo systemctl start jenkins` - Start Jenkins
- `sudo systemctl stop jenkins` - Stop Jenkins
- `sudo systemctl restart jenkins` - Restart Jenkins
- `usermod -aG docker jenkins` - Add Jenkins user to Docker group

**Logs & Troubleshooting (VERY common)**

- sudo journalctl -u jenkins # View Jenkins service logs
- sudo tail -f /var/log/jenkins/jenkins.log # Live Jenkins logs

**Initial Setup / Access**

- sudo cat /var/lib/jenkins/secrets/initialAdminPassword

**Network & Port Checks**

- ss -tulnp | grep 8080 # Check Jenkins port
- curl http://localhost:8080

**Jenkins CLI**

Allows you to run the Jenkins CLI from the command line. It requires jenkins-cli.jar downloaded from Jenkins.

- java -jar jenkins-cli.jar -s http://localhost:8080/ help: It shouws all the available commands
- java -jar jenkins-cli.jar version: It shows jenkins server version.
- java -jar jenkins-cli.jar list-plugins: Lists all the plugins installed currently.
- java -jar jenkins-cli.jar install-plugin <plugin>: Installs a plugin by name.
- java -jar jenkins-cli.jar restart: Restart the Jenkins server immediately.
- java -jar jenkins-cli.jar build <job-name>: Start a jenkins job by name.

**Docker Integration**

- docker ps
- docker images
- docker logs <container-id>

## 📫 Connect With Me

<div align="center">

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ksubramanyeshwara)
[![X (Twitter)](https://img.shields.io/badge/X-000000?style=for-the-badge&logo=x&logoColor=white)](https://x.com/ksubramanyaa)
[![Peerlist](https://img.shields.io/badge/Peerlist-46923c?style=for-the-badge&logo=peerlist&logoColor=white)](https://peerlist.io/subramaneshwara)
[![Gmail](https://img.shields.io/badge/Gmail-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:ksubramanyeshwara@gmail.com)

</div>

## 💁‍♂️ Support

<div align="center">

Found this repo helpful ? Give it a ⭐️

</div>

<div align="center">

Made with ❤️ by **K Subramanyeshwara**

</div>
