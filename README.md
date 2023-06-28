[![View on Medium](https://img.shields.io/badge/Medium-View%20on%20Medium-blue?logo=medium)](https://towardsdatascience.com/how-to-structure-an-ml-project-for-reproducibility-and-maintainability-54d5e53b4c82?sk=c3d05ae5b8ccc95822618d0dacfad8a4)

# Data Science Cookie Cutter
## Quick Start
### Set up the environment
1. Install [Poetry](https://python-poetry.org/docs/#installation)
2. Set up the environment:
```bash
make setup
make activate
```
### Install new packages
To install new PyPI packages, run:
```bash
poetry add <package-name>
```

### Run Python scripts
To run the Python scripts to process data, train model, and run a notebook, type the following:
```bash
make pipeline
```
### View all flow runs
A [flow](https://docs.prefect.io/concepts/flows/) is the basis of all Prefect workflows.

To view your flow runs from a UI, sign in to your [Prefect Cloud](https://app.prefect.cloud/) account or spin up a Prefect Orion server on your local machine:
```bash
prefect orion start
```
Open the URL http://127.0.0.1:4200/, and you should see the Prefect UI:

![](images/prefect_cloud.png)

### Run flows from the UI

After [creating a deployment](https://towardsdatascience.com/build-a-full-stack-ml-application-with-pydantic-and-prefect-915f00fe0c62?sk=b1f8c5cb53a6a9d7f48d66fa778e9cf0), you can run a flow from the UI with default parameters:

![](https://miro.medium.com/max/1400/1*KPRQS3aeuYhL_Anv3-r9Ag.gif)
or custom parameters:
![](https://miro.medium.com/max/1400/1*jGKmPR3aoXeIs3SEaHPhBg.gif)

### Auto-generate API documentation

To auto-generate API document for your project, run:

```bash
make docs_save
```

### Run tests when creating a PR
When creating a PR, the tests in your `tests` folder will automatically run. 

![](images/github_actions.png)


## Project Structure

# Init Project
python -m venv venv
venv\Scripts\activate.bat
python -m pip install pip setuptools wheel
python -m pip install -e .

# Params to train model
from config import config
from src import main
from pathlib import Path
args_fp = Path(config.CONFIG_DIR, "args.json")
main.train_model(args_fp)

# Optimize hiperparameters
from config import config
from src import main
from pathlib import Path
args_fp = Path(config.CONFIG_DIR, "args.json")
main.optimize(args_fp, study_name="optimization", num_trials=20)

# Tracking experiments
from config import config
from src import main
from pathlib import Path
args_fp = Path(config.CONFIG_DIR, "args.json")
main.train_model(args_fp, experiment_name="baselines", run_name="sgd")

# Predict text labels
text = "Transfer learning with transformers for text classification."
run_id = open(Path(config.CONFIG_DIR, "run_id.txt")).read()
predict_tag(text=text, run_id=run_id)


