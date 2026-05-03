# UK EV Charging Access Segmentation and Rollout Prioritisation

## Project Overview

This project combines official UK data on public EV chargers, plug-in vehicle counts, and local authority population to identify patterns of EV charging access across local authorities.

The goal is to build a local-authority level view of charger supply, EV demand pressure, and relative charging access. Unsupervised learning methods are then used to segment local authorities, compare clustering structures, and identify atypical authorities that may deserve separate review.

## Business Problem

Public EV charger counts alone do not fully describe charging access.

A local authority may appear well served in absolute charger numbers, but still face infrastructure pressure if it also has a high number of plug-in vehicles. At the same time, some areas may look weak in raw charger counts but appear more reasonable after population-based normalisation.

This project addresses that problem by identifying broad EV charging access patterns across UK local authorities and highlighting authorities that behave unusually relative to the dominant national structure.

## Analytical Strategy

This project uses multiple unsupervised learning methods, but they do not all play the same role.

- **Main segmentation method:** PCA followed by K-Means
- **Hierarchical comparison:** Agglomerative Clustering and dendrogram
- **Atypical-authority detection:** DBSCAN
- **Nonlinear visual support:** t-SNE

This keeps the project decision-led rather than method-led. K-Means provides the main segmentation, while the other methods are used to validate, compare, or refine the interpretation.

## Data Sources

The project uses three official UK datasets:

- public EV charger counts by local authority
- licensed plug-in vehicle counts by local authority
- local authority population estimates

These are cleaned and merged into one local-authority level analytical dataset.

## Feature Engineering

The merged dataset was used to create EV charging access-pressure features, including:

- EV chargers per 100,000 population
- fast chargers per 100,000 population
- plug-in vehicles per 100,000 population
- plug-in vehicles per charger
- plug-in vehicles per fast charger
- fast charger share

These features were designed to capture charger availability, EV intensity, supply-demand pressure, and charger mix quality.

## Methods Used

### 1. PCA
PCA was used to reduce redundancy in the engineered EV charging access-pressure feature space.

The first three principal components captured most of the structure in the data and were used for downstream clustering.

### 2. K-Means
K-Means was used as the main segmentation method.

An initial two-cluster solution produced a singleton authority, so that authority was treated separately as atypical. K-Means was then re-run on the remaining authorities, producing the main three-cluster segmentation.

### 3. Agglomerative Clustering
Agglomerative Clustering was applied as a hierarchical comparison method using Ward linkage.

A dendrogram was used to inspect the hierarchical grouping structure and compare it with the K-Means result.

### 4. DBSCAN
DBSCAN was applied as a density-based comparison method.

In this dataset, it was more useful for identifying atypical authorities than for producing broad segmentation groups.

### 5. t-SNE
t-SNE was used as a supporting nonlinear visualisation method to inspect whether the cluster structure and atypical-authority pattern remained visible in a nonlinear embedding.

## Main Findings

The final analysis suggests three broad local-authority EV charging access patterns:

### 1. Charger-Rich Lower-Pressure Authorities
- very high overall charger availability
- low plug-in vehicle pressure per charger
- weaker fast-charger share

### 2. Mainstream Lower-Supply Authorities
- largest authority group
- lower overall provision
- more moderate EV access-pressure conditions

### 3. High-EV High-Pressure Authorities
- highest EV intensity
- highest pressure per charger
- strongest fast-charger presence and fast-charger share

In addition, **Windsor and Maidenhead** emerged as a highly atypical authority and was treated separately rather than forced into the main segmentation.

## Business Interpretation

The results suggest that local authorities should not be treated as a single national charging access pattern.

- **High-EV High-Pressure Authorities** may deserve the strongest rollout attention because infrastructure pressure appears highest there.
- **Mainstream Lower-Supply Authorities** represent the largest broad group and may be suitable for wider medium-term rollout planning.
- **Charger-Rich Lower-Pressure Authorities** appear better served overall, but may still require review of charger mix, especially fast-charger provision.
- **Atypical authorities** should be reviewed separately rather than grouped blindly into mainstream rollout logic.

## Limitations

This project has several important limitations.

- The analysis uses charger counts, plug-in vehicle counts, and population totals, but does not directly observe charger utilisation, queueing, or real-time availability.
- Licensed plug-in vehicle counts are used as a demand-side proxy, but local authority registration totals may not perfectly reflect actual public charging behaviour in all areas.
- Results depend on the engineered feature set and selected clustering parameters.
- The project is a strategic local-authority level analysis and does not include finer-grained charger location, station-level utilisation, or temporal demand variation.

## Repository Contents

- `uk_ev_charging_access_segmentation.ipynb` — main notebook
- `uk_ev_charging_access_segmentation.html` — HTML export of the notebook

## Tools and Libraries

- Python
- pandas
- numpy
- matplotlib
- scikit-learn
- scipy

## Final Conclusion

This project demonstrates a practical unsupervised learning workflow for a real UK infrastructure problem.

By combining official EV charger, plug-in vehicle, and population data, the analysis shows how dimensionality reduction, clustering, hierarchical comparison, density-based outlier detection, and nonlinear visualisation can be used together to build a clearer view of EV charging access patterns across local authorities.

The final result is a portfolio project that combines:
- data cleaning and integration
- feature engineering
- PCA
- clustering comparison
- atypical-authority detection
- business interpretation
- rollout decision-support logic
