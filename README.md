# Predicting Spotify Song Genres from Song Features

**Authors:** Meredith Fraser, Vaibhav Korrapati, Gabriella Angelica Jemima Hasian, Siwei Wang

This repository was created as part of coursework (DSCI 522) in the UBC MDS program.

## Summary

In this repository, we ask whether a song's genre can be predicted from its audio features. The dataset has about 33,000 songs drawn from Spotify playlists across six genres: EDM, Latin, pop, R&B, rap and rock. The data was collected with the `spotifyr` R package and sourced from the TidyTuesday project. We split the data into training and test sets, explore the training data, and then fit a classification model to predict each song's playlist genre.

<!-- TODO: Once the analysis is complete, add a few sentences describing findings and results of the analysis. -->

In the current iteration of our analysis, a k-nearest neighbours (k-NN) model correctly predicted the genre of about half of the songs in the test set (50.56%). This suggests that audio features alone are only moderately useful for telling these genres apart, and that adding other information about songs or trying other models may improve predictions.

## Report

The rendered report is available here: <https://ubc-mds-2026-27.github.io/DSCI-522-Group-22-Spotify-Prediction/>

The source for the report is [`analysis/spotify-genre-prediction.qmd`](analysis/spotify-genre-prediction.qmd).

<!-- TODO: Add link to report hosted on GitHub Pages as part of Milestone 3 -->

## How to run the analysis

This project uses Docker to provide a reproducible environment for running the analysis. The container includes the software and dependencies required by the project, so you do not need to install Python, R, Quarto, or the project packages individually on your computer.

These instructions are for Windows and macOS users. On Windows, run the commands in PowerShell or Git Bash. On macOS, run them in Terminal.

### Pre-requisites

Make sure the following software is installed and running on your machine:

- [Git](https://git-scm.com/install/) - for cloning the repository

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) - for running the project container. Docker Desktop must be running before executing Docker commands.

To check whether Docker is installed and running, open your terminal and run:

``` bash
docker --version
docker compose version
```

Both commands should return version information.

### Steps to run analysis

1.  Open a terminal and navigate to the directory where you want to store the project.

2.  Clone the repository and navigate into the project directory:

    ``` bash
    git clone https://github.com/UBC-MDS-2026-27/DSCI-522-Group-22.git
    cd DSCI-522-Group-22
    ```

3.  Set up an SSH key (if you do not already have one)

    The project Docker container uses SSH to support connecting to the container through Positron. If you already have an Ed25519 SSH key at \`\~/.ssh/id_ed25519\`, you can skip this step.

    Otherwise, generate a key by running:

    ``` bash
    ssh-keygen -t ed25519
    ```

    Press **Enter** at each prompt to accept the default location and settings. This creates a public key at \`\~/.ssh/id_ed25519.pub\`, which is mounted into the container for SSH authentication.

    If you do not have this key, Docker may create a directory or file with incorrect permissions or contents when mounting the key, and SSH connections to the container may fail.

4.  Download the project Docker image

    Make sure Docker Desktop is running before proceeding.

    From the root of the cloned repository, download the Docker image specified in `docker-compose.yml`:

    ``` bash
    docker compose pull
    ```

    Wait for the download to finish before moving to the next step.

5.  Render the report inside the container

    The report is rendered inside the Docker container, using the project's reproducible environment. You do not need to install the project's Python or R packages directly on your host computer.

    Make sure you are in the root directory of the repository when running the following commands.

    #### Render using Python, or Python and R

    Run:

    ``` bash
    docker compose run --rm analysis-env uv run quarto render
    ```

    #### Render using R only

    Run:

    ``` bash
    docker compose run --rm analysis-env quarto render
    ```

    If the report file is not specified in the project's `_quarto.yml` configuration, provide the report path explicitly after `quarto render`:

    ``` bash
    docker compose run --rm analysis-env uv run quarto render analysis/spotify-genre-prediction.qmd
    ```

    The rendering process will download the data, execute the analysis, and generate the rendered HTML report.

6.  Access the rendered report

    After rendering finishes, locate the generated HTML report in the project directory. The expected report file is: `analysis/spotify-genre-prediction.html`

    Open the HTML file in your web browser to view the report.

    #### Windows

    From PowerShell, you can open the report using:

    ``` bash
    start analysis/spotify-genre-prediction.html
    ```

    #### macOS

    From Terminal, you can open the report using:

    ``` bash
    open analysis/spotify-genre-prediction.html
    ```

7.  Container cleanup

    The `--rm` option in the rendering commands automatically removes the temporary container after the rendering process finishes. You do not need to manually stop or remove it.

    If you started a persistent container separately using:

    ``` bash
    docker compose up -d
    ```

    Stop and remove the container using:

    ``` bash
    docker compose down
    ```

For instructions on modifying the project, working inside the container using Positron, adding packages, and republishing the report, see CONTRIBUTING.md.

## Troubleshooting

- Problem : Docker commands fail or Docker daemon is unavailable\
  Solution : Make sure Docker Desktop is installed and running. Open Docker Desktop and wait until it has fully started before running the commands again.

- Problem : Docker compose pull fails\
  Solution : Check your internet connection and make sure Docker Desktop is running, then retry:

  ``` bash
  docker compose pull
  ```

- Problem : Commands are not recognized or fail to run\
  Solution : Make sure you are running the commands from the root directory of the cloned DSCI-522-Group-22 repository. On Windows, use PowerShell or Git Bash. On macOS, use Terminal.

- Problem : Report rendering fails\
  Solution : Check the error message in the terminal. Make sure you are using the correct rendering command for the environment (Python, Python and R, or R only) and that Docker is running.

- Problem : Report HTML cannot be found after rendering\
  Solution : Check the rendering output in the terminal to confirm whether Quarto completed successfully. If the report was rendered successfully but the HTML file is missing from your local project directory, verify that the project directory is correctly mounted into the container.

## Dependencies

The project environment is managed through Docker to ensure reproducibility across different operating systems. The following tools and versions are used within the project environment:

- [uv](https://docs.astral.sh/uv/) (version 0.9 or later)

- [Quarto](https://quarto.org/) (version 1.6 or later)

- Python 3.13

- [R](https://cran.r-project.org/) 4.6

Users do not need to install these dependencies individually on their local machines to run the analysis. Docker will provide the required environment.

## Data

We use the [Spotify Songs](https://github.com/rfordatascience/tidytuesday/blob/main/data/2020/2020-01-21/readme.md) data set from the TidyTuesday project. The data was collected from the Spotify Web API with the [`spotifyr`](https://www.rcharlie.com/spotifyr/) R package.

## Licenses

The code in this project is licensed under the [MIT License](LICENSE.md). The report is licensed under the [Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0)](LICENSE.md) license. See [`LICENSE.md`](LICENSE.md) for the full text of both licenses.

## Contributing

Please read our [contributing guidelines](https://github.com/UBC-MDS-2026-27/DSCI-522-Group-22-Spotify-Prediction/tree/gab-README-containersetup?tab=contributing-ov-file) and the [code of conduct](CODE_OF_CONDUCT.md) for instructions on the contribution workflow and expectations for all contributors.

## Use of generative AI

Team members used generative AI tools to varying degrees. Typical uses included boilerplate code, troubleshooting and documentation tweaks. The research question, analysis decisions and interpretation of results are our own. Every commit, issue and pull request was created by a team member and all pull requests were reviewed by a human before merging.