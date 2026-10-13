# NEMESIS — Fleet Notebook (hosted VM)

The fleet + circuit breaker as a **hosted notebook**. The notebook runtime is the VM:
it executes on the host service's CPU/GPU, not on any local box.

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Tarpy666/nemesis-notebook/blob/main/nemesis_fleet.ipynb)
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/Tarpy666/nemesis-notebook/main?filepath=nemesis_fleet.ipynb)
[![Kaggle](https://kaggle.com/static/images/open-in-kaggle.svg)](https://kaggle.com/kernels/welcome?src=https://github.com/Tarpy666/nemesis-notebook/blob/main/nemesis_fleet.ipynb)

## What it is

- **Circuit breaker** — faithful mirror of `covenant.js` (`THRESHOLD=3`, `COOLDOWN=30s`,
  closed → open → half-open → closed).
- **OOM guard** — concurrency capped against real `MemAvailable` and a per-worker byte budget.
- **Guarded parallel pool** — retries every task across the breaker; opens fast on repeated failure.

## What it is not

- Not WebGPU. A notebook kernel is server-side **CUDA** (or CPU); `navigator.gpu` does not exist
  there. WebGPU belongs to the browser client, not the kernel.
- Not the local `opencode` fleet. The local gateway is not reachable from a hosted VM; add a model
  key (e.g. a Colab secret) to make `task()` an LLM worker.

## Launch

- **Colab** (needs a Google session; gives a free GPU VM): the badge above.
- **Binder** (no account; headless-launchable; CPU, ephemeral):
  `https://mybinder.org/v2/gh/Tarpy666/nemesis-notebook/main?filepath=nemesis_fleet.ipynb`
- **Kaggle** (needs `KAGGLE_USERNAME`/`KAGGLE_KEY` for headless): the badge above.
