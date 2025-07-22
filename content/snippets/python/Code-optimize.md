---
title: Code optimize
---

## Profiling 

```python
import cProfile
import optuna
import time
from sklearn.metrics import roc_auc_score
from sklearn.model_selection import StratifiedKFold

# Define the LSTMModel class and Trainer class here

# Define the objective function for Optuna optimization
def objective(trial):
    # ... (rest of the code)

# Profile the objective function
profiler = cProfile.Profile()
profiler.enable()

# Perform hyperparameter optimization with Optuna
study = optuna.create_study(direction='maximize')
study.optimize(objective, n_trials=100)

profiler.disable()
profiler.print_stats(sort='cumulative')

```