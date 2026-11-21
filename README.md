# Predicting Term Deposit Subscription

## Authors

- Abdulrahman Aleid
- Ahmed Muhaimin Choudhury
- David Wu

## Summary

In this project, we asked whether we can predict if a bank client will subscribe to a term deposit, using information the bank has before calling the client. We used the Bank Marketing data set from the UCI Machine Learning Repository, which contains data from phone marketing campaigns of a Portuguese bank.

We compared a Dummy Classifier, Logistic Regression and K-Nearest Neighbours, and chose Logistic Regression as our final model. On the unseen test set, it had an accuracy of 0.889, a precision of 0.584 and a recall of 0.170: when it predicts that a client will subscribe, it is correct about 58.4% of the time (compared with an overall subscription rate of about 11.7%), but it finds only about 17% of the clients who actually subscribe, so further work is needed to improve its recall.

## How to run the analysis

### 1. Install the required software

- [Git](https://git-scm.com/)
- [uv](https://docs.astral.sh/uv/getting-started/installation/)
- [Quarto](https://quarto.org/docs/get-started/)

You also need an internet connection, because the analysis downloads the data from the UCI Machine Learning Repository.

### 2. Clone the repository

```bash
git clone https://github.com/UBC-MDS-2026-27/DSCI-522-GROUP-6-Predicting_term_deposit_subscription.git

cd DSCI-522-GROUP-6-Predicting_term_deposit_subscription
```

### 3. Set up the environment

```bash
uv sync
```

This creates a virtual environment with the exact package versions listed in `uv.lock`.

### 4. Install TinyTeX (needed for the PDF version of the report)

```bash
quarto install tinytex
```

Skip this step if you already have a LaTeX installation.

### 5. Render the report

```bash
uv run quarto render reports/term_deposit_subscription_predictor_report.qmd
```

This downloads the data, runs the analysis, and creates the report in `reports/` as both HTML and PDF.

## Dependencies

- [uv](https://docs.astral.sh/uv/) (manages the Python environment)
- [Quarto](https://quarto.org/) (renders the report)
- Python packages and their exact versions are listed in [`pyproject.toml`](pyproject.toml) and locked in [`uv.lock`](uv.lock)

## Licenses

The analysis report is licensed under the [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/). The software code is licensed under the MIT License. See [LICENSE.md](LICENSE.md) for details.

## AI use

Our team used generative AI (Claude) as a tutor and reviewer during this project. We used it to explain Git, uv and Quarto workflows, to review our writing and code for mistakes, and to suggest fixes, which we then checked, tested and edited ourselves. All pull requests and issues were opened, reviewed and merged by team members, not by an AI tool.

We gave the AI tool the instructions in [CLAUDE.md](CLAUDE.md), which asks it to act as a tutor that guides us with hints and explanations instead of doing the work for us.

Example prompts we used:

- "Check our CODE_OF_CONDUCT.md for spelling and grammar mistakes."
- "Are uv add vl-convert-python and quarto install tinytex both part of the environment setup?"
- "Why did our EDA disappear after the PR was merged?"

## Report

The final report can be found [here](https://ubc-mds-2026-27.github.io/DSCI-522-GROUP-6-Predicting_term_deposit_subscription/reports/term_deposit_subscription_predictor_report.html) (HTML), or as a [PDF](https://github.com/UBC-MDS-2026-27/DSCI-522-GROUP-6-Predicting_term_deposit_subscription/blob/main/reports/term_deposit_subscription_predictor_report.pdf).
