# Multi-Branch Pipeline Job

Instead of manually creating a Jenkins job for each branch, Jenkins scans your repository and automatically creates a pipeline job for every branch that contains a **Jenkinsfile**.

```
my-repo/
├── main          → Jenkins job: my-repo/main
├── develop       → Jenkins job: my-repo/develop
├── feature/login → Jenkins job: my-repo/feature-login
└── hotfix/bug-42 → Jenkins job: my-repo/hotfix-bug-42
```

## How It Works

- Jenkins connects to the SCM and scans all branches and pull requests
- Any branch containing a **Jenkinsfile** gets its own pipeline job automatically
- Each branch carries its own **Jenkinsfile** at the repository root
- Different branches can have different pipeline logic

## Create a Multi-Branch Pipeline Job

1. Go to Jenkins Dashboard
2. Click on **New Item**
3. Enter an item name
4. Select **Multi-Branch Pipeline**
5. Click on **OK**

## Configure the Multi-Branch Pipeline Job

1. In the **Branch Sources** section, click on **Add source** and select **Git**
2. Enter the repository URL
3. Enter the credentials if required (select **none** if the repository is public)
4. In the **Behaviours** section, click on **Add** and select **Discover branches**
5. In **Property strategy**, select **All branches get the same properties**
6. In the **Build Configuration** section, select **by Jenkinsfile**
7. In the **Script Path** section, enter the path to the Jenkinsfile
8. Click on **Save**

## Run the Multi-Branch Pipeline Job

1. Go to Jenkins Dashboard
2. Click on the Multi-Branch Pipeline Job
3. Click on **Scan Repository Now**
4. Click on the branch or pull request to run the pipeline
