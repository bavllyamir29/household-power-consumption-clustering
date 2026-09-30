# Household Power Consumption Clustering

Unsupervised learning project that segments 2M+ household electricity readings into consumption patterns using K-Means, DBSCAN, and PCA.

## Overview

This project analyzes one-minute household electric power consumption data collected over almost four years (Dec 2006 – Nov 2010). Since the dataset has no labels, the goal is to discover natural groupings that reflect different electricity usage behaviors, which can support energy-saving recommendations and demand pattern analysis.

## Dataset

- **Source:** [UCI Machine Learning Repository - Individual Household Electric Power Consumption](https://archive.ics.uci.edu/dataset/235/individual+household+electric+power+consumption)
- **Size:** 2,075,259 readings (2,049,280 after removing missing values)
- **Features:** Global active power, global reactive power, voltage, global intensity, and three sub-metering values (kitchen, laundry room, water-heater/AC)
- **Target:** None (unsupervised learning)

> The dataset file (`household_power_consumption.txt`) is ~127 MB and is not included in this repository. Download it from the link above and place it in the same folder as the notebook.

## Workflow

1. **Data Understanding:** explored the dataset and confirmed the task is clustering
2. **EDA:** histograms, boxplots, correlation heatmap, and time-series plot
3. **Preprocessing:**
   - Converted string columns to numeric and handled missing values (`?`)
   - IQR capping for power, intensity, and voltage features
   - 99th percentile capping for sparse sub-metering features
   - Standardization with `StandardScaler`
4. **Modeling:**
   - K-Means with the Elbow Method and Silhouette Score to choose K
   - DBSCAN for comparison
   - PCA for 2D visualization
5. **Evaluation:** Silhouette Score and cluster interpretation

## Results

| Model | Clusters | Silhouette Score |
|---|---|---|
| **K-Means** | 4 | **0.45** |
| DBSCAN (eps=0.5) | 24 | 0.117 |

K-Means was selected as the final model. DBSCAN failed to produce a meaningful partition because power consumption changes gradually between usage levels, without the clear density gaps DBSCAN needs.

### Discovered Consumption Patterns (K-Means, K=4)

| Cluster | Share of readings | Avg. active power (kW) | Interpretation |
|---|---|---|---|
| 1 | ~60% | 0.43 | Low consumption (idle household) |
| 2 | ~35% | 1.81 | Moderate consumption |
| 0 | ~2.6% | 3.02 | High consumption |
| 3 | ~2.7% | 3.19 | High / peak consumption |

PCA on 2 components captured ~60% of the total variance and was used to visualize the clusters.

## Tools & Libraries

Python, Pandas, NumPy, Scikit-learn, Matplotlib, Seaborn

## How to Run

1. Clone the repository
```bash
   git clone https://github.com/bavllyamir29/household-power-consumption-clustering.git
```
2. Install the requirements
```bash
   pip install pandas numpy matplotlib seaborn scikit-learn
```
3. Download the dataset from the link above and place it next to the notebook
4. Open `household_power_clustering.ipynb` and run all cells

## Author

**Bavlly Amir**, Computer Science student at Ain Shams University
[LinkedIn](https://www.linkedin.com/in/bavlly-amir)
