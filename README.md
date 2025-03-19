# Org-level TruffleHog Scan GitHub Action

## Overview
This GitHub Action scans repositories under the `pleo-io` organization for exposed secrets using [TruffleHog](https://github.com/trufflesecurity/trufflehog). It runs on a scheduled basis and can also be manually triggered.

## Features
- Automatically retrieves repositories under `pleo-io`.
- Runs a TruffleHog scan on each repository.
- Creates a GitHub issue if secrets are detected.
- Supports manual triggering and scheduled runs (weekly).

## Workflow Details

### Trigger Conditions
The workflow can be triggered in two ways:
- **Manually**: Using the `workflow_dispatch` event.
- **Scheduled**: Runs every Sunday at midnight (`0 0 * * 0`).

### Jobs
#### 1. Get Repositories
- Uses `raven-actions/get-repos@v1` to fetch repositories under `pleo-io`.
- Stores the repository list as an output.

#### 2. Scan Repositories
- Runs if repositories are retrieved successfully.
- Checks out each repository.
- Runs TruffleHog in a Docker container.
- If secrets are detected, creates a GitHub issue with the findings.

## Requirements
- The repository must have appropriate permissions to allow issue creation.
- Docker must be available in the runner environment.

