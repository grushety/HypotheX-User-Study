# Some general tools aspects

### 📊 Cognitive Bias Metrics in HypotheX Evaluation

| **Metric** | **Full Name**                                 | **Bias Targeted** | **Description**                                                                 | **Implementation Details**                                                                 |
|------------|-----------------------------------------------|--------------------|----------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|
| **MPR**    | Main Profile Reached                          | Anchoring (CB1.1)  | Checks if user interacted with the main (largest) cluster of a class.           | KMeans clustering used to find largest cluster; binary flag = 1 if user selected any point from it. |
| **SubC**   | Subgroup Coverage                             | Anchoring (CB1.1)  | Measures how many subclusters of a class the user explored.                     | KMeans used to segment class, proportion of clusters touched is computed.                   |
| **MSelE**  | Multiclass Selection Entropy                  | Anchoring (CB1.1)  | Captures class-level diversity in hypothesis testing.                           | Shannon entropy over non-goal class occurrences in test actions.                           |
| **FRC**    | Feature Range Coverage                        | Anchoring (CB1.2)  | Measures how much of the goal class's feature range is covered.                 | Min-max normalized range explored vs known full class range.                               |
| **FTB**    | Feature Test Balance                          | Anchoring (CB1.2)  | Measures how evenly features are tested.                                        | Entropy over feature usage frequency.                                                       |
| **CII**    | Contradiction Ignoring Index                 | Confirmation (CB2.1) | Degree of mismatch between user's judgment and test results.                    | Distance between participant's declared rating and aggregated test outcomes on a 5-point scale. |
| **CHAAR**  | Confirmed Hypothesis Action Agreement Ratio   | Confirmation (CB2.2) | % of test actions that support a confirmed hypothesis.                          | Proportion of supporting actions among all actions for confirmed hypotheses.                |
| **DHAAR**  | Disproved Hypothesis Action Agreement Ratio   | Confirmation (CB2.2) | % of test actions contradicting a disproved hypothesis.                         | Proportion of contradicting actions for rejected hypotheses.                                |
| **EEC**    | Early Evaluation Consistency                  | Availability (CB3.1) | Agreement between early (first 30%) test outcomes and final judgment.          | Average test score of first 30% vs declared hypothesis rating.                              |
| **LEI**    | Late Evaluation Influence                     | Availability (CB3.1) | Agreement between late (last 20%) test outcomes and final judgment.            | Average of last 20% test actions compared with final hypothesis rating.                     |
| **HC**     | Hypothesis Complexity                         | Availability (CB3.2) | Measures structural richness of user hypotheses.                               | Aggregated normalized scores for feature count, ranges, thresholds, and class mentions.     |


# Anova analysis
### 1. F-statistic:

The F-statistic is a measure of the ratio of the variance between groups (e.g., between tools) to the variance within the groups (e.g., within each tool). A higher F-statistic indicates that the groups are more different from each other compared to the variation within the groups.

- **F-statistic > 1**: Suggests that there is variability between groups, which might be statistically significant.
- **F-statistic close to 1**: Suggests that there is little difference between the groups, indicating no significant effect.

### 2. P-value:

The P-value indicates whether the observed differences are statistically significant.

- **P-value < 0.05**: Suggests that the difference between the groups is statistically significant (i.e., there is evidence to reject the null hypothesis that the means of the groups are equal).
- **P-value ≥ 0.05**: Suggests that the difference is not statistically significant (i.e., we fail to reject the null hypothesis).


# Cognitive Bias & Evaluation Metrics

# Confirmation bias metrics

## Results
### Metrics per task (mean)

