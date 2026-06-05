# CLA-DADA

Python implementation of the CLA (Cluster-Based Learning) and DADA (Data-Centric Anomaly Detection) algorithms from:

> G. D'Angelo, A. Castiglione, and F. Palmieri, "A Cluster-Based Multidimensional Approach for Detecting Attacks on Connected Vehicles," *IEEE Internet of Things Journal*, vol. 8, no. 16, pp. 12518–12527, Aug. 2021.

## Requirements

```bash
pip install numpy pandas scikit-learn
```

## Usage

```bash
python cla_dada_faithful.py --train path/to/normal.csv --test path/to/test.csv
```

| Flag | Default | Description |
|------|---------|-------------|
| `--K` | 300 | K-means clusters per CAN ID (paper default) |
| `--nPts` | 30 | k-NN neighbours in DADA (paper default) |
| `--profiles-dir` | `profiles/` | Directory to cache trained CLA profiles |
| `--no-plots` | off | Skip confusion matrix and bar chart output |

### Input format

Required columns: `arbitration_id`, `data0`–`data7`.  
Optional label column (any one): `label` (0/1 or R/T), `Flag`, or `Attack_Type`.  
Byte values may be decimal or hex strings (`0xff`, `ff`).

## results

**SONATA flooding:**
```bash
python cla_dada_faithful.py \
  --train data/FreeDrivingData_20180323_SONATA.csv \
  --test  data/Flooding_dataset_SONATA.csv
```

**GEM-CAN** 
```bash
python cla_dada_faithful.py \
  --train data/GEM_Normal_Driving.csv \
  --test  data/GEM_Attack.csv
```

## Results

| Dataset | Accuracy | Recall | FPR | TP / TN / FP / FN |
|---------|----------|--------|-----|-------------------|
| SONATA  | 95.91%   | 100%   | 5.23% | 32,422 / 111,069 / 6,121 / 0 |
| GEM     | 98.67%   | 100%   | 55.63% | 42,405 / 403 / 578 / 0 |

