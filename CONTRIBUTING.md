# Contributing to the Term Deposit Subscription Predictor Project

We, the contributors and maintainers of the Term Deposit Subscription Predictor project, welcome contributions from everyone. We pledge to treat people respectfully when they report issues, suggest features, improve documentation, submit pull requests, or participate in other project activities.

This guide explains how to propose and submit changes to the project.

## Fixing Typos

Small spelling or grammatical corrections are welcome. All changes, including typo fixes made through the GitHub web interface, must be proposed on a separate branch and submitted through a pull request (PR). Do not commit directly to `main`.

Edit source files rather than generated output. For example:

- **YES:** Edit the Quarto source file `reports/term_deposit_subscription_predictor_report.qmd`.
- **NO:** Edit the rendered `reports/term_deposit_subscription_predictor_report.html` or `.pdf` files directly.

## Prerequisites

Before making a substantial change, open a GitHub issue describing the proposed work and wait for a maintainer to confirm that it is appropriate. For bug reports, include steps to reproduce the problem and, where possible, a minimal reproducible example ([reprex](https://tidyverse.org/help/#reprex)).

## Pull Request Process

1. Start from an up-to-date `main` branch:

   ```bash
   git switch main
   git pull origin main
   ```

2. Create a new branch with a short, descriptive name for each PR, such as `fix-readme-typo` or `add-eda-figure`:

   ```bash
   git switch -c <your-branch-name>
   ```

3. Keep each PR focused on one independent change. Do not commit directly to `main`.

4. If your changes affect the report or its analysis, render the Quarto source to confirm it runs successfully:

   ```bash
   uv run quarto render reports/term_deposit_subscription_predictor_report.qmd
   ```

5. Review your changes and check for unintended files before committing or pushing:

   ```bash
   git status
   git diff
   ```

6. Commit your intended changes and push the branch. For the first push, set its upstream branch:

   ```bash
   git add <files-you-changed>
   git commit -m "Describe your change"
   git push -u origin <your-branch-name>
   ```

7. Open a PR targeting `main`. Explain what changed and why, and link any related issue (for example, `Closes #12`). Request reviews from all team members.

8. At least one team member other than the author must review and approve the PR before it is merged. The reviewer, not the author, merges the PR.

New Python code should follow the [PEP 8 style guide](https://peps.python.org/pep-0008/).

## AI Policy
Contributors may use generative AI tools to assist with tasks such as brainstorming, explaining code, debugging, improving writing, and suggesting tests, subject to the following requirements:

- You must understand, review, and verify all AI-assisted code, text, and other contributions before submitting them. Do not submit AI-generated work that you cannot explain or validate.
- In the PR description, identify the AI tools used, describe which parts of the contribution were AI-assisted, and explain how you checked the results. If no AI was used, no AI disclosure is required.
- Contributors must make the final decisions about their changes. GitHub issues and PRs must be opened and managed by a human contributor, not autonomously by an AI agent or chatbot.
- Before using an AI tool for project work, read CLAUDE.md and provide its relevant guidance to the tool when appropriate.
- Do not share secrets, credentials, or private information with AI tools. Check AI-assisted content for correctness, appropriate attribution, and compliance with project requirements.
- Pull requests and GitHub issues are opened by human contributors, never by an AI agent or chat bot.

## Attribution

This contributing guide adapts elements of the [dplyr contributing guide](https://github.com/tidyverse/dplyr/blob/main/.github/CONTRIBUTING.md) and the [tidyverse guide to reproducible examples](https://tidyverse.org/help/#reprex). It has been modified to reflect this project's workflow and AI policy.