| Task Number | CII_wit | CII_HX | CSE_wit | CSE_HX | CHAAR_wit | CHAAR_HX | DHAAR_wit | DHAAR_HX | CER_wit | CER_HX |
|-------------|---------|--------|---------|--------|------------|-----------|------------|-----------|---------|--------|
| 1           | 0.23    | 0.28 ↑ | 0.19    | 0.17 ↓ | 0.49       | 0.58 ↑    | 0.81       | 0.75 ↓    | 0.07    | 0.11 ↑ |
| 2           | 0.21    | 0.34 ↑ | 0.21    | 0.00 ↓ | 0.56       | 0.50 ↓    | 0.72       | 0.69 ↓    | 0.01    | 0.08 ↑ |
| 3           | 0.27    | 0.17 ↓ | 0.35    | 0.00 ↓ | 0.49       | 0.66 ↑    | 0.67       | 0.78 ↑    | 0.09    | 0.02 ↓ |
| 4           | 0.23    | 0.23   | 0.00    | 0.09 ↑ | 0.66       | 0.56 ↓    | 0.75       | 0.83 ↑    | 0.04    | 0.00 ↓ |

### Metrics per participant (mean)

| Participant ID | CII_wit | CII_HX | CSE_wit | CSE_HX | CHAAR_wit | CHAAR_HX | DHAAR_wit | DHAAR_HX | CER_wit | CER_HX |
|----------------|---------|--------|---------|--------|------------|-----------|------------|-----------|---------|--------|
| P-djk2vq-9     | 0.25    | 0.20 ↓ | 0.38    | 0.00 ↓ | 0.28       | 0.67 ↑    | 0.56       | 0.88 ↑    | 0.02    | 0.11 ↑ |
| P-ebx8mj-7     | 0.18    | 0.18   | 0.58    | 0.22 ↓ | 0.67       | 0.56 ↓    | 0.75       | 0.81 ↑    | 0.00    | 0.00   |
| P-hu5tcn-3     | 0.24    | 0.37 ↑ | 0.00    | 0.21 ↑ | 0.56       | 0.67 ↑    | 0.75       | 0.56 ↓    | 0.00    | 0.00   |
| P-kpe1cz-10    | 0.32    | 0.41 ↑ | 0.23    | 0.00 ↓ | 0.53       | 0.42 ↓    | 0.88       | 0.75 ↓    | 0.23    | 0.08 ↓ |
| P-mqv4gh-2     | 0.31    | 0.15 ↓ | 0.00    | 0.00   | 0.42       | 0.67 ↑    | 0.75       | 0.81 ↑    | 0.06    | 0.00 ↓ |
| P-pj7twb-5     | 0.13    | 0.28 ↑ | 0.33    | 0.00 ↓ | 0.67       | 0.28 ↓    | 0.62       | 0.81 ↑    | 0.09    | 0.17 ↑ |
| P-snt3rw-8     | 0.24    | 0.22 ↓ | 0.18    | 0.00 ↓ | 0.56       | 0.78 ↑    | 0.75       | 0.75      | 0.00    | 0.12 ↑ |
| P-vr9xmd-4     | 0.18    | 0.24 ↑ | 0.00    | 0.00   | 0.67       | 0.56 ↓    | 0.81       | 0.75 ↓    | 0.06    | 0.00 ↓ |
| P-zf6uoq-6     | 0.24    | 0.24   | 0.00    | 0.16 ↑ | 0.56       | 0.56      | 0.75       | 0.75      | 0.00    | 0.00   |

### Metrics per tool

| Tool      | CII   | CER   | CHAAR | DHAAR | CSE   |
|-----------|--------|--------|--------|--------|--------|
| HypotheX  | 0.25 ↑ | 0.05   | 0.58 ↑ | 0.76 ↑ | 0.07 ↓ |
| WhatIf    | 0.23   | 0.05   | 0.55   | 0.74   | 0.19   |

## ANOVA Results Summary

### One-Way ANOVA (Main Effect of Tool)

| Metric Name                                   | F-statistic | Statistically Significant? | P-value   | Meaningful? |
|-----------------------------------------------|-------------|-----------------------------|-----------|-------------|
| contradiction_ignoring_index                  | 0.337       | No                          | 0.563     | No          |
| contradictory_evidence_ratio                  | 0.002       | No                          | 0.962     | No          |
| confirmed_hypothesis_action_agreement_ratio   | 0.248       | No                          | 0.620     | No          |
| disproved_hypothesis_action_agreement_ratio   | 0.435       | No                          | 0.512     | No          |
| confirmation_strategy_entropy                 | 3.193       | No                          | 0.078     | No          |

---

