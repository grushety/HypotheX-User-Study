# Metrics used in event flow evaluation

| Metric | Full Name | Bias (Manifestation) | Short Description (Computation) |
|---|---|---|---|
| MPR | Main Profile Reached | Anchoring (Preference for dominant cluster) | Binary indicator (0/1) whether the user selected at least one instance from the largest cluster (KMeans-based) within a class. |
| SubC | Subgroup Coverage | Anchoring (Limited subgroup exploration) | Proportion of subclusters (KMeans) within a class that were interacted with by the user. |
| FRC | Feature Range Coverage | Anchoring (Restricted feature-space exploration) | Normalized min–max coverage of the goal-class feature range explored by the user relative to the full known range. |
| EEC | Early Evaluation Consistency | Availability (Primacy effect) | Agreement between the average outcome of the first 30% of test actions and the final hypothesis rating. |
| LEC | Late Evaluation Consistency | Availability (Recency effect) | Agreement between the average outcome of the last 20% of test actions and the final hypothesis rating. |
| HC | Hypothesis Complexity | Availability (Simplified mental model formation) | Aggregated normalized score combining number of features, thresholds, value ranges, and class references used in a hypothesis. |
| EC | Exploration Complexity | Availability (Breadth of initial exploration) | Number of distinct regions, feature combinations, or classes inspected before finalizing a hypothesis. |
| CHAAR | Confirmed Hypothesis Action Agreement Ratio | Confirmation (Selective supporting evidence use) | Proportion of test actions that support hypotheses the user confirmed. |
| DHAAR | Disproved Hypothesis Action Agreement Ratio | Confirmation (Selective contradiction handling) | Proportion of test actions that contradict hypotheses the user rejected. |


# Anchoring

## MPR / SubC / FRC

### Mean per Tool
| Tool | MPR | SubC | FRC |
|---|---:|---:|---:|
| HypotheX | 0.81 | 0.70 | 0.71 |
| WhatIf | 0.39 | 0.36 | 0.48 |

### Mean per Participant
| Participant | MPR (WIT) | MPR (HX) | SubC (WIT) | SubC (HX) | FRC (WIT) | FRC (HX) |
|---|---:|---:|---:|---:|---:|---:|
| P-djk2vq-9 | 0.00 | 0.75 | 0.20 | 0.56 | 0.21 | 0.55 |
| P-ebx8mj-7 | 0.05 | 0.94 | 0.37 | 0.97 | 0.33 | 0.89 |
| P-hu5tcn-3 | 0.25 | 0.50 | 0.30 | 0.52 | 0.59 | 0.75 |
| P-kpe1cz-10 | 0.75 | 1.00 | 0.60 | 0.95 | 0.65 | 0.86 |
| P-mqv4gh-2 | 0.25 | 1.00 | 0.31 | 0.95 | 0.38 | 0.96 |
| P-pj7twb-5 | 0.58 | 0.75 | 0.27 | 0.61 | 0.47 | 0.54 |
| P-snt3rw-8 | 0.75 | 0.50 | 0.35 | 0.42 | 0.58 | 0.57 |
| P-vr9xmd-4 | 0.83 | 1.00 | 0.48 | 1.00 | 0.66 | 0.91 |
| P-wgr7sa-11 | 0.30 | 1.00 | 0.47 | 0.72 | 0.56 | 0.66 |
| P-zf6uoq-6 | 0.17 | 0.62 | 0.27 | 0.38 | 0.38 | 0.33 |

### Mean per Task
| Task | MPR (WIT) | MPR (HX) | SubC (WIT) | SubC (HX) | FRC (WIT) | FRC (HX) |
|---:|---:|---:|---:|---:|---:|---:|
| 1 | 0.37 | 0.72 | 0.39 | 0.72 | 0.45 | 0.64 |
| 2 | 0.30 | 0.70 | 0.38 | 0.64 | 0.54 | 0.70 |
| 3 | 0.50 | 0.90 | 0.40 | 0.77 | 0.54 | 0.80 |
| 4 | 0.40 | 0.90 | 0.28 | 0.68 | 0.39 | 0.69 |

---

# Availability temporal

