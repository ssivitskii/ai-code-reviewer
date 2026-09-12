# AI Code Reviewer

**LLM-assisted code review with a CLI, FastAPI service and Streamlit interface.**

[Source](https://github.com/ssivitskii/ai-code-reviewer) · [Issues](https://github.com/ssivitskii/ai-code-reviewer/issues) · [Contributing](CONTRIBUTING.md)

## What it does

Reviews files, Git diffs and staged changes, returning structured issues and a summary. Provider adapters support OpenAI, Anthropic and a local OpenAI-compatible endpoint. Review modes are `quick`, `standard` and `deep`.

**Stack:** Python · OpenAI / Anthropic SDKs · Click · FastAPI · Streamlit

## Run locally

Use Python 3.11 and run these commands from the repository root:

```bash
git clone https://github.com/ssivitskii/ai-code-reviewer.git
cd ai-code-reviewer
python -m venv .venv
source .venv/bin/activate
python -m pip install -e ".[api,demo,dev]"
```

Set `OPENAI_API_KEY` or `ANTHROPIC_API_KEY` in your environment for the corresponding provider. Choose a model available to your account:

```bash
ai-review review examples/sample_bad_code.py --provider openai --model YOUR_MODEL --output json
ai-review staged --repo . --provider openai --model YOUR_MODEL
ai-review diff changes.diff --provider openai --model YOUR_MODEL
```

For a local server, set `LOCAL_LLM_URL` to its OpenAI-compatible base URL (default: `http://localhost:11434/v1`) and use `--provider local --model YOUR_LOCAL_MODEL`. The server and model must already be running.

### Interfaces

```bash
# FastAPI: interactive documentation at http://127.0.0.1:8000/docs
python -m uvicorn api.main:app --host 127.0.0.1 --port 8000

# Streamlit
python -m streamlit run demo/app.py
```

The API currently initializes the default OpenAI reviewer. `POST /review` returns top-level `status`, `issues`, `summary`, `positive_feedback` and `file_path` fields; `POST /review/diff` returns a list of review results. Provider/model selection shown above applies to the CLI.

## Repository map

| Path | Purpose |
| --- | --- |
| `src/ai_code_reviewer/` | Review engine, configuration, prompts and provider adapters |
| `cli/main.py` | Click commands |
| `api/main.py` | HTTP endpoints |
| `demo/app.py` | Streamlit interface |
| `action/` | Experimental GitHub Action integration |
| `tests/` | Automated tests |

## Validation and limitations

```bash
python -m pytest
```

Tests use mocked model responses; they do not establish real-world review accuracy. No reproducible quality benchmark is published in this repository. To evaluate a provider, record the model version, prompt, labelled code samples, false positives, missed issues, latency and cost.

The GitHub Action integration is experimental: its dependency installation and API-key wiring need verification before adoption. `ai-review init` writes a configuration template; CLI review commands do not automatically load that file. Use the explicit configuration API when needed. LLM findings require human review, and provider availability depends on your configuration.

## License

[MIT](LICENSE)