###  Two-Way ANOVA (Tool × Task)

| Metric Name                                   | F-statistic | Statistically Significant? | P-value   | Meaningful? |
|-----------------------------------------------|-------------|-----------------------------|-----------|-------------|
| contradiction_ignoring_index                  | 1.564       | No                          | 0.207     | No          |
| contradictory_evidence_ratio                  | 1.216       | No                          | 0.311     | No          |
| confirmed_hypothesis_action_agreement_ratio   | 1.321       | No                          | 0.275     | No          |
| disproved_hypothesis_action_agreement_ratio   | 0.937       | No                          | 0.428     | No          |
| confirmation_strategy_entropy                 | 2.198       | No                          | 0.097     | No          |

---

### Two-Way ANOVA (Tool × Participant)

| Metric Name                                   | F-statistic | Statistically Significant? | P-value   | Meaningful? |
|-----------------------------------------------|-------------|-----------------------------|-----------|-------------|
| contradiction_ignoring_index                  | 0.769       | No                          | 0.632     | No          |
| contradictory_evidence_ratio                  | 1.075       | No                          | 0.394     | No          |
| confirmed_hypothesis_action_agreement_ratio   | 2.313       | **Yes**                     | 0.033     | **Yes**     |
| disproved_hypothesis_action_agreement_ratio   | 1.480       | No                          | 0.186     | No          |
| confirmation_strategy_entropy                 | 1.287       | No                          | 0.270     | No          |



# Anchoring metrics

## Results

### Mean per Task

| Task Number | MPR_wit | MPR_HX | SubC_wit | SubC_HX | CSE_wit | CSE_HX | MSelE_wit | MSelE_HX | FC_wit | FC_HX | FTB_wit | FTB_HX |
|-------------|---------|--------|----------|---------|---------|--------|------------|-----------|--------|--------|----------|--------|
| 1           | 0.39    | 0.69 ↑ | 0.40     | 0.73 ↑  | 0.59    | 0.73 ↑ | 0.92       | 0.78 ↓    | 0.44   | 0.65 ↑ | 1.98     | 1.66 ↓ |
| 2           | 0.33    | 0.67 ↑ | 0.38     | 0.67 ↑  | 0.29    | 0.42 ↑ | 0.77       | 0.87 ↑    | 0.54   | 0.69 ↑ | 0.91     | 1.08 ↑ |
| 3           | 0.44    | 0.89 ↑ | 0.36     | 0.74 ↑  | 0.58    | 0.33 ↓ | 0.69       | 1.02 ↑    | 0.53   | 0.79 ↑ | 1.35     | 1.15 ↓ |
| 4           | 0.44    | 0.89 ↑ | 0.27     | 0.69 ↑  | 0.21    | 0.16 ↓ | 0.64       | 0.60 ↓    | 0.37   | 0.71 ↑ | 1.16     | 1.02 ↓ |


### Mean per Participant

