# Jenkins Jobs

- Jobs are automated tasks or operations that Jenkins runs automatically.
- A job is a configured set of instructions that tells Jenkins what to do, when to do it, and how to do it.

## Tasks or configurations can include:

- Pull code from GitHub
- Build the application
- Run tests
- Create Docker image
- Deploy to server

## Types of Jenkins Jobs

1. **Freestyle Job**
2. **Pipeline Job**
3. **Multibranch Pipeline Job**

## Freestyle Job

- GUI-based configuration
- Not recommended for complex tasks

## Pipeline Job

- Script-based configuration
- Recommended for complex tasks

## Boardgame Freestyle Job

### Creating the Job

1. Navigate to Jenkins dashboard and click **New Item**
2. Enter job name, select **Freestyle Project**, and click **OK**
3. Enter a description for the job

### Configuration Options

**Build History Management**

- Configure "Discard old builds" to keep only the last 5 builds

**Parameters**

- **String Parameter**: A parameter that you can pass to the job when you trigger it. This is used to deploy to different environments (dev, test, prod)

**Agent Selection**

- **Restrict where this project can be run**: Choose the agent where you want your job to run

**Source Code Management**

- Copy the GitHub URL from the code section (HTTPS)
- Paste it in the Repository URL field
- No credentials required if the GitHub repository is public

**Triggers**

- Configure triggers to let the job run based on specific conditions
  - **Poll SCM**: `H/5 * * * *` (checks every 5 minutes)
  - **OR** use GitHub webhook for instant builds

**Build Steps**

- **Invoke top-level Maven targets**: Select the Maven version
- **Goals**: Use `compile`, `test`, and `package` separately, or use `clean package` to compile, test, and package in one step

**Post-Build Actions**

- Use for email notifications when the build is complete, etc.

### Running the Job

- Click on the job name and select **Build with Parameters**
- Choose what you want to do with this build (dev, prod, etc.)

### Understanding Key Directories

**Workspace**

- A directory where Jenkins stores all files related to the job
- Files include source code, build artifacts, logs, target folder, etc.

**Target**

- A directory where Maven stores the compiled code and build artifacts

## Java Version Management

If you are using Java, projects built on lower Java versions will generally work with higher versions. If compatibility issues occur:

1. Navigate to **Plugins** and search for **Eclipse**
2. Install **Eclipse Temurin Installer** to help configure multiple Java versions
3. Configure plugins in the **Tools** section:
   - Go to **JDK installations** and add JDK
   - Name it (e.g., `jdk17`)
   - Select **Install automatically**
   - Choose **Install from adoptium.net**
   - Select `jdk-17.0.14+7`

> **Note**: The GitHub repository should contain a Dockerfile and tests
