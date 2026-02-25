# Jenkins controller and agent setup

- Go to EC2, Security group, Create security group

## Security group for Jenkins controller

- Name: controller-sg
- Description: Allow SSH and HTTP traffic
- VPC: default
- Inbound rules:
  - SSH (22) from my IP
  - Custom TCP (8080) from my IP
- Outbound rules: All traffic, destination 0.0.0.0/0
  > Attach it to Jenkins controller instance

## Security group for Jenkins agent

- name: agent-sg
- description: Allow controller to SSH into agent
- VPC: default
- Inbound rules:
  - SSH (22), source Custom, controller-sg
- Outbound rules: All traffic, destination 0.0.0.0/0
  > Attach it to Jenkins agent instance

## Jenkins controller instance

- Name your EC2 instance Jenkins-controller
- Select Ubuntu Server 22.04 LTS (HVM), SSD Volume Type
- Select t2.medium
- Create a new key pair, download the .pem file
- Select the controller-sg security group
- Launch instance
- Connect to the instance using SSH
- Update and Upgrade the instance
- Install Java, and Jenkins
- Start Jenkins, open Jenkins in browser
- Get Initial Admin Password: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`
- Paste the initial admin password you copied above
- Click Install suggested plugins and wait for it to finish
- Create your admin user (username, password, email)
- Click Save and Finish → Start using Jenkins

## Jenkins agent instance

- Name your EC2 instance Jenkins-agent
- Select Ubuntu Server 22.04 LTS (HVM), SSD Volume Type
- Select t2.medium
- Use the same key pair as the controller
- Select the agent-sg security group
- Launch instance
- Connect to the instance using SSH
- Update and Upgrade the instance
- Install Java
- Create Jenkins working directory: `sudo mkdir -p /var/lib/jenkins`

## Add SSH Credential in Jenkins Controller

- Open Jenkins → Manage Jenkins → Credentials
- Click System → Global credentials (unrestricted)
- Click Add Credentials → Select a type of credential → SSH Username with private key
- Scope: Global → ID: ec2-agent-key
- Username: ubuntu(This should be the username of the agent instance)
- Private Key: Enter directly → click Add
- Open your .pem file on your local machine and select all and copy the content
- Paste the content into the Private Key field
- Click Create

## Create Node

- Go to Manage Jenkins → Nodes, Click New Node
- Node name: agent-1
- Select Permanent Agent, Click Create
- Number of executors: 2
- Remote root directory: /var/lib/jenkins. Same directory that we created on the agent instance
- Labels: agent-1
- Usage: Only build jobs with label expressions matching this node
- Launch method: Launch agents via SSH
- Host: <agent-1-private-ip>
- Credentials: ec2-agent-key
- Host Key Verification Strategy: Non verifying Verification Strategy
- Click Save

## Check if the agent is connected

- Go to Manage Jenkins → Nodes
- Click Launch agent
- Watch the logs — you should see:
  ```
  [SSH] Opening SSH connection to <ip>:22
  [SSH] Authentication successful
  Agent successfully connected and online
  ```
