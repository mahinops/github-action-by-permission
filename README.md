# RBAC in Github Action

## Why? 
RBAC (Role-Based Access Control) in GitHub Actions provides a mechanism to control who can trigger specific workflows. By using a `permissions.yml` file, you can define the GitHub usernames that are authorized to manually trigger particular pipelines. This setup ensures that only users with explicit permission can execute these workflows, offering enhanced security and strict access control within your CI/CD processes. This approach is ideal for organizations that require granular control over workflow initiation, limiting access to those who are authorized to perform critical actions.

## Status
Development of this action is still ongoing, with plans to introduce more features in the future, offering even greater flexibility and control over workflow permissions.


## Usage

### Step: 1
The `github-action-by-permission` action is designed to enforce Role-Based Access Control (RBAC) for manually triggered (`workflow_dispatch`) GitHub workflows. Here's a simple example of how to use this action to control who can trigger a specific workflow:

```yml
name: Test Action Trigger Permissions

on:
  workflow_dispatch:

jobs:
  example-job:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Check Permissions
        uses: mokhlesurr031/github-action-by-permission@v1.0
        with:
          permissions-file: 'user-permissions.yml' //specify your yml file with correct path here

      - name: Echo Something
        run: echo "Hello World!"
```
### Step: 2
Create a yml file mentioning the specific users with their username for the pipeline permission. The file format should be as followed_

```yml
allowed_users:
- username1
- username2
- username3
```
`Note`: *In general, this `permissions.yaml` file should be kept in the root directory of the project*.

### Explanation
**Checkout Code**: The first step checks out the repository code using the standard `actions/checkout@v3` action.

**Check Permissions**: The `github-action-by-permission` action is then used to verify if the user who initiated the workflow has permission to do so. It references a `yml` file (*in this case, named user-permissions.yml*) where allowed users are defined.

**Echo Something**: If the permission check passes, the workflow proceeds to execute subsequent steps, such as echoing "Hello World!" in this example. You can specify your workflows as needed.

### Key Points
**permissions-file**: This input points to the YAML file that contains the list of users authorized to trigger the workflow. Only those listed in this file will be able to execute the pipeline. 

`Note Again`: *In general, this `permissions.yaml` file should be kept in the root directory of the project*.


**Security and Control**: By integrating this action into your workflows, you can ensure that only authorized individuals have the ability to initiate critical processes, adding a layer of security and control to your CI/CD pipelines.


This example demonstrates how to set up and use the `github-action-by-permission` action to manage access to your GitHub Actions workflows.


## Github Repository
And this repo contains the test of this action => [Test Repo for Github Action Permission](https://github.com/mokhlesurr031/test-github-action-by-permission)
