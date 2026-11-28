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

## Setting up the project

We develop in the same Docker container that users run the analysis in, so everyone uses the same software and package versions. First follow the setup steps in the [README](README.md) to install Docker, clone the repository, create an ssh key, and download the image. Run all the commands below from the root of this repository.


## Working in the Container

We edit and run the code inside the container by connecting Positron to it over ssh. Your project folder is shared with the container at `/workspace`, so a file you change there changes on your computer too.

### Once, before your first connection

Install Positron on your computer. Make sure you have followed the setup steps in the [README](README.md): you have an ssh key at `~/.ssh/id_ed25519.pub` and you have run `docker compose pull`.

Check that Git knows who you are on your computer:

```bash
git config --global user.name
git config --global user.email
```

These should print your name and email of your GitHub account. If these prints nothing, set your name and email:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

`docker-compose.yml` shares your `~/.gitconfig` with the container, so the commits you make there count as yours.

### Each time you work on the project

1. In a terminal, in the root of this repository, start the container in the background:

   ```bash
   docker compose up -d
   ```

   `docker compose ps` should list `analysis-env` as running.

2. In Positron, open the Command Palette (`Cmd+Shift+P` on Mac, `Ctrl+Shift+P` on Windows), type and run **Remote SSH: Show Remote Menu**, and pick **Connect to Host**.

3. Type `root@localhost:2222` and press Enter. A new Positron window opens.
   - If it asks for the platform of the remote host, pick **Linux**.
   - If it asks whether you trust the host (a "fingerprint"), click **Continue**.
   - The first time, Positron installs its server inside the container, which takes a few minutes.

4. Open the project folder. The bottom-left corner shows `SSH: localhost:2222`, but the Explorer says **No folder opened** and the terminal starts in `/root`, which has no project files. That is normal. Click **Open Folder**, clear the path box, type `/workspace`, and click OK (you may need to click OK a few times). The window reloads, and the Explorer shows **WORKSPACE [SSH: LOCALHOST:2222]** with the project files.

5. Pick the Python interpreter (check this every time).
   - Click the interpreter button at the top right of the window. The **Running Interpreter Sessions** menu only lists sessions that are already running (such as `/usr/bin/python3`, the container's system Python - not the one you want).
   - Click **New Console Session...** and pick **Python 3.x (uv: dsci-522-group-6-predicting-term-deposit-subscription)**, with the path `/opt/venv/bin/python` - the environment built from `uv.lock`.
   - If it isn't in the list, run **Python: Select Interpreter**, choose **Enter interpreter path...**, and type `/opt/venv/bin/python`.
   - Do **not** pick `/workspace/.venv`: that is an environment from your own computer and does not run in the container.
   - To check, run `import sys; print(sys.executable)` in the Console. It should print `/opt/venv/bin/python`.

6. Work as usual. The Terminal, Console, and **Render** button all run inside the container.

7. When you are done, close the Positron window, then stop and remove the container in a terminal on your computer:

   ```bash
   docker compose down
   ```


### If it does not connect

   * **No Remote SSH commands in the Command Palette:** install the **Open Remote - SSH** extension by jeanp413.

   * **The container's Python is not listed:** run **Python: Select Interpreter → Enter interpreter path... →** `/opt/venv/bin/python`, then confirm with `import sys; print(sys.executable)`.

   * **The interpreter still does not appear:** run **Developer: Reload Window,** then select it again.

   * **It asks for a password:** the container cannot see your key. Check that your key is named `id_ed25519.pub`, or change the key path in `docker-compose.yml`.

   * **`~/.ssh/id_ed25519.pub` is a folder:** Docker created it because the key did not exist yet. Run `docker compose down`, delete that folder, create the key (see the [README](README.md)), and start again.

   * **`~/.gitconfig` is a folder:** the same happened with your Git settings. Run `docker compose down`, delete that folder, set your name and email (above), and start again.

   * **"Remote host identification has changed":** you are using a new image. Run `ssh-keygen -R "[localhost]:2222"`, then connect again.

   * **GitHub asks you to sign in when you push:** sign in once in the browser window Positron opens. Positron remembers it.
   
   * **Port 2222 is already in use:** change the first `2222` in `docker-compose.yml` to another number (e.g. `2223`), and connect to that port instead.

   * **Every file shows as changed (Windows, cloned before `.gitattributes` was added):** a line-ending mismatch. Commit any real changes first, then run `git rm --cached -r . -q` followed by `git reset --hard`. This discards uncommitted changes, so commit first.

More detail: [Working in a container over ssh with Positron](https://ubc-dsci.github.io/reproducible-and-trustworthy-workflows-for-data-science/lectures/containers-ssh-positron.html).

To re-run the analysis and render the report without opening the container:

```bash
docker compose run --rm analysis-env uv run quarto render reports/term_deposit_subscription_predictor_report.qmd
```

## Adding or Updating a Package

On a new branch, add the package with `uv add <package>==<version>` (this pins the version in `pyproject.toml` and updates `uv.lock`), then commit the changed `pyproject.toml` and `uv.lock` together and push them. GitHub Actions then builds and publishes a new image on Docker Hub, and commits the new `sha-` tag to the `image:` line of `docker-compose.yml` on your branch. When the workflow finishes, get that commit and download the new image:

```bash
git pull
docker compose pull
```

Then merge the branch into `main` in a pull request.

## Publishing the Report

The report on GitHub Pages is a copy of the rendered report at `docs/index.html`. Each time you re-render the report, copy it there again, commit, and push:

```bash
cp reports/term_deposit_subscription_predictor_report.html docs/index.html
git add docs/index.html
git commit -m "Update published report"
git push
```

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
   docker compose run --rm analysis-env uv run quarto render reports/term_deposit_subscription_predictor_report.qmd
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


## Attribution

This contributing guide adapts elements of the [dplyr contributing guide](https://github.com/tidyverse/dplyr/blob/main/.github/CONTRIBUTING.md) and the [tidyverse guide to reproducible examples](https://tidyverse.org/help/#reprex). It has been modified to reflect this project's workflow and AI policy.


