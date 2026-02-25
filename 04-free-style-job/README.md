# Jenkins Jobs

- Jobs are autonated tasks or operations that jenkins runs automatically
- It is a configured set of instruction that tells jenkins what to do, when to do, and how to do it.
- Task or Configuration can look like:
  - Pull code from GitHub
  - Build the application
  - Run tests
  - Create Docker image
  - Deploy to server

## Types of jenkins jobs

1. Freestyle Job
2. Pipeline Job
3. Multibranch Pipeline Job

## Freestyle Job

- GUI-based configuration
- Not recommended for complex task.

## Pipeline Job

## Boradgame-maven Job

- Jenkins dashboard --> Click on New item
- Enter Job name --> select Freestyle Project --> OK
- Enter Description
- Discard old build and keep only last 5 builds
- Restrict where this project can be run --> Choose the agent: Here you can choose where you want your job to run
- Source Code Management --> copy github url from code section and copy HTTPS --> paste it in Repository URL
- No Credentials as github repo is open
- Triggers --> It let's job to run based on condition
  - Poll SCM: H/5 \* \* \* \* (check every 5 minutes)
  - OR GitHub webhook for instant builds
- Build Steps --> Invoke top-level Maven targets --> select Maven Version
- Goals --> compile, repeat it for test and package or use clean package it will compile, test and package
- Post-build action --> use it for email notification when build is done, etc
- Click on jobname and click on Build with parameters --> chose the what you want to do with this build.(dev or prod etc)
- Workspace --> It is a directory where jenkins stores all the files related to the job. Files include source code, build artifacts, logs, target, etc
- Target --> It is a directory where maven stores the compiled code and build artifacts.

## Java Version

- If you are using java then the project built on lower version java will work with higher version. If it didn't then
- Go to pluggins --> search for eclipse --> install Eclipse Temurin Installer It help you to configure multiple Java version
- You configure plugins in tool section
- JDK installations, add JDK, jdk17 --> Install automatically --> Install from adoptium.net --> select jdk-17.0.14+7

> GitHub repo should contain, Dockerfile and tests
