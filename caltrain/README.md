# Mitigating bias in calibration error estimation

Code for the paper: "[Mitigating Bias in Calibration Error Estimation](https://arxiv.org/abs/2012.08668)"


## Setup

### Install dependencies

```bash
virtualenv -p python3 env3
source env3/bin/activate
pip install -r caltrain/requirements.txt
```

### Download data

```bash
source env3/bin/activate
DATA_DIR='./caltrain/data' # This is the default value if omitted below
python -m caltrain.download_data --data_dir=${DATA_DIR}
```

## Running

### Setup

Plots that are generated by each script are saved in a command-line configurable variable `plot_dir=./caltrain/plots` by default. To speed up computation, some values have been precomputed and cached. Each plotting script is configured to read these data from a command-line configurable variable `data_dir='./caltrain/data` by default.  Generating Figure 3 requires downloading logit data from `https://github.com/markus93/NN_calibration/tree/master/logits` into the `data_dir` as well.

The following environment variables should be defined:
```bash
export MPLBACKEND=Agg
```

### Generating figures
```bash
source env3/bin/activate
DATA_DIR='./caltrain/data' # This is the default value if omitted below
PLOT_DIR='./caltrain/plots' # This is the default value if omitted below

# Figure 1 left panel
python -m caltrain.plot_intro_reliability_diagram --plot_dir=${PLOT_DIR}
# Figure 1 right panel
python -m caltrain.plot_intro_ece_distribution --plot_dir=${PLOT_DIR}
# Figure 3 "Curves controlling true calibration error."
python -m caltrain.plot_tce_assumptions --plot_dir=${PLOT_DIR}
# Figure 4 "ECE_bin may underestimate or overestimate TCE."
python -m caltrain.plot_bias_heat_map --data_dir=${DATA_DIR} --plot_dir=${PLOT_DIR}
# Figure 5. "Maximum likehood fits to empirical datasets..."
python -m caltrain.plot_glm_beta_eece_sece --data_dir=${DATA_DIR} --plot_dir=${PLOT_DIR}
# Figure 6. "EMsweep is less biased than alternative calibration metrics."
python -m caltrain.plot_calibration_errors --data_dir=${DATA_DIR} --plot_dir=${PLOT_DIR}
# Figure 7. "Bias in calibration estimation increases as TCE decreases."
python -m caltrain.plot_ece_vs_tce --data_dir=${DATA_DIR} --plot_dir=${PLOT_DIR}
```

## Citing this work

```
@article{roelofs2020mitigating,
  title={Mitigating bias in calibration error estimation},
  author={Roelofs, Rebecca and Cain, Nicholas and Shlens, Jonathon and Mozer, Michael C},
  journal={arXiv preprint arXiv:2012.08668},
  year={2020}
}
```

