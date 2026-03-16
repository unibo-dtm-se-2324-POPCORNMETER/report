---
title: Deployment
has_children: false
nav_order: 8
---

# Deployment

## User installation

Popcorn Meter is primarily a Streamlit application intended to run on the user's machine.

Users need:

- Python >=3.10 and <4.0.0 (recommended: Python 3.12+)
- `pip`
- Poetry (recommended for reproducible setup)

### Installation from source (recommended)

```bash
git clone https://github.com/unibo-dtm-se-2324-POPCORNMETER/artifact.git
cd artifact
pip install -r requirements.txt
poetry install
```

### Configuration

For full functionality, create `.streamlit/secrets.toml` and add API keys:

```toml
OMDB_API_KEY = "your_omdb_key"
TMDB_API_KEY = "your_tmdb_key"
```

Without `OMDB_API_KEY`, movie details lookup will fail; without `TMDB_API_KEY`, trending titles will be unavailable and the UI falls back to a small built-in list.

### Run the application

```bash
poetry run popcorn-meter
# or
poetry run python -m popcorn_meter
```

### Optional installation from TestPyPI

The package can also be installed from TestPyPI:

```bash
pip install --index-url https://test.pypi.org/simple/ --extra-index-url https://pypi.org/simple popcorn-meter==<version>
```

## Server-side installation

A dedicated server is not required for normal use.
Popcorn Meter is designed to run locally on the user's machine with local SQLite persistence.

### Optional hosted deployment

A hosted Streamlit deployment is possible (for example, Streamlit Community Cloud).
In that case:

- Deploy from the artifact repository
- Set app secrets (`OMDB_API_KEY`, `TMDB_API_KEY`) in Streamlit Cloud
- Hosted deployment may require external persistent storage or another persistence strategy if long-term account/watchlist data must survive restarts, because the current application uses a local SQLite file

If hosted on Streamlit Cloud default settings, storage can be ephemeral, so user data may not persist across restarts/redeployments.

## Additional server software

No additional server software (message broker, external DB server, etc.) is required by default.
The project uses SQLite as embedded local storage.