## EEC / LEC

### Mean per Tool
| Tool | EEC | LEC |
|---|---:|---:|
| HypotheX | 0.74 | 0.84 |
| WhatIf | 0.78 | 0.88 |

### Mean per Participant
| Participant | EEC (WIT) | EEC (HX) | LEC (WIT) | LEC (HX) |
|---|---:|---:|---:|---:|
| P-bcm4tn-12 | – | 0.76 | – | 0.86 |
| P-djk2vq-9 | 0.63 | 0.88 | 0.93 | 0.90 |
| P-ebx8mj-7 | 0.76 | 0.82 | 0.86 | 0.89 |
| P-hu5tcn-3 | 0.76 | 0.63 | 0.86 | 0.68 |
| P-kpe1cz-10 | 0.92 | 0.63 | 0.89 | 0.71 |
| P-mqv4gh-2 | 0.76 | 0.82 | 0.86 | 0.93 |
| P-pj7twb-5 | 0.91 | 0.69 | 0.84 | 0.87 |
| P-snt3rw-8 | 0.76 | 0.69 | 0.86 | 0.87 |
| P-vr9xmd-4 | 0.76 | 0.76 | 0.93 | 0.86 |
| P-wgr7sa-11 | 0.83 | 0.67 | 0.90 | 0.82 |
| P-zf6uoq-6 | 0.76 | 0.76 | 0.86 | 0.86 |

### Mean per Task
| Task | EEC (WIT) | EEC (HX) | LEC (WIT) | LEC (HX) |
|---:|---:|---:|---:|---:|
| 1 | 0.76 | 0.73 | 0.86 | 0.84 |
| 2 | 0.78 | 0.66 | 0.89 | 0.80 |
| 3 | 0.80 | 0.81 | 0.86 | 0.87 |
| 4 | 0.80 | 0.76 | 0.90 | 0.85 |

---

# Availability spacial

## HC / EC

### Mean per Tool
| Tool | HC | EC |
|---|---:|---:|
| HypotheX | 0.21 | 3.28 |
| WhatIf | 0.20 | 5.88 |

### Mean per Participant
| Participant | HC (WIT) | HC (HX) | EC (WIT) | EC (HX) |
|---|---:|---:|---:|---:|
| P-bcm4tn-12 | – | 0.22 | – | 1.00 |
| P-djk2vq-9 | 0.19 | 0.20 | 6.00 | 2.00 |
| P-ebx8mj-7 | 0.18 | 0.15 | 3.75 | 3.00 |
| P-hu5tcn-3 | 0.26 | 0.23 | 6.75 | 4.25 |
| P-kpe1cz-10 | 0.16 | 0.19 | 3.50 | 3.50 |
| P-mqv4gh-2 | 0.13 | 0.23 | 6.50 | 5.50 |
| P-pj7twb-5 | 0.26 | 0.18 | 6.75 | 3.75 |
| P-snt3rw-8 | 0.25 | 0.25 | 6.75 | 3.00 |
| P-vr9xmd-4 | 0.19 | 0.21 | 6.00 | 2.75 |
| P-wgr7sa-11 | 0.22 | 0.23 | 7.75 | 3.00 |
| P-zf6uoq-6 | 0.14 | 0.27 | 5.00 | 2.50 |

### Mean per Task
| Task | HC (WIT) | HC (HX) | EC (WIT) | EC (HX) |
|---:|---:|---:|---:|---:|
| 1 | 0.20 | 0.22 | 10.0 | 5.8 |
| 2 | 0.18 | 0.18 | 3.8 | 1.3 |
| 3 | 0.21 | 0.23 | 5.2 | 4.1 |
| 4 | 0.19 | 0.22 | 4.5 | 1.9 |

---

# Confirmation

## CHAAR / DHAAR

### Mean per Tool
| Tool | CHAAR | DHAAR |
|---|---:|---:|
| HypotheX | 0.61 | 0.71 |
| WhatIf | 0.61 | 0.71 |

