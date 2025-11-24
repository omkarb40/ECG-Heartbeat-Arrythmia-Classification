Venv setup and verification

This README contains steps to finish the virtual environment setup, install packages required for `code.ipynb`, register the kernel with Jupyter, and verify that key imports (including PyTorch with MPS) work.

1) Activate your venv (example - adjust path/name):

# If your venv directory is named `.venv` inside the project
source .venv/bin/activate

# Or if you created venv elsewhere, use its activate script path
# Example: source /path/to/venv/bin/activate

2) Upgrade pip (recommended):

python -m pip install --upgrade pip setuptools wheel

3) Install the project dependencies from `requirements.txt`:

python -m pip install -r requirements.txt

Notes about PyTorch on macOS (MPS):
- For Apple Silicon (M1/M2/M3/M4) with MPS support, follow the official instructions at https://pytorch.org/get-started/locally/ and select "macOS" + "pip" + your Python version to get the recommended command. In many cases the following works, but if you want to be certain, use the website selector:

# Example (may install wheels appropriate for your system):
python -m pip install torch torchvision torchaudio

If you hit issues with the default wheel, use the command shown on the PyTorch website for macOS (it will point at the correct extra-index URL if necessary).

4) Register the venv as a Jupyter kernel (so `code.ipynb` can use it):

# Replace `my_venv` with a short name you want displayed in Jupyter
python -m ipykernel install --user --name=my_venv --display-name "Python (my_venv)"

After that, in Jupyter/VS Code notebook UI choose the kernel named "Python (my_venv)" for `code.ipynb`.

5) Quick verify snippet (run this in a new notebook cell or as a short script):

import sys
import numpy as np
import pandas as pd
import matplotlib
import seaborn as sns
import sklearn
import torch

print('python:', sys.executable)
print('numpy:', np.__version__)
print('pandas:', pd.__version__)
print('matplotlib:', matplotlib.__version__)
print('seaborn:', sns.__version__)
print('sklearn:', sklearn.__version__)
print('torch:', torch.__version__)

# Check device availability for PyTorch (MPS on Apple Silicon):
if hasattr(torch.backends, 'mps') and torch.backends.mps.is_available():
    print('MPS available: True')
else:
    print('MPS available: False')

6) If you prefer to pin exact versions after a successful install, run:

python -m pip freeze > pinned-requirements.txt

This will create `pinned-requirements.txt` with exact versions which you can commit if desired.

Troubleshooting
- If an import fails, ensure the notebook kernel is the same Python interpreter as the activated venv (compare `sys.executable` printed above).
- For PyTorch wheel issues on macOS, use the exact command from https://pytorch.org/get-started/locally/.

If you'd like, I can now:
- attempt to detect your venv and run installs automatically (I tried to configure the environment but the environment configuration step was skipped), or
- register and configure the notebook kernel for you if you give me the venv path.  
