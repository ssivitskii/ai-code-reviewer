# Contributing

Bug reports, documentation fixes and focused improvements are welcome.

## Local setup

Fork [ssivitskii/ai-code-reviewer](https://github.com/ssivitskii/ai-code-reviewer), clone your fork and create a branch. Use Python 3.11 and run from the repository root:

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -e ".[dev,api,demo]"
python -m pytest
```

Follow [README.md](README.md) for data and runtime configuration. Never commit credentials or private datasets. Model-provider keys are only needed when exercising real provider calls in AI Code Reviewer.

## Pull requests

Describe the problem, the resulting behavior and how you checked the change. Keep changes focused, add relevant regression tests for behavior changes and update documentation when commands or interfaces change.

For metric claims, include dataset provenance, preprocessing, split, random seed, model parameters and the command that produced the results. Distinguish measured results from example output.

Report bugs through [Issues](https://github.com/ssivitskii/ai-code-reviewer/issues), including a minimal reproduction, Python version and relevant logs with secrets removed.
