# Contributing to DSCI 522 Group 22

Thank you for your interest in contributing to our Spotify Genre Prediction project! Please follow the guidelines below.

## Setting Up the Development Environment

Before working inside the project container, make sure you have completed the initial setup steps described in the [README](README.md), including:

- Setting up your SSH key (if you do not already have one).
- Pulling the Docker image using `docker compose pull`.

## Working in the Container with Positron over SSH

1.  [Install Positron](https://positron.posit.co/download) and follow the instruction match with your operating system.

2.  Check your Git identity

    Open your local terminal and run:

    ``` bash
    git config --global user.name
    git config --global user.email
    ```

    If either is missing or incorrect, configure it:

    ``` bash
    git config --global user.name "Your Name"
    git config --global user.email "your-email@example.com"
    ```

3.  Start the container

    From the root of your project repository, run:

    ``` bash
    docker compose up -d analysis-env
    docker compose ps
    ```

    Confirm that the container is running.

4.  Connect to the container via SSH

    Test the SSH connection from your local terminal:

    ``` bash
    ssh -p 2222 root@localhost
    ```

    If prompted to confirm the host, type `yes`. If the connection succeeds, type `exit` to return to your local terminal.

5.  Connect using Positron

    1.  Open Positron and open the Command Palette (`Cmd + Shift + P` on macOS or `Ctrl + Shift + P` on Windows/Linux).

    2.  Search for **Remote SSH: Show Remote Menu**.

    3.  Select **Connect to Host**.

    4.  Enter the SSH host:

        ``` bash
        root@localhost
        ```

    5.  When prompted for the port, enter:

        ``` bash
        2222
        ```

    6.  If prompted to confirm the host authenticity, select **Continue** or **Yes**.

    7.  Once connected, open the project folder:

        ```         
        /workspace
        ```

6.  Select the Python interpreter

    Inside the remote Positron window:

    1.  Open the Command Palette (`Cmd + Shift + P` on macOS or `Ctrl + Shift + P` on Windows/Linux).

    2.  Search for **Python: Select Interpreter**.

    3.  Select the Python interpreter located at `/opt/venv/bin/python` from the list.

    4.  If the interpreter is not listed, select **Enter interpreter path**, and enter:

        ```         
        /opt/venv/bin/python
        ```

    5.  Open the Positron terminal and verify the selected interpreter:

        ```         
        which python
        python --version
        ```

        The path should return `/opt/venv/bin/python`, confirming that Positron is using the project's Python environment inside the container.

    6.  Stop the container

        When finished working, stop the container from your local terminal:

        ``` bash
        docker compose down
        ```

    7.  **To start working again, repeat Step 4.**

## Troubleshooting

1.  If container is not running, run this in your local terminal:

    ``` bash
    docker compose up -d analysis-env
    docker compose ps
    ```

2.  If SSH connection fails, run this in your local terminal:

    ``` bash
    ssh -p 2222 root@localhost
    ```

    If it fails, confirm Docker is running, the container is active, and port `2222` is available.

3.  If you encounter a connection issue when using `localhost`, try connecting with the loopback IP address instead:

    ``` bash
    ssh -p 2222 root@127.0.0.1
    ```

    For Positron, you can also try entering the following SSH host:

    ``` bash
    root@127.0.0.1:2222
    ```

4.  If SSH key is missing, run this in your local terminal:

    ``` bash
    ls ~/.ssh/id_ed25519.pub
    ```

    If the key does not exist, follow the SSH key setup instructions in the [README](README.md).

5.  To check container logs, run this in your local terminal:

    ``` bash
    docker compose logs analysis-env
    ```

6.  To restart the container, run this in your local terminal:

    ``` bash
    docker compose restart analysis-env
    ```

7.  If Positron is using the wrong Python interpreter, follow the Select the Python Interpreter instructions (Step 6) in the [Working in the Container with Positron over SSH] section again.

## Adding or Updating a Package

When adding a new package or updating an existing one, make sure the changes are made within the project's environment so that the dependencies are reflected in the Docker image.

1.  Create a branch before changing the project environment.

    Start from the latest `main` branch and create a new branch for your changes:

    ``` bash
    git switch main
    git pull
    git switch -c new-branch-name
    ```

    Replace `new-branch-name` with a descriptive branch name.

2.  Add the package inside the container using `uv` to add the package and specify its version:

    ``` bash
    uv add package-name==version
    ```

    Replace `package-name` and `version` with the package name and required version. This updates the project's dependency files.

3.  Commit the updated environment files and push your branch to GitHub:

    ``` bash
    git add pyproject.toml uv.lock
    git commit -m "Add package-name dependency"
    git push -u origin add-package-name
    ```

4.  Wait for the new Docker image to be built.

    Pushing your branch triggers GitHub Actions to build and publish a new Docker image and update the image tag in `docker-compose.yml` on your branch. Once the GitHub Actions workflow in the Actions tab completes successfully (green check mark), the updated image is ready.

5.  Stage the updated dependency files and run:

    ``` bash
    git add pyproject.toml uv.lock
    ```

6.  Commit your changes using the project's commit message convention:

    ``` bash
    git commit -m "Add package-name dependency"
    ```

    Replace `package-name` with the actual package name you added or updated.

7.  Push your branch to GitHub and run:

    ``` bash
    git push -u origin add-package-name
    ```

    Replace `add-package-name` with your actual branch name.

8.  Go to the project repository on GitHub and open a pull request from your branch into `main`.

9.  Wait for your pull request to be reviewed and merged into `main`. Address any requested changes before merging.

    After merging, GitHub Actions will build and publish a new Docker image and update the image SHA tag in `docker-compose.yml` on `main`.

    Do not manually edit the image SHA tag in `docker-compose.yml`.

10. After your pull request has been merged, update your local `main` branch and download the latest Docker image:

    ``` bash
    git switch main
    git pull
    docker compose pull
    ```

    Your local repository and Docker image are now updated with the new package dependency.

## Publish the Report

After making your final changes, re-render the report and publish the updated HTML to GitHub Pages.

1.  Re-render the report from the project root using the Docker container:

    ``` bash
    docker compose run --rm analysis-env uv run quarto render
    ```

2.  Copy the generated HTML file from `analysis/` to `docs/index.html`, replacing the existing published report:

    ``` bash
    cp analysis/spotify-genre-prediction.html docs/index.html
    ```

3.  Check your changes:

    ``` bash
    git status
    ```

4.  Stage and commit the updated report:

    ``` bash
    git add docs/index.html
    git commit -m "Add-Commit-Message"
    ```

5.  Push your working branch to GitHub:

    ``` bash
    git push origin your-branch-name
    ```

    Replace `your-branch-name` with your working branch name.

6.  Go to the project repository on GitHub and open a pull request from your branch into `main`.

7.  Wait for your pull request to be reviewed and merged into `main` for the published website to update.

8.  Verify the published report by visiting the updated project website and confirming that the latest changes are visible.

## Making Contributions

1.  Clone the repository and create a new branch from the latest `main`.
2.  Make your changes and commit them with clear messages.
3.  Push your branch to GitHub and open a pull request (PR).
4.  Describe your changes and link the related issue if applicable.
5.  Have at least one other team member review and approve your PR before merging.

Please do not push changes directly to `main`.

## Reporting Bugs

If you find a bug, please [open a GitHub issue](https://github.com/UBC-MDS-2026-27/DSCI-522-Group-22-Spotify-Prediction/issues) and include:

- A description of the problem.
- Steps to reproduce it.
- Expected and actual results.

## Suggesting Improvements

We welcome suggestions for improving our code, analysis, or documentation. Please open a GitHub issue to describe your idea before making major changes.

## Generative AI Policy

AI tools such as ChatGPT, Claude, and GitHub Copilot may be used to assist with coding, debugging, and writing.

However, contributors must:

- Review, understand, and verify all AI-assisted work.
- Disclose which AI tools were used and how they were used.
- Take full responsibility for their contributions.
- Open, review, and merge GitHub issues and pull requests themselves. AI agents must not perform these actions on their behalf.

## Code of Conduct

All contributors are expected to follow our [Code of Conduct](CODE_OF_CONDUCT.md).