### Mean per Participant
| Participant | CHAAR (WIT) | CHAAR (HX) | DHAAR (WIT) | DHAAR (HX) |
|---|---:|---:|---:|---:|
| P-djk2vq-9 | 0.31 | 0.71 | 0.54 | 0.86 |
| P-ebx8mj-7 | 0.71 | 0.61 | 0.71 | 0.79 |
| P-hu5tcn-3 | 0.61 | 0.71 | 0.71 | 0.54 |
| P-kpe1cz-10 | 0.56 | 0.46 | 0.86 | 0.71 |
| P-mqv4gh-2 | 0.46 | 0.71 | 0.71 | 0.79 |
| P-pj7twb-5 | 0.71 | 0.31 | 0.61 | 0.79 |
| P-snt3rw-8 | 0.61 | 0.81 | 0.71 | 0.71 |
| P-vr9xmd-4 | 0.71 | 0.61 | 0.79 | 0.71 |
| P-wgr7sa-11 | 0.81 | 0.61 | 0.79 | 0.48 |
| P-zf6uoq-6 | 0.61 | 0.61 | 0.71 | 0.71 |

### Mean per Task
| Task | CHAAR (WIT) | CHAAR (HX) | DHAAR (WIT) | DHAAR (HX) |
|---:|---:|---:|---:|---:|
| 1 | 0.57 | 0.61 | 0.77 | 0.71 |
| 2 | 0.61 | 0.55 | 0.73 | 0.67 |
| 3 | 0.53 | 0.69 | 0.64 | 0.67 |
| 4 | 0.73 | 0.61 | 0.71 | 0.80 |



# ANOVA Summary – All Metrics

### 1. F-statistic:

The F-statistic is a measure of the ratio of the variance between groups (e.g., between tools) to the variance within the groups (e.g., within each tool). A higher F-statistic indicates that the groups are more different from each other compared to the variation within the groups.

- **F-statistic > 1**: Suggests that there is variability between groups, which might be statistically significant.
- **F-statistic close to 1**: Suggests that there is little difference between the groups, indicating no significant effect.

### 2. P-value:

The P-value indicates whether the observed differences are statistically significant.

- **P-value < 0.05**: Suggests that the difference between the groups is statistically significant (i.e., there is evidence to reject the null hypothesis that the means of the groups are equal).
- **P-value ≥ 0.05**: Suggests that the difference is not statistically significant (i.e., we fail to reject the null hypothesis).


## One-Way ANOVA (Main Effect of Tool)

| Metric | F-statistic | p-value | Significant |
|---|---:|---:|:---:|
| MPR | 18.510 | <0.001 | Yes |
| SubC | 36.740 | <0.001 | Yes |
| FRC | 13.860 | <0.001 | Yes |
| EEC | 1.451 | 0.232 | No |
| LEC | 1.443 | 0.233 | No |
| HC | 1.517073 | 0.221763 | No |
| EC | 16.999 | <0.001 | Yes |
| CHAAR | 0.01 | 0.916 | No |
| DHAAR | ~0 | 1.000 | No |

---

## Two-Way ANOVA (Tool × Task)

| Metric | F-statistic | p-value | Significant |
|---|---:|---:|:---:|
| MPR | 0.101 | 0.959 | No |
| SubC | 0.265 | 0.850 | No |
| FRC | 0.253 | 0.859 | No |
| EEC | 0.526 | 0.666 | No |
| LEC | 0.354 | 0.786 | No |
| HC | 0.201997 | 0.894686 | No |
| EC | 2.266 | 0.088 | No |
| CHAAR | 1.36 | 0.263 | No |
| DHAAR | 0.66 | 0.578 | No |

---

## Two-Way ANOVA (Tool × Participant)

| Metric | F-statistic | p-value | Significant |
|---|---:|---:|:---:|
| MPR | 1.448 | 0.183 | No |
| SubC | 1.783 | 0.084 | No |
| FRC | 1.535 | 0.150 | No |
| EEC | 1.416 | 0.196 | No |
| LEC | 0.669 | 0.748 | No |
| HC | 2.087488 | 0.039828 | Yes |
| EC | 0.504 | 0.880 | No |
| CHAAR | 2.09 | 0.0397 | Yes |
| DHAAR | 1.66 | 0.111 | No |