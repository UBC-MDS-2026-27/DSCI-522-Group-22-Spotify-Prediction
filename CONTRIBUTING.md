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

3.  If SSH key is missing, run this in your local terminal:

    ``` bash
    ls ~/.ssh/id_ed25519.pub
    ```

    If the key does not exist, follow the SSH key setup instructions in the [README](README.md).

4.  To check container logs, run this in your local terminal:

    ``` bash
    docker compose logs analysis-env
    ```

5.  To restart the container, run this in your local terminal:

    ``` bash
    docker compose restart analysis-env
    ```

6.  If Positron is using the wrong Python interpreter, follow the Select the Python Interpreter instructions (Step 6) in the [Working in the Container with Positron over SSH] section again.

## Reporting Bugs

If you find a bug, please [open a GitHub issue](https://github.com/UBC-MDS-2026-27/DSCI-522-Group-22-Spotify-Prediction/issues) and include:

- A description of the problem.
- Steps to reproduce it.
- Expected and actual results.

## Suggesting Improvements

We welcome suggestions for improving our code, analysis, or documentation. Please open a GitHub issue to describe your idea before making major changes.

## Making Contributions

1.  Clone the repository and create a new branch from the latest `main`.
2.  Make your changes and commit them with clear messages.
3.  Push your branch to GitHub and open a pull request (PR).
4.  Describe your changes and link the related issue if applicable.
5.  Have at least one other team member review and approve your PR before merging.

Please do not push changes directly to `main`.

## Generative AI Policy

AI tools such as ChatGPT, Claude, and GitHub Copilot may be used to assist with coding, debugging, and writing.

However, contributors must:

- Review, understand, and verify all AI-assisted work.
- Disclose which AI tools were used and how they were used.
- Take full responsibility for their contributions.
- Open, review, and merge GitHub issues and pull requests themselves. AI agents must not perform these actions on their behalf.

## Code of Conduct

All contributors are expected to follow our [Code of Conduct](CODE_OF_CONDUCT.md).