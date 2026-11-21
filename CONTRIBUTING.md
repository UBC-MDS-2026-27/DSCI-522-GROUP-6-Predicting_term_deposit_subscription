# Contributing to term deposite subscription predictor project
We, the contributors and maintainers of pterm deposite subscription predictor project, pledge to respect all people who contribute through reporting issues, posting feature requests, updating documentation, submitting pull requests or patches, and other activities. 

Here is the outline about how to propose a change to our project. 

## Fixing Typos
Small typos or grammatical errors in documentation may be edited directly using the GitHub web interface, so long as the changes are made in the source file.

* YES: you edit the Quarto source file reports/term_deposit_subscription_predictor_report.qmd.
* NO: you edit the rendered reports/term_deposit_subscription_predictor_report.html or .pdf.

## Prerequisites
Before you make a substantial pull request, you should always file an issue and make sure someone from the team agrees that it's a problem. If you've found a bug, create an associated issue and illustrate the bug with a minimal [reprex](https://tidyverse.org/help/#reprex).

## Pull Request Process
* Create a new Git branch for each pull request (PR), starting from an up-to-date main. Do not commit directly to main.
* Give the branch a short name that describes the work, for example fix-readme-typo or add-eda-figure (it has to be meaningful, not a random name).
```bash
    git switch -c <your-branch-name>
```
* Keep each branch small: one independent piece of work per branch.
* Before opening the PR, render the report (uv run quarto render) to check that the analysis still runs from start to finish.
```bash
    uv run quarto render reports/term_deposit_subscription_predictor_report.qmd
```
* Before opening the PR, make sure no extra files are added to push, check the status of all files.
```bash
    git status
```
* Run the following code when you first submit your branch:
```bash
    git push -u origin BRANCH_NAME
```
* Open a PR into main and describe what changed and why. Link the related issue (e.g., "Closes #12").
* For pull request, add all team members as reviewers.
* At least one other team member must review and approve the PR before it is merged. The reviewer, not the author, merges it.
* New code should follow the [PEP8 style guide](https://peps.python.org/pep-0008/).


## AI Policy
You are allowed to use generative AI tools, while the following rules have to be obeyed:
* Contribution totally depends on AI is meaningless, which is not allowed.
* Pull requests and GitHub issues are opened by team members, never by an AI agent or chat bot.
* AI is used as assistant, while not the leader, feed the content of CLAUDE.md to your AI at first
* You are responsible to understand all of the coding or context you make with the help of AI
* Mentioned group members which part do you do with the help of AI