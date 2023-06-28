## Project Structure

# Init Project
- python -m venv venv
- venv\Scripts\activate.bat
- python -m pip install pip setuptools wheel
- python -m pip install -e .

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


