# Centralized Renovate Bot

## Purpose

This repository runs a centralized [Renovate bot](https://github.com/renovatebot/renovate) to manage dependencies across all of your GitHub repositories. It is configured to automatically discover repositories you have access to and create onboarding pull requests.

## Setup Instructions

To get this centralized Renovate bot working, you need to provide it with a GitHub Personal Access Token (PAT).

### 1. Generate a GitHub Personal Access Token (PAT)

Follow the official GitHub documentation to [create a new Personal Access Token (classic)](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token).

When creating the token, ensure you grant it the **`repo`** scope. This will give it the necessary permissions to read your repositories and create pull requests.

**Important:** Copy the token immediately after it's generated. You won't be able to see it again.

### 2. Add the PAT to GitHub Actions Secrets

Next, you need to add the PAT as a secret to this repository so that the GitHub Actions workflow can use it.

1.  In this repository, go to **Settings > Secrets and variables > Actions**.
2.  Click on **New repository secret**.
3.  For the **Name**, enter `RENOVATE_TOKEN`.
4.  For the **Secret**, paste the Personal Access Token you generated in the previous step.
5.  Click **Add secret**.

## How it Works

This repository is configured to run Renovate in "autodiscover" mode. Here's what that means:

1.  **Scheduled Job**: A GitHub Actions workflow in this repository runs every hour.
2.  **Discovery**: During each run, Renovate uses the `RENOVATE_TOKEN` to find all the repositories that the token has access to.
3.  **Onboarding**: For each new repository it discovers, Renovate will create a pull request titled "Onboard Renovate". This PR adds a basic `renovate.json` configuration file to that repository.
4.  **Activation**: To enable Renovate for a repository, simply merge the "Onboard Renovate" pull request. Renovate will then start creating pull requests for dependency updates in that repository based on the configuration in its `renovate.json` file.

You can monitor the Renovate job's progress in the "Actions" tab of this repository.
