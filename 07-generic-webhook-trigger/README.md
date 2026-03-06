# Generic Webhook Trigger

- In the Jenkins context, a **webhook** is an automated notification mechanism that tells Jenkins an event has occurred.
- Instead of Jenkins checking the repository repeatedly (polling), the repository sends an HTTP request to Jenkins when an event occurs.
- When the event happens, the webhook triggers a Jenkins pipeline build automatically.

## Common Events

- Push to repository
- Pull request created
- Merge to main branch
- Tag creation

## Simple Flow

```
Developer pushes code → GitHub/GitLab detects event
        ↓
Webhook sends HTTP request to Jenkins
        ↓
Jenkins receives the request
        ↓
Pipeline job starts automatically
```

## Why Use Webhooks?

- Jenkins pipeline triggers instantly after a commit
- Eliminates the CPU and network overhead of continuous polling

## Create a Webhook Pipeline Job

1. Go to Jenkins Dashboard
2. Click on **New Item**
3. Enter an item name
4. Select **Pipeline**
5. Click on **OK**

## Configure the Webhook Pipeline Job

1. In the **Triggers** section, select **Generic Webhook Trigger**
2. In the **Post content parameters** section, set the variable name as **ref**, Expression as **$.ref**, then choose **JSONPath**
3. In the **Token** section, enter a token
4. In the **Token Credential** section, select **Add** and select **Jenkins** or **global**
5. In the popup, select **secret text**. You can choose the scope as either global or System
6. In the **secret text** field, write your secret text, provide an ID, then click on **Create**
7. Select the created secret text in the Token Credential field
8. In the **optional filter**, write the branch name where you want to trigger the pipeline as `refs/heads/branchname` and text as **$ref**
9. Copy **http://JENKINS_URL/generic-webhook-trigger/invoke?token=TOKEN_HERE**. This URL is used for invoking the webhook
10. Go to the GitHub repository where you want to set up the webhook, click on **Settings**, and on the left you will see **Webhooks**. Click on that
11. Click on **Add webhook**, add the Payload URL (`http://JENKINS_URL/generic-webhook-trigger/invoke?token=TOKEN_HERE`), and set Content type to `application/json`
12. Disable SSL verification for the time being
13. For "Which events would you like to trigger this webhook?", select **Just the push event** and click on **Add webhook**

## Plugin Used

**Generic Webhook Trigger Plugin**: This plugin helps to assign specific branches for webhook triggering.