| Participant ID | MPR_wit | MPR_HX | SubC_wit | SubC_HX | CSE_wit | CSE_HX | MSelE_wit | MSelE_HX | FC_wit | FC_HX | FTB_wit | FTB_HX |
|----------------|---------|--------|----------|---------|---------|--------|------------|-----------|--------|--------|----------|--------|
| P-djk2vq-9     | 0.00    | 0.75 ↑ | 0.20     | 0.56 ↑  | 0.50    | 0.45 ↓ | 0.59       | 0.66 ↑    | 0.21   | 0.55 ↑ | 1.19     | 1.32 ↑ |
| P-ebx8mj-7     | 0.05    | 0.94 ↑ | 0.37     | 0.97 ↑  | 0.41    | 0.00 ↓ | 0.68       | 0.95 ↑    | 0.33   | 0.89 ↑ | 1.51     | 0.96 ↓ |
| P-hu5tcn-3     | 0.25    | 0.50 ↑ | 0.30     | 0.52 ↑  | 0.95    | 0.86 ↓ | 1.08       | 1.03 ↓    | 0.59   | 0.75 ↑ | 1.44     | 1.26 ↓ |
| P-kpe1cz-10    | 0.75    | 1.00 ↑ | 0.60     | 0.95 ↑  | 0.16    | 0.44 ↑ | 0.35       | 1.06 ↑    | 0.65   | 0.86 ↑ | 1.35     | 1.36 ↑ |
| P-mqv4gh-2     | 0.25    | 1.00 ↑ | 0.31     | 0.95 ↑  | 0.20    | 0.62 ↑ | 0.48       | 0.79 ↑    | 0.38   | 0.96 ↑ | 1.21     | 1.30 ↑ |
| P-pj7twb-5     | 0.58    | 0.75 ↑ | 0.27     | 0.61 ↑  | 0.48    | 0.69 ↑ | 1.23       | 0.61 ↓    | 0.47   | 0.54 ↑ | 1.51     | 1.18 ↓ |
| P-snt3rw-8     | 0.75    | 0.50 ↓ | 0.35     | 0.42 ↑  | 0.24    | 0.00 ↓ | 0.72       | 0.84 ↑    | 0.58   | 0.57 ↓ | 1.09     | 1.25 ↑ |
| P-vr9xmd-4     | 0.83    | 1.00 ↑ | 0.48     | 1.00 ↑  | 0.64    | 0.00 ↓ | 0.89       | 0.85 ↓    | 0.66   | 0.91 ↑ | 1.52     | 1.23 ↓ |
| P-zf6uoq-6     | 0.17    | 0.62 ↑ | 0.27     | 0.38 ↑  | 0.16    | 0.65 ↑ | 0.77       | 0.58 ↓    | 0.38   | 0.33 ↓ | 1.30     | 1.21 ↓ |

### Mean per Tool

| Tool      | MPR     | SubC    | CSE     | MSelE   | FC      | FTB     |
|-----------|---------|---------|---------|---------|---------|---------|
| HypotheX  | 0.78 ↑  | 0.71 ↑  | 0.41 ↓  | 0.82 ↑  | 0.71 ↑  | 1.23 ↓  |
| WhatIf    | 0.40    | 0.35    | 0.42    | 0.76    | 0.47    | 1.35    |


## ANOVA Results – Strategy and Coverage Metrics



### One-Way ANOVA (Main Effect of Tool)

| Metric Name                              | F-statistic | Statistically Significant? | P-value   | Meaningful? |
|------------------------------------------|-------------|-----------------------------|-----------|-------------|
| class_strategy_entropy                   | 0.001       | No                          | 0.971     | No          |
| feature_test_balance                     | 1.015       | No                          | 0.317     | No          |
| main_profile_reached                     | 13.566      | **Yes**                     | 0.0004498 | **Yes**     |
| subgroup_coverage                        | 36.207      | **Yes**                     | 0.000000073 | **Yes**     |
| multiclass_selection_entropy             | 0.265       | No                          | 0.609     | No          |
| goal_class_feature_range_coverage        | 12.741      | **Yes**                     | 0.0006514 | **Yes**     |


### Two-Way ANOVA (Tool × Task)

| Metric Name                              | F-statistic | Statistically Significant? | P-value   | Meaningful? |
|------------------------------------------|-------------|-----------------------------|-----------|-------------|
| class_strategy_entropy                   | 0.564       | No                          | 0.641     | No          |
| feature_test_balance                     | 1.411       | No                          | 0.248     | No          |
| main_profile_reached                     | 0.122       | No                          | 0.947     | No          |
| subgroup_coverage                        | 0.257       | No                          | 0.856     | No          |
| multiclass_selection_entropy             | 0.704       | No                          | 0.553     | No          |
| goal_class_feature_range_coverage        | 0.331       | No                          | 0.803     | No          |

### Two-Way ANOVA (Tool × Participant)

| Metric Name                              | F-statistic | Statistically Significant? | P-value   | Meaningful? |
|------------------------------------------|-------------|-----------------------------|-----------|-------------|
| class_strategy_entropy                   | 1.180       | No                          | 0.328     | No          |
| feature_test_balance                     | 0.394       | No                          | 0.919     | No          |
| main_profile_reached                     | 1.647       | No                          | 0.133     | No          |
| subgroup_coverage                        | 2.278       | **Yes**                     | 0.035     | **Yes**     |
| multiclass_selection_entropy             | 0.993       | No                          | 0.452     | No          |
| goal_class_feature_range_coverage        | 1.713       | No                          | 0.116     | No          |


