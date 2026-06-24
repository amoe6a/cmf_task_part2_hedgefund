# cmf_task_part2

This repository contains a reproducible Python 3.11 notebook implementation for the Part 2 coding task.

## Repository structure

- `main.ipynb` - final self-contained notebook.
- `data/crypto_ohlcv.csv` - committed historical OHLCV data snapshot for 135 cryptocurrency pairs.
- `data/sol_implied_volatility_call_120.csv` - reproducible proxy IV data used by the SOL IV/Parkinson volatility-ratio strategy.
- `pyproject.toml` and `uv.lock` - reproducible Python 3.11 environment.
- `Dockerfile` - optional containerized JupyterLab runtime.

## Run locally with uv

```powershell
uv sync
uv run python -m ipykernel install --user --name cmf_task_part2 --display-name "cmf_task_part2"
```

Open `main.ipynb` in VS Code, Jupyter, or another notebook UI and select the `cmf_task_part2` kernel.

## Run with Docker

```bash
docker build -t cmf_task_part2 .
docker run --rm -p 8888:8888 cmf_task_part2
```

Then open the JupyterLab URL printed in the Docker logs.

## Validate the notebook

PowerShell:

```powershell
New-Item -ItemType Directory -Force .nbvalidate | Out-Null
uv run jupyter nbconvert --to notebook --execute main.ipynb --output main.executed.ipynb --output-dir .nbvalidate
```

Bash:

```bash
mkdir -p .nbvalidate
uv run jupyter nbconvert --to notebook --execute main.ipynb --output main.executed.ipynb --output-dir .nbvalidate
```

The command should finish without execution errors.

## Data and scope

The notebook uses Solana as the baseline cryptocurrency, BTC, ETH, SOL, XRP, ADA, DOGE, and LINK for the small portfolio tasks, and more than 100 eligible non-stable coins from the broad local OHLCV snapshot for the final expanded dynamic portfolio.

This is a research backtest, not a live trading bot. It does not include exchange order execution, order book slippage, funding/borrow costs, custody handling, or production monitoring.
