# MNIST Digit Recognition - Deploy Repo

**Live app:** https://huggingface.co/spaces/harpreetmalhotra/mnist-digit-recognition

This is the deployment version of my MNIST project. The actual development repo is [nea-code](https://github.com/iceey/nea-code) - this one just has the files that go on Hugging Face Spaces.

## HF Spaces Config

HF Spaces needs a YAML block at the top of the README inside `deploy/`. These are the settings it uses:

```yaml
sdk: gradio
sdk_version: 4.36.1
python_version: 3.11.0
app_file: app.py
```

## Differences from nea-code

A few things had to change for deployment:

- `tensorflow` becomes `tensorflow-cpu` (the full version is huge and HF doesn't have a GPU on the free tier anyway)
- `app_ui.py` is renamed to `app.py` because that's what HF expects
- The database and all 9 trained models are included so users don't have to train anything themselves

The rest of the code (models.py, utils.py, init_db.py) is copied straight from nea-code.

## How to Deploy

Just upload the contents of the `deploy/` folder:

```bash
cd deploy
hf upload harpreetmalhotra/mnist-digit-recognition . . --repo-type space
```

HF picks up the YAML from the README and sorts out the Python version and packages.

## What's in Here

- `deploy/` - the folder that actually gets uploaded to HF Spaces
  - `README.md` - has the YAML config HF needs
  - `app.py` - the main Gradio app
  - `models.py`, `utils.py`, `init_db.py` - same as nea-code
  - `requirements.txt` - packages (tensorflow-cpu instead of tensorflow)
  - `artifacts/` - pre-trained models and database
- `README.md` - this file
- `LIVE_URL.txt` - just the live link for quick reference