# Availability Bias Metrics

## Results

### Mean per task 

| Task Number | HC_wit | HC_HX  | EEC_wit | EEC_HX | LEC_wit | LEC_HX |
|-------------|--------|--------|---------|--------|---------|--------|
| 1           | 0.21   | 0.22 ↑ | 0.75    | 0.73 ↓ | 0.84    | 0.84   |
| 2           | 0.17   | 0.17   | 0.76    | 0.65 ↓ | 0.90    | 0.79 ↓ |
| 3           | 0.20   | 0.23 ↑ | 0.80    | 0.84 ↑ | 0.86    | 0.88 ↑ |
| 4           | 0.19   | 0.22 ↑ | 0.81    | 0.76 ↓ | 0.89    | 0.85 ↓ |

### Mean per participant

| Participant ID | HC_wit | HC_HX | EEC_wit | EEC_HX | LEC_wit | LEC_HX |
|----------------|--------|--------|---------|--------|---------|--------|
| P-djk2vq-9     | 0.19   | 0.20 ↑ | 0.63    | 0.88 ↑ | 0.93    | 0.90 ↓ |
| P-ebx8mj-7     | 0.18   | 0.15 ↓ | 0.76    | 0.82 ↑ | 0.86    | 0.89 ↑ |
| P-hu5tcn-3     | 0.26   | 0.23 ↓ | 0.76    | 0.63 ↓ | 0.86    | 0.68 ↓ |
| P-kpe1cz-10    | 0.16   | 0.19 ↑ | 0.92    | 0.63 ↓ | 0.89    | 0.70 ↓ |
| P-mqv4gh-2     | 0.13   | 0.23 ↑ | 0.76    | 0.82 ↑ | 0.86    | 0.93 ↑ |
| P-pj7twb-5     | 0.26   | 0.18 ↓ | 0.91    | 0.69 ↓ | 0.83    | 0.87 ↑ |
| P-snt3rw-8     | 0.25   | 0.25   | 0.76    | 0.69 ↓ | 0.86    | 0.87 ↑ |
| P-vr9xmd-4     | 0.19   | 0.21 ↑ | 0.76    | 0.76   | 0.93    | 0.86 ↓ |
| P-zf6uoq-6     | 0.14   | 0.27 ↑ | 0.76    | 0.76   | 0.86    | 0.86   |

### Mean per tool
| Tool      | EEC   | LEC   | HC    |
|-----------|-------|-------|-------|
| HypotheX  | 0.74 ↓ | 0.84 ↓ | 0.21 ↑ |
| WhatIf    | 0.78  | 0.87  | 0.19  |


## ANOVA Results – Evaluation and Complexity Metrics

### One-Way ANOVA (Main Effect of Tool)

| Metric Name                     | F-statistic | Statistically Significant? | P-value   | Meaningful? |
|--------------------------------|-------------|-----------------------------|-----------|-------------|
| early_evaluation_consistency   | 0.796       | No                          | 0.375     | No          |
| late_evaluation_influence      | 0.986       | No                          | 0.324     | No          |
| average_hypothesis_complexity  | 1.416       | No                          | 0.238     | No          |

---

### Two-Way ANOVA (Tool × Task)

| Metric Name                     | F-statistic | Statistically Significant? | P-value   | Meaningful? |
|--------------------------------|-------------|-----------------------------|-----------|-------------|
| early_evaluation_consistency   | 0.597       | No                          | 0.620     | No          |
| late_evaluation_influence      | 0.578       | No                          | 0.631     | No          |
| average_hypothesis_complexity  | 0.314       | No                          | 0.815     | No          |

---

### Two-Way ANOVA (Tool × Participant)

| Metric Name                     | F-statistic | Statistically Significant? | P-value   | Meaningful? |
|--------------------------------|-------------|-----------------------------|-----------|-------------|
| early_evaluation_consistency   | 1.640       | No                          | 0.135     | No          |
| late_evaluation_influence      | 0.721       | No                          | 0.672     | No          |
| average_hypothesis_complexity  | 2.426       | **Yes**                     | 0.026     | **Yes**     |

