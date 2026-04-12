# Institutional-Asymmetry
Institutional Asymmetry, Endogenous Fragility, and Economic Growth
# Replication Code — *Institutional Asymmetry, Endogenous Fragility, and Economic Growth*

**Dr. Omer Cayirli** | Vietnamese-German University

---

## What is in this repository

This repository contains the Monte Carlo simulation scripts that produce the numerical results in Section 6 of the paper. There are three self-contained Python scripts:

| File | Paper section | What it does |
|---|---|---|
| `mc_block_1.py` | Section 6.2 (Table 1) | Micro-level comparative statics, drag mapping, spillover and premium extensions |
| `mc_block_2.py` | Section 6.3 | Dynamic stability: attractor classification, collapse incidence, timescale analysis |
| `mc_block_3.py` | Section 6.4 | Hysteresis, stimulus attenuation, and escape probability under repeated reforms |

Each script is independent. You can run one without running the others.

---

## Requirements

You need **Python 3.9 or later**. If you are not sure which version you have, open a terminal (on Mac/Linux) or Command Prompt (on Windows) and type:

```
python --version
```

or

```
python3 --version
```

You also need four Python packages. Install them by running this single command in your terminal:

```
pip install numpy pandas matplotlib scipy
```

If `pip` does not work, try `pip3` instead.

---

## How to run the scripts

There are three ways to run these scripts depending on your setup. Pick whichever is easiest for you.

---

### Option A — Run directly from the terminal (simplest)

This is the most straightforward method and requires no additional tools.

1. Download or clone this repository to your computer.
2. Open a terminal and navigate to the folder where you saved the files. For example:
   ```
   cd /Users/yourname/Downloads/replication
   ```
3. Run whichever script you want:
   ```
   python mc_block_3.py
   ```
   ```
   python mc_block_1.py
   ```
   ```
   python mc_block_2.py
   ```

When the script finishes, it will print a summary to the terminal and save all output files (CSV tables and PDF/PNG figures) into a timestamped folder inside the directory where you ran the script.

> **Note for `mc_block_1.py` and `mc_block_2.py`:** These two scripts were originally developed in Google Colab and contain a path pointing to a Google Drive folder. Before running them locally, open the script in any text editor and change this line near the top:
> ```python
> BASE_OUT_DIR = "/content/drive/MyDrive/vsc_saves"
> ```
> to a folder on your own computer, for example:
> ```python
> BASE_OUT_DIR = "."
> ```
> This makes outputs save to your current folder. `mc_block_3.py` does not require this change.

---

### Option B — Run inside a Jupyter Notebook

If you prefer working in notebooks (`.ipynb` files), you can run these scripts from a notebook cell without converting anything.

1. Install Jupyter if you do not have it:
   ```
   pip install notebook
   ```
2. Launch Jupyter:
   ```
   jupyter notebook
   ```
3. In the browser window that opens, create a new notebook or open an existing one.
4. In a notebook cell, type and run:
   ```python
   %run mc_block_3.py
   ```
   Replace `mc_block_3.py` with whichever script you want. The `%run` command executes the script exactly as if you had run it from the terminal, and all printed output will appear below the cell.

   Alternatively, you can paste the entire contents of a script directly into a notebook cell and run it as normal code.

> **Make sure the script file is in the same folder as your notebook**, or provide the full path:
> ```python
> %run /Users/yourname/Downloads/replication/mc_block_3.py
> ```

---

### Option C — Run in Google Colab (cloud, no local installation needed)

This is useful if you do not want to install anything on your computer.

1. Go to [https://colab.research.google.com](https://colab.research.google.com).
2. Click **File → Upload notebook** and upload any of the scripts, or create a new notebook.
3. In the first cell, mount your Google Drive (optional, but needed to save outputs there):
   ```python
   from google.colab import drive
   drive.mount('/content/drive')
   ```
4. Upload the script file using the file browser on the left sidebar (click the folder icon, then the upload icon).
5. Run the script from a cell:
   ```python
   %run mc_block_1.py
   ```

For `mc_block_1.py` and `mc_block_2.py` the default output path already points to Google Drive (`/content/drive/MyDrive/vsc_saves`), so you do not need to change anything if you have Drive mounted. If you prefer to save locally within Colab, change the path to `"."` as described in Option A.

---

## What the scripts produce

Each script creates a timestamped output folder named `mc_block_X_YYMMDD_HHMM` in the output directory. Inside that folder you will find:

- **CSV files** — the raw simulation results, one row per draw or trajectory, plus summary tables. These are the numbers reported in Section 6.
- **PDF and PNG figures** — the figures that appear in the paper.
- **`config_dump.json`** — the exact configuration used for that run, for full reproducibility.

All results in the paper were produced with the random seeds set in the scripts (`SEED = 20260212` for `mc_block_1` and `mc_block_2`; `SEED = 20260312` for `mc_block_3`). Do not change the seed values if you want to reproduce the exact numbers in the paper.

---

## Expected runtimes

These are approximate times on a standard laptop (2020 or later). All scripts are single-threaded and will not use more than one CPU core.

| Script | Approximate runtime |
|---|---|
| `mc_block_1.py` | 30–90 minutes |
| `mc_block_2.py` | 3–8 hours |
| `mc_block_3.py` | 2–4 hours |

`mc_block_2.py` is the most demanding: it simulates up to 15,750 trajectories, each potentially running for thousands of time steps. `mc_block_3.py` runs a multi-axis numerical sensitivity sweep on top of the core simulation. Plan accordingly — both scripts are safe to leave running overnight.

---

## Changing the number of simulation draws

If you want a faster test run to check that everything is working, you can reduce the number of draws. Open the script in a text editor and find the configuration block near the top. For `mc_block_1.py` and `mc_block_2.py`, change:

```python
"N": 1000
```

to something like:

```python
"N": 50
```

For `mc_block_3.py`, change:

```python
"N_BISTABLE_POOL_TARGET": 600,
"MAX_TRIES": 400000,
```

to:

```python
"N_BISTABLE_POOL_TARGET": 50,
"MAX_TRIES": 10000,
```

The script will finish in seconds but the results will not match the paper.

---

## Troubleshooting

**`ModuleNotFoundError: No module named 'scipy'`** (or numpy, pandas, matplotlib)
Run `pip install numpy pandas matplotlib scipy` and try again.

**`python: command not found`**
Try `python3` instead of `python`. On some systems the command is `python3`.

**The script runs but produces no figures**
Make sure `matplotlib` is installed. Also check that the output folder was created — all files are saved there, not displayed in the terminal.

**`PermissionError` when saving files**
The script does not have write access to the output directory. Either run it from a folder where you have write permissions (your home folder or Desktop always works), or change `BASE_OUT_DIR` in the script to a path you control.

**Outputs look different from the paper**
Make sure you have not changed the `SEED` value in the script. Results are fully reproducible given the same seed and the same package versions. The scripts were developed with NumPy 1.24+, Pandas 1.5+, and SciPy 1.10+.

---

## Citation

If you use this code, please cite the paper:

> Cayirli, O. (2025). Institutional Asymmetry, Endogenous Fragility, and Economic Growth. *Working paper*, Vietnamese-German University.

---

## Contact

omer_cayirli@uncbusiness.net
