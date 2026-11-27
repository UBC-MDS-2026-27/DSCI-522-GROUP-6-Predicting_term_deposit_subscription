# Predicting Term Deposit Subscription

## Authors

- Abdulrahman Aleid
- Ahmed Muhaimin Choudhury
- David Wu

## Summary

In this project, we asked whether we can predict if a bank client will subscribe to a term deposit, using information the bank has before calling the client. We used the Bank Marketing data set from the UCI Machine Learning Repository, which contains data from phone marketing campaigns of a Portuguese bank.

We compared a Dummy Classifier, Logistic Regression and K-Nearest Neighbours, and chose Logistic Regression as our final model. On the unseen test set, it had an accuracy of 0.889, a precision of 0.584 and a recall of 0.170: when it predicts that a client will subscribe, it is correct about 58.4% of the time (compared with an overall subscription rate of about 11.7%), but it finds only about 17% of the clients who actually subscribe, so further work is needed to improve its recall.

## Report
The final report can be found [here](https://ubc-mds-2026-27.github.io/DSCI-522-GROUP-6-Predicting_term_deposit_subscription/), or as a [PDF](https://github.com/ubc-mds-2026-27/DSCI-522-GROUP-6-Predicting_term_deposit_subscription/blob/main/reports/term_deposit_subscription_predictor_report.pdf).

## How to run the analysis
To make our results easy to reproduce, all of the software for this project is packaged in a Docker image called [muhighmin/dsci-522-group-6-predicting_term_deposit_subscription](https://hub.docker.com/r/muhighmin/dsci-522-group-6-predicting_term_deposit_subscription). This means the only tools you need on your own computer are Git and Docker Desktop.

### 1. Install the required software
Download and install [Git](https://git-scm.com/) and [Docker Desktop](https://docs.docker.com/get-docker/) for your operating system. If you are using Windows, make sure to use Git Bash. Docker Desktop must be running before you run the commands in steps 4 and 5, or they will fail with a connection error.

### 2. Get a copy of the project
Open a terminal and run:

```bash
git clone https://github.com/UBC-MDS-2026-27/DSCI-522-GROUP-6-Predicting_term_deposit_subscription.git

cd DSCI-522-GROUP-6-Predicting_term_deposit_subscription
```

Every command after this point should be run inside this directory.

### 3. Create an ssh key (first time only)
When the container starts, it reads your public ssh key so that tools like Positron can log in to it over ssh without a password.

To see if you already have a key, run `ls ~/.ssh/id_ed25519.pub`.
If you get a "No such file" message, create one with the command below and accept the defaults by pressing Enter at each question:

```bash
ssh-keygen -t ed25519
```

If this key is missing when the container starts, Docker makes an empty folder at `~/.ssh/id_ed25519.pub` in its place. To fix this, delete that folder, run `ssh-keygen -t ed25519`, and start the container again.

### 4. Pull the Docker image
The command below downloads our project's image from Docker Hub. It may take a few minutes the first time.

```bash
docker compose pull
```

### 5. Reproduce the analysis
To run the full analysis and build the report inside the container, use:

```bash
docker compose run --rm analysis-env uv run quarto render reports/term_deposit_subscription_predictor_report.qmd
```

This command repeats every step of the analysis. The data is downloaded fresh from the UCI Machine Learning Repository, so make sure you are connected to the internet. Running it replaces the files in `data/raw` and `data/processed` and the report files `reports/term_deposit_subscription_predictor_report.html` and `reports/term_deposit_subscription_predictor_report.pdf`. The `--rm` option deletes the container as soon as the render is finished, so you do not have to shut it down yourself.

## Contributing
To set up a development environment, add a new package or update the published report, follow the steps in [CONTRIBUTING.md](CONTRIBUTING.md).

## Dependencies

- [Docker](https://docs.docker.com/get-docker/)

Our image is built from the `Dockerfile` in this repository and includes Quarto, uv and Python. The Python packages we use are listed in `pyproject.toml`, and their exact versions are pinned in `uv.lock`.

## Licenses

The analysis report is licensed under the [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/). The software code is licensed under the MIT License. See [LICENSE.md](LICENSE.md) for details.

## AI use

Our team used generative AI (Claude) as a tutor and reviewer during this project. We used it to explain Git, uv and Quarto workflows, to review our writing and code for mistakes, and to suggest fixes, which we then checked, tested and edited ourselves. All pull requests and issues were opened, reviewed and merged by team members, not by an AI tool.

We gave the AI tool the instructions in [CLAUDE.md](CLAUDE.md), which asks it to act as a tutor that guides us with hints and explanations instead of doing the work for us.

Example prompts we used:

- "Check our CODE_OF_CONDUCT.md for spelling and grammar mistakes."
- "Are uv add vl-convert-python and quarto install tinytex both part of the environment setup?"
- "Why did our EDA disappear after the PR was merged?"