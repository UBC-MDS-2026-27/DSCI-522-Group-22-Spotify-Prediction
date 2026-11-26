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

These instructions work on Windows and macOS. On Windows, run the commands in PowerShell or Git Bash. On macOS, run them in Terminal.

### Pre-requisites
Make sure the following dependencies are installed on your machine:
   - [uv](https://docs.astral.sh/uv/getting-started/installation/) - Python env and dependency manager
   - [Quarto](https://quarto.org/docs/get-started/) - Used to render the report

### Steps to run analysis
1. Clone the repository:

   ```bash
   git clone https://github.com/UBC-MDS-2026-27/DSCI-522-Group-22-Spotify-Prediction.git
   cd DSCI-522-Group-22-Spotify-Prediction
   ```

2. Setup Python environment:

   ```bash
   uv sync
   ```

3. Render the report. This downloads the data, saves it to `data/raw/` and `data/processed/`, runs the analysis, and writes `analysis/spotify-genre-prediction.html`:

   ```bash
   uv run quarto render analysis/spotify-genre-prediction.qmd
   ```

4. Open `analysis/spotify-genre-prediction.html` in a web browser to read the report.


## Dependencies

- [uv](https://docs.astral.sh/uv/) (version 0.9 or later)
- [Quarto](https://quarto.org/) (version 1.6 or later)
- Python 3.13

## Data

We use the [Spotify Songs](https://github.com/rfordatascience/tidytuesday/blob/main/data/2020/2020-01-21/readme.md) data set from the TidyTuesday project. The data was collected from the Spotify Web API with the [`spotifyr`](https://www.rcharlie.com/spotifyr/) R package.

## Licenses

The code in this project is licensed under the [MIT License](LICENSE.md). The report is licensed under the [Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0)](LICENSE.md) license. See [`LICENSE.md`](LICENSE.md) for the full text of both licenses.

## Contributing

Please read our [contributing guidelines](CONTRIBUTING.md) and the [code of conduct](CODE_OF_CONDUCT.md) before making contributions.

## Use of generative AI

Team members used generative AI tools to varying degrees. Typical uses included boilerplate code, troubleshooting and documentation tweaks. The research question, analysis decisions and interpretation of results are our own. Every commit, issue and pull request was created by a team member and all pull requests were reviewed by a human before merging.
