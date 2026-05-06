```markdown
# Time Series Outlier Detection and Imputation (ETTh1 Dataset)

## Overview
This notebook demonstrates a practical case study for detecting and imputing spike outliers in real-world time series sensor data. It uses the ETTh1 dataset, which consists of hourly oil temperature readings from an electricity transformer, simulating a common scenario of sensor faults.

## Project Goal
The primary goal is to:
1.  Load real industrial sensor data (ETTh1).
2.  Artificially inject spike outliers to simulate sensor errors.
3.  Apply Z-score based methods to detect these outliers.
4.  Compare two common imputation techniques: simple mean imputation and rolling average imputation.
5.  Evaluate the performance of each imputation method using Root Mean Squared Error (RMSE) against the ground truth (original clean data).
6.  Visualize the raw, detected, imputed, and ground truth data for better understanding.

## Dataset
*   **Name**: ETTh1 — Electricity Transformer Temperature
*   **Source**: [github.com/zhouhaoyi/ETDataset](https://github.com/zhouhaoyi/ETDataset/tree/main/ETT-small)
*   **Description**: The `OT` (Oil Temperature) column is used, which represents the primary sensor reading. Other columns are power load features.
*   **Subset Used**: The first 500 hourly records of the `OT` column are used for this demonstration.

## Methodology
1.  **Data Loading**: The ETTh1 dataset is loaded, and a subset of the first 500 `OT` readings is extracted.
2.  **Spike Injection**: 18 synthetic spike outliers are randomly injected into the `Temperature_C` series. These spikes are 4-6 times the maximum normal temperature to simulate significant sensor faults.
3.  **Outlier Detection**: A Z-score method is applied to the noisy data. Points with an absolute Z-score greater than 3 are flagged as outliers.
4.  **Imputation Techniques**:
    *   **Mean Imputation**: Detected outliers are replaced with the mean of the *clean* (non-outlier) data points.
    *   **Rolling Average Imputation**: Detected outliers are replaced with a rolling average (window=10) of the preceding clean data points. This method aims to be more context-aware.
5.  **Evaluation**: Root Mean Squared Error (RMSE) is calculated for both imputation methods by comparing the imputed series against the original, clean `Temperature_C` (ground truth) values.
6.  **Visualization**: A three-panel plot is generated to visualize:
    *   The raw noisy data with detected spikes.
    *   A full comparison of ground truth, mean imputed, and rolling average imputed data.
    *   A zoomed-in view around a detected spike to highlight the behavior of each imputation method.

## Key Findings
*   The Z-score method successfully detected all 18 injected spike outliers.
*   **Rolling Average Imputation** significantly outperformed Mean Imputation in terms of RMSE, demonstrating a closer approximation to the ground truth. It improved accuracy by **52.7%** over Mean imputation in this case.
*   The rolling average method provides a smoother, context-aware estimation, whereas mean imputation results in a flat line at the overall clean mean.

## Generated Files
*   `temperature_outlier_real_ETTh1.png`: A plot visualizing the outlier detection and imputation comparison.
*   `ETTh1_cleaned_output.csv`: A CSV file containing the original timestamp, raw noisy temperature, Z-score, outlier flags, and the cleaned temperature using the superior rolling average imputation.

## How to Run
1.  Open the `.ipynb` file in Google Colab.
2.  Run all cells sequentially. The notebook will automatically download the dataset, perform the analysis, and generate the plots and CSV output.

```
