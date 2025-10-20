# End-to-End Book Recommender System

## Overview
An end-to-end book recommendation project that provides a training pipeline and a Streamlit-based UI to serve recommendations with poster images. The app can train the recommendation pipeline from the UI and show recommended book titles + posters in a multi-column layout.

## Features
- Streamlit UI for interactive recommendations and poster display.
- Training pipeline entrypoint to run the end-to-end training process (data ingestion → preprocessing → model training → artifact serialization).
- Packaging support via setup.py and a simple project template generator/snippet.
- Dockerfile for containerized deployment of the Streamlit app.
- MIT license included.

## Repository layout (key files)
- app.py - Streamlit application and recommendation-serving logic (fetch_poster, recommend_book, recommendations_engine). The UI shows recommendations in columns with poster images and can trigger training from the UI.
- main.py - launches the TrainingPipeline to run the training pipeline.
- requirements.txt - Python dependencies used by the project; confirm/install these before running.
- Dockerfile - container image setup that installs requirements and runs the Streamlit app on port 8501.
- setup.py - package metadata and install configuration for the local package.
- template.py - project scaffolding and logging helper used in the repository template utilities.
- LICENSE - MIT license for the project.

Prerequisites
- Python 3.7+ (the Dockerfile uses python:3.7-slim-buster).
- Git to clone the repository.
- Optional: Docker to run the app in a container.

## Installation - local
1. Clone the repository:
```bash
git clone https://github.com/Anurag0798/End-to-End-Book-Recommender-System
```
```bash
cd End-to-End-Book-Recommender-System
```

2. (Recommended) Create & activate a virtual environment:
   ```bash
   python -m venv .venv

   # Linux / macOS
   source .venv/bin/activate

   # Windows (PowerShell)
   .venv\Scripts\Activate.ps1
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
Confirm that core packages (streamlit, pandas, numpy, scikit-learn) are present; add any missing packages before running.

Optional: install package in editable mode for development
```
pip install -e .
```
This uses setup.py packaging metadata.

### Run the training pipeline
- The training pipeline entrypoint is main.py. Running this will create a TrainingPipeline object and execute start_training_pipeline():
```
python main.py
```
This runs the end-to-end training workflow defined by the project.

### Run the Streamlit app
- Start the UI locally:
```
streamlit run app.py
```
The app shows a header "End to End Books Recommendation System", provides a selection box for books, displays recommendations in columns with poster images, and can trigger training from the UI.

### Required artifacts
- The Streamlit app loads serialized artifacts (e.g., book pivot, final rating / model artifacts, book names and poster data). Ensure any expected pickles (such as book_names.pkl in templates or other serialized objects your pipeline emits) are present at the paths referenced by the code. If the app cannot find these artifacts, it will raise errors when attempting to recommend.

### Docker (build & run)
- Build image:
```
docker build -t book-recommender .
```
- Run container:
```
docker run -p 8501:8501 book-recommender
```
The Dockerfile installs requirements and runs streamlit on port 8501.

### Configuration notes
- If you change artifact filenames or paths (for serialized models, pivot tables, pickles), update the paths referenced in app.py or the configuration the app reads. The app expects certain serialized objects to be available for recommendation and poster fetch logic.

## Troubleshooting
- Missing packages: confirm requirements.txt includes all runtime dependencies and reinstall.
- Artifact loading errors: verify that serialized artifacts produced by the training pipeline exist and were created with compatible Python/pickle versions.
- Streamlit errors: ensure the Streamlit package is installed and you run with the same Python environment used for installation.

## Contributing
- Fork the repository, create a feature branch, implement & test changes, then open a PR. Update requirements/setup and README when adding new dependencies or modifying scripts.

## License
- MIT License - see LICENSE for full text.