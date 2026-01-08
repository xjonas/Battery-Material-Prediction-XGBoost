# Band Gap Prediction for Nitride-Based Solid-State Electrolytes

## 1. Background
The development of high-performance solid-state electrolytes is critical for advancing next-generation battery technologies, particularly for applications in electric vehicles. Nitride-based materials, such as Li3N and Mg3N2, represent an underexplored class of potential electrolytes. This is due to their promising ionic conductivity and wide electronic band gaps, which are essential for ensuring electrochemical stability and safety [1]. This project leverages a Gradient Boosting Regressor (XGBoost) to predict the band gaps of nitride-based compounds sourced from the Materials Project database [2]. This project aims to propose a method to identify stable, high-performance electrolyte candidates.

## 2. Implementation
Using the mp-api, the data selection criteria require the presence of nitrogen  
- exclude oxynitrides and thionitrides, therefore no elements S and O
- limit compounds to 2–6 elements with energy above hull ≤0.15 eV for stability
- selected features, adopted from paper Qin et a. (2024) [3], include ```material_id```, ```formula_pretty```, ```band_gap```, ```volume```, ```cbm```, ```density```, ```density_atomic```, ```efermi```, ```energy_above_hull```, ```num_magnetic_sites```, and ```num_unique_magnetic_sites```


## 3. Results
The XGBoost model achieved the following performance metrics:

**Training Set:**
- R^2 = 0.954
- MAE = 0.247 eV
- MSE = 0.118 eV^2

**Test Set:**
- R^2 = 0.865
- MAE = 0.435 eV
- MSE = 0.392 eV^2

The test R^2 of 0.865 represents similar performance to literature [3][4]. Several limitations warrant consideration:
- Dataset size: The 1,671-sample dataset is relatively small compared to recent materials ML studies, potentially limiting generalizability. However, it is easy to expand.
- Feature selection: The eight-feature approach may oversimplify the complex relationships governing band gaps in nitride systems.


## 4. Feature Analysis
SHAP analysis identified feature importance hierarchy:
- Dominant predictor: Fermi energy (efermi)
- Secondary importance: Conduction band minimum (cbm)
- Moderate positive correlation: Density
- Minor contributions: Volume, atomic density, energy above hull
- Negligible influence: Magnetic descriptors

The dominance of electronic descriptors over structural features aligns with fundamental band gap physics. However, the strong reliance on Fermi energy differs from Qin et al.'s findings for silicon oxides, where CBM showed greater prominence [3]. This discrepancy may reflect material-specific electronic structure differences between nitrides and silicon oxides.


## References
1. Li, W., Li, M., Ren, H., Kim, J.T., Li, R., Sham, T.-K. and Sun, X. (2025). Nitride solid-state electrolytes for all-solid-state lithium metal batteries. Energy & Environmental Science. 
‌

2. Jain, A., Ong, S.P., Hautier, G., Chen, W., Richards, W.D., Dacek, S., Cholia, S., Gunter, D., Skinner, D., Ceder, G. and Persson, K.A. (2013). Commentary: The Materials Project: A materials genome approach to accelerating materials innovation. APL Materials, 1(1), p.011002. 
‌

3. Qin, H., Zhang, Y., Guo, Z., Wang, S., Zhao, D. and Xue, Y. (2024). Prediction of Bandgap in Lithium-Ion Battery Materials Based on Explainable Boosting Machine Learning Techniques. Materials, 17(24), pp.6217–6217. 
‌

4. Wang, Y., Lv, J., Zhu, L. and Ma, Y. (2021). Accurate prediction of band gap of materials using stacking machine learning model. Computational Materials Science, 201, p.110899.

