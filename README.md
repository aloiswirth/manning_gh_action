# manning_gh_action

This repository contains GitHub Actions workflows used to automate repository tasks.

## Auto-label new issues

Workflow file: `.github/workflows/label_new_issues.yml`

Purpose: Automatically add the label `new_label` to every newly opened GitHub Issue.

Key details:
- Trigger: `issues` event, `types: [opened]`
- Permissions: `issues: write` (grants the workflow permission to manage issue labels)
- Behavior:
  - Ensures the label `new_label` exists (creates it if missing with color `#0E8A16`).
  - Adds the label to the newly opened issue.

This workflow works alongside the existing triage workflow (`.github/workflows/issue_triage.yml`), which may add additional labels like `bug`, `feature`, or `needs-triage` based on the issue body. Multiple labels can coexist on the same issue.

### How to test
1. Push the workflow to the default branch (e.g., `main`) or ensure it already exists there.
2. Open a new issue in the repository.
3. Confirm that the label `new_label` is added automatically.
4. If needed, open the Actions tab in GitHub and review the logs for the workflow named “Add label to new issues”.

### Customization
- Change the label name:
  - Edit `labelName` in `.github/workflows/label_new_issues.yml` to your desired label (e.g., `"triage-needed"`).
- Change the label color:
  - Update the `color` hex in the `createLabel` call (e.g., `FF5733`).
- Extend triggers:
  - Add more issue activity types if desired (e.g., `edited`) by modifying the `on.issues.types` array.

### Troubleshooting
- If the label is not added:
  - Check the Actions run logs for errors.
  - Ensure repository settings permit GitHub Actions and Issues are enabled.
  - Ensure the workflow file is present on the default branch.
  - Verify `permissions.issues: write` is present in the job or at the workflow level.

## Existing Workflows

- `.github/workflows/issue_triage.yml`: Adds labels like `bug`, `feature`, or `needs-triage` based on keywords in the issue body.
- `.github/workflows/MyFirstWorkflow.yml`: Example workflow that runs on push to `main` and lists files.
