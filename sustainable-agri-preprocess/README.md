# Sustainable Agriculture: Data Preprocessing Pipeline

This repository operationalizes an **end-to-end Kaggle → Jupyter → GitHub** data-prep workflow tailored for sustainable agriculture use cases (e.g., crop yield prediction, soil/irrigation planning, pest/disease monitoring).

## Quick Start (Local)

1. **Clone or unzip** this repo locally.
2. Create and activate a Python environment (choose one):
   ```bash
   # Option A: venv
   python -m venv .venv
   # Windows
   .venv\Scripts\activate
   # macOS/Linux
   source .venv/bin/activate

   pip install --upgrade pip
   pip install -r requirements.txt
   ```

3. **Set up Kaggle API credentials** (one-time):
   - Get `kaggle.json` from your Kaggle account: **Kaggle → Account → Create New API Token**.
   - Place it at:
     - Windows: `C:\Users\<YOU>\.kaggle\kaggle.json`
     - macOS/Linux: `/home/<you>/.kaggle/kaggle.json` or `/Users/<you>/.kaggle/kaggle.json`
   - Ensure permissions (macOS/Linux):
     ```bash
     chmod 600 ~/.kaggle/kaggle.json
     ```

4. **Launch Jupyter**:
   ```bash
   jupyter notebook
   ```
   Open `notebooks/01_preprocess.ipynb` and follow the cells.

## Using the Kaggle API

Update the placeholder in the notebook and run the `Download from Kaggle` cell:
```python
from kaggle.api.kaggle_api_extended import KaggleApi
api = KaggleApi(); api.authenticate()
api.dataset_download_files("OWNER/DATASET-NAME", path="data/raw", unzip=True)
```

> Tip: For competitions, use `api.competition_download_files("comp-name", ...)` instead.

## Typical Preprocessing Steps Included
- Schema audit (`.info()`, `.describe()`), missing value heatmap (optional), and outlier checks.
- Date/time parsing and temporal alignment with weather/soil data.
- Categorical encoding (`OneHotEncoder`), numeric imputation (`SimpleImputer`), scaling.
- Train/validation/test split with stratification (if relevant).
- Persist processed CSV/Parquet into `data/processed/`.

## Ship to GitHub
```bash
git init
git add .
git commit -m "Initial commit: sustainable-agri preprocessing pipeline"
# Create a repo on GitHub first, then:
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```

## Project Structure
```
sustainable-agri-preprocess/
├─ data/
│  ├─ raw/          # Kaggle dumps (excluded from Git by default)
│  └─ processed/    # Cleaned artifacts for modeling
├─ notebooks/
│  └─ 01_preprocess.ipynb
├─ src/             # Helper utilities (optional)
├─ requirements.txt
├─ .gitignore
└─ README.md
```

## License
MIT