# Reusable Workflows

## Overview
Rather than copying and pasting from one workflow to another, you can make workflows reusable. You and anyone with access to the reusable workflow can then call the reusable workflow from another workflow.

Reusing workflows avoids duplication. This makes workflows easier to maintain and allows you to create new workflows more quickly by building on the work of others, just as you do with actions. Workflow reuse also promotes best practice by helping you to use workflows that are well designed, have already been tested, and have been proven to be effective. Your organization can build up a library of reusable workflows that can be centrally maintained.

The diagram below shows an in-progress workflow run that uses a reusable workflow.

After each of three build jobs on the left of the diagram completes successfully, a dependent job called "Deploy" is run.
The "Deploy" job calls a reusable workflow that contains three jobs: "Staging", "Review", and "Production."
The "Production" deployment job only runs after the "Staging" job has completed successfully.
When a job targets an environment, the workflow run displays a progress bar that shows the number of steps in the job. In the diagram below, the "Production" job contains 8 steps, with step 6 currently being processed.
Using a reusable workflow to run deployment jobs allows you to run those jobs for each build without duplicating code in workflows.

![Deployment](https://docs.github.com/assets/cb-34427/images/help/images/reusable-workflows-ci-cd.png)

## How to make any GitHub Actions workflow reusable
Step 1: Add a workflow_call trigger
A reusable workflow is just like any GitHub Actions workflow with one key difference: it includes a workflow_call trigger.

That means all you need to do is add in the following syntax to any action’s YAML workflow file:
```bash
on:
  workflow_call:
```
You can then reference this workflow in another workflow by adding in this syntax:

```bash
Uses:
  USER_OR_ORG_NAME/REPO_NAME/.github/workflows/REUSABLE_WORKFLOW_FILE.yml@TAG_OR_BRANCH
```

You can also pass data such as job information or passwords to a reusable workflow by using inputs and secret triggers. Inputs are used to pass non-sensitive information while secrets are used to pass along sensitive information such as passwords and credentials. You can learn more about that in our docs.

Step 2: Make your actions accessible across your organization
After you add a workflow_call trigger, you need to make sure that your repositories in your organization have access to it. To do this, go to your repository settings, select Actions, and enable access to repositories in your organization.

![Enabling access for GitHub Actions at the organization level](https://github.blog/wp-content/uploads/2022/02/enabling-access-github-actions-org-level.png?w=658)
Enabling access for GitHub Actions at the organization level

## TL;DR

The more things you can do to follow the DRY principle, the better. Reusable workflows make it simple to spin up new repositories and projects and immediately start using automation and CI/CD workflows with GitHub Actions that you know will work. That saves you time, and it lets you focus more on what’s important: writing great code.

## Contributing

Pull requests are welcome. For major changes, please open an issue first
to discuss what you would like to change.