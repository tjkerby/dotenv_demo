# dotenv demo

A tiny demo of keeping secrets out of your code with a `.env` file. The notebook in this repo ([apod.ipynb](apod.ipynb)) loads a NASA API key from `.env` with [python-dotenv](https://pypi.org/project/python-dotenv/) and uses it to fetch NASA's [astronomy picture of the day](https://apod.nasa.gov/apod/astropix.html).

## What you'll need

- Python 3.13+ and [uv](https://docs.astral.sh/uv/getting-started/installation/)
- A free NASA API key (see below)

## Setup

1. **Clone this repo** and open a terminal in the project folder.

2. **Install the dependencies:**

   ```
   uv sync
   ```

   This creates a virtual environment (`.venv/`) with `requests` and `python-dotenv`.

3. **Get a NASA API key:** fill out the form at <https://api.nasa.gov/#signUp>. It's free and the key arrives by email almost immediately.

4. **Create a file named `.env` in the project root** (the same folder as this README) with these two lines:

   ```
   NASA_API_KEY="paste your key from the email here"
   SECRET_TEXT="any secret message you like"
   ```

   - `NASA_API_KEY` is what the notebook sends to the API.
   - `SECRET_TEXT` is just a second secret the notebook prints at the end, to show that *any* value can live in `.env` — not just keys.

   Note that `.env` is listed in `.gitignore`, so it will never be committed — that's the whole point of this pattern. Your secrets stay on your machine; the repo only ever contains code that *reads* them.

5. **Open `apod.ipynb`** (make sure the kernel is the project's `.venv` Python) and run the cells top to bottom.

## Troubleshooting

- **`KeyError: 'NASA_API_KEY'`** — the notebook can't find `.env`. Check that the file is named exactly `.env`, sits in the project root, and that you've run the `load_dotenv()` cell. If you created `.env` after starting the notebook, rerun the cells from the top.
- **`500 Server Error` or "The API served a placeholder"** — NASA's APOD service is going through a backend migration and is currently flaky. This is on NASA's end, not yours; just rerun the fetch cell.