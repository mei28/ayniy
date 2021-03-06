# Ayniy, All You Need is YAML

Ayniy is a supporting tool for machine learning competitions.

[**Documentation**](https://upura.github.io/ayniy-docs/) | [**Slide (Japanese)**](https://speakerdeck.com/upura/ayniy-with-mlflow)

```python
# Import packages
import yaml
from sklearn.model_selection import StratifiedKFold
from ayniy.preprocessing.runner import Tabular
from ayniy.model.runner import Runner

# Load configs
f = open('configs/fe000.yml', 'r+')
fe_configs = yaml.load(f, Loader=yaml.SafeLoader)
g = open('configs/run000.yml', 'r+')
run_configs = yaml.load(g, Loader=yaml.SafeLoader)

# Difine CV strategy as you like
cv = StratifiedKFold(n_splits=5, shuffle=True, random_state=7)

# Feature engineering
tabular = Tabular(fe_configs, cv)
tabular.create()

# Modeling
runner = Runner(run_configs, cv)
runner.run_train_cv()
runner.run_predict_cv()
runner.submission()
```

## Examples

- [atmaCup #5](https://github.com/upura/atma-comp5)
- [ProbSpace YouTube](https://github.com/upura/probspace-youtube)

## Environment

```
docker-compose -d --build
docker exec -it ayniy-test bash
```

## MLflow

```
cd experiments
mlflow ui
```

## Test

```
cd test
pytest --cov=. --cov-report=html
```

## Docs
In container,
```
cd docs
make html
```

Out of container,
```
sh deploy.sh
```
https://github.com/upura/ayniy-docs