# Additional potentially usefull for evaluation aspects

### Mean per task
| Task Number | HSR_wit | HSR_HX | IBM_R_wit | IBM_R_HX | AvTaskTime_wit | AvTaskTime_HX |
|-------------|---------|--------|------------|-----------|------------------|----------------|
| 1           | 0.48    | 0.64 ↑ | 0.56       | 0.76 ↑    | 20.92            | 18.48 ↓        |
| 2           | 0.09    | 0.06 ↓ | 0.33       | 0.44 ↑    | 4.78             | 4.28 ↓         |
| 3           | 0.30    | 0.50 ↑ | 0.11       | 0.44 ↑    | 9.39             | 6.44 ↓         |
| 4           | 0.51    | 0.18 ↓ | 0.44       | 0.33 ↓    | 5.80             | 5.67 ↓         |

### Mean per participant

| Participant ID | HSR_wit | HSR_HX | IBM_R_wit | IBM_R_HX | AvTaskTime_wit | AvTaskTime_HX |
|----------------|---------|--------|------------|-----------|------------------|----------------|
| P-djk2vq-9     | 0.16    | 0.41 ↑ | 0.00       | 0.86 ↑    | 8.68             | 6.21 ↓         |
| P-ebx8mj-7     | 0.38    | 0.23 ↓ | 0.25       | 0.25      | 11.12            | 7.50 ↓         |
| P-hu5tcn-3     | 0.44    | 0.29 ↓ | 0.50       | 0.11 ↓    | 9.62             | 7.25 ↓         |
| P-kpe1cz-10    | 0.48    | 0.26 ↓ | 0.00       | 0.75 ↑    | 0.00             | 7.12 ↑         |
| P-mqv4gh-2     | 0.38    | 0.40 ↑ | 0.50       | 1.00 ↑    | 10.50            | 12.00 ↑        |
| P-pj7twb-5     | 0.37    | 0.28 ↓ | 0.50       | 0.25 ↓    | 15.00            | 14.50 ↓        |
| P-snt3rw-8     | 0.41    | 0.38 ↓ | 1.00       | 0.75 ↓    | 8.20             | 5.00 ↓         |
| P-vr9xmd-4     | 0.27    | 0.45 ↑ | 0.00       | 0.00      | 16.75            | 12.38 ↓        |
| P-zf6uoq-6     | 0.21    | 0.40 ↑ | 0.50       | 0.50      | 12.12            | 6.50 ↓         |

### Mean per tool
| Tool      | HSR   | AvTaskTime | IBM_R |
|-----------|-------|------------|--------|
| HypotheX  | 0.34   | 8.72 ↓     | 0.50 ↑ |
| WhatIf    | 0.34   | 10.22      | 0.36   |


## ANOVA Results – Interaction Behavior and Task Duration

### One-Way ANOVA (Main Effect of Tool)

| Metric Name                    | F-statistic | Statistically Significant? | P-value   | Meaningful? |
|--------------------------------|-------------|-----------------------------|-----------|-------------|
| inspect_before_modify_ratio    | 1.364       | No                          | 0.247     | No          |
| task_duration_minutes          | 0.578       | No                          | 0.450     | No          |

---

### Two-Way ANOVA (Tool × Task)

| Metric Name                    | F-statistic | Statistically Significant? | P-value   | Meaningful? |
|--------------------------------|-------------|-----------------------------|-----------|-------------|
| inspect_before_modify_ratio    | 0.679       | No                          | 0.568     | No          |
| task_duration_minutes          | 0.245       | No                          | 0.864     | No          |

---

## Two-Way ANOVA (Tool × Participant)

| Metric Name                    | F-statistic | Statistically Significant? | P-value   | Meaningful? |
|--------------------------------|-------------|-----------------------------|-----------|-------------|
| inspect_before_modify_ratio    | 2.458       | **Yes**                     | 0.024     | **Yes**     |
| task_duration_minutes          | 0.416       | No                          | 0.906     | No          |

---
