# RemoteCLIP Hydrology Baselines  

Supplementary materials for the IEEE ICIP 2026 Satellite Workshop paper:  
**"Weighted Prompt Ensembles for Fine-Grained Zero-Shot Surface-Water Feature Classification in Aerial Images with RemoteCLIP"**

This repository provides all supplementary artifacts required to reproduce the evaluation results, calibration analyses, and prompt‑ensemble ablations reported in the paper and rebuttal. It includes our full hydrology‑aware prompt library, nested five‑fold partitions, TOP‑N summary metrics, and the complete calibration PDF.

---

## 📁 Repository Contents

### 📄 **1. Hydrology_prompt_library.csv**
The full prompt library used for margin‑based scoring and TOP‑N ensembling.  
Contains 15 prompts per class across five surface-water categories:
- Deep Water  
- Turbid Water  
- Rocky Substrate  
- Emergent Vegetation  
- Submerged Aquatic Vegetation (SAV)

Each prompt is annotated with:
- `sensor`: Aerial, National Land Survey (NLS), or both.
- `waterbody_type`: Lake, river, coast, or any.
- `ablation_level`: Simple, hydrology, sensor, context, or full.

---

### 📂 **2. folds/**
Nested five‑fold cross‑validation partitions used to validate the method.  
Each fold contains:
- `train.csv`: Tile IDs used exclusively for prompt scoring, weighting, and Platt calibration.
- `test.csv`: Held‑out tile IDs used strictly for zero‑shot inference.

*Note: These partitions use separate waterbodies across distinct geographic regions to ensure zero spatial autocorrelation leakage.*

---

### 📊 **3. summary_topN_*.json**
Per‑ensemble performance summaries for TOP‑N ∈ {1, 3, 5, 10, 15}.  
Each JSON file includes:
- Accuracy, Macro‑F1, and Weighted‑F1 scores.
- Uncalibrated and Platt‑scaled Brier scores.
- Prompt scoring mode, weighting mode, and temperature.

*These values correspond directly to Table 1 in the paper and supplementary material.*

---

### 📉 **4. Supplementary_Material.pdf**
Contains extended experimental results, figures, and calibration analyses:
- TOP‑N accuracy, macro‑F1, and Brier score trajectory curves.
- Expected Calibration Error (ECE) computations across ensemble sizes.
- Reliability diagrams and fold‑wise confidence intervals.
- Traditional RGB‑only baseline comparisons (NDI, ExG, and RGB turbidity indices).

*Note: All plots and diagrams are embedded inside this PDF; no standalone image files are included.*

---

## 🔁 Operational & Reproducibility Notes

- **Zero Leakage**: Prompt scoring, weighting, and calibration are restricted strictly to training folds.
- **Zero-Shot Test Deployment**: Inference on all held‑out test folds remains entirely zero‑shot using frozen weights.
- **Diagnostic Upper Bound**: The supervised frozen-feature linear probe is included purely as a diagnostic upper bound, not as a competing zero-shot method.
- **RGB Standardization**: Standardizing the dataset into RGB tiles precludes traditional multi-spectral indices (e.g., NDWI). RGB baselines are provided in the PDF to offer standard computer vision benchmarks.

---

## 📄 Citation

If you use this repository or prompt library, please cite our workshop paper:

```bibtex
@inproceedings{shah2026weighted,
  title={Weighted Prompt Ensembles for Fine-Grained Surface-Water Feature Classification with Zero-Shot RemoteCLIP Inference},
  author={Shah, Afifah and Humayun, Muhammad Farhan},
  booktitle={IEEE International Conference on Image Processing (ICIP) Satellite Workshops},
  year={2026}
}
```
