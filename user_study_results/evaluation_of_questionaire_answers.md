# Table of Contents

1. [Questionnaire Answer Evaluation](#questionnaire-answer-evaluation)
2. [Answer Encoding](#answer-encoding)
    1. [Class Labels](#class-labels)
    2. [Feature IDs](#feature-ids)
3. [Task 1: Scoring Overview]
    1. [Importance Score Calculation](#1-importance-score-calculation)
    2. [Value Score Calculation](#2-value-score-calculation)
    3. [Profile Match Score](#3-profile-match-score)
    4. [Overall Correctness Score](#4-overall-correctness-score)
4. [Results](#results)
    1. [Metrics Interpretation](#metrics-interpretation)
    2. [Comparison Table (HypotheX vs WhatIf)](#comparison-table-hypothex-vs-whatif)
    3. [Average Scores per Tool](#average-scores-per-tool)
5. [Task 2](#task-2)
6. [Task 3](#task-3)
7. [Task 4](#task-4)

# Questionnaire Answer Evaluation

All responses are encoded and evaluated with the **ground truth**. The encoded file is
`questionaire_answers_encoded.json`. All approaches to calculation are described below.

---

## Answer Encoding

### Class Labels

| ID | Animal Class | Alien Class |
|----|--------------|-------------|
| c1 | Duck         | Zarnak      |
| c2 | Cat          | Bliptor     |
| c3 | Dog          | Quorvian    |

### Feature IDs

| ID | Animal Hobby Feature | Alien Hobby Feature            |
|----|----------------------|--------------------------------|
| f1 | Running              | Laser Pointer Chasing (LPC)    |
| f2 | Swimming             | Reality Show Studies (RSS)     |
| f3 | Art                  | Plant Telepathy Practice (PTP) |
| f4 | Detective Stories    | Box Collecting (BC)            |
| f5 | Gardening            | Tool Worship (TW)              |

---

## Task 1

### 1. **Importance Score Calculation**

- **What it measures**: Compares the **ordered list of features** (importance) selected by the participant with the *
  *ground truth importance list**.
- **How it's computed**:
    - Calculates the **Jaccard index** for **set overlap**.
    - **Penalizes** based on the **incorrect order** of features.
    - Combines the Jaccard index and order penalty.
- **Range**: `0.0` (no match) to `1.0` (perfect match).

### 2. **Value Score Calculation**

- **What it measures**: Compares the **value range** stated by the participant with the **ground truth value range** for
  each feature.
- **How it's computed**:
    - Each participant's stated value range (e.g., "high", "medium-low", "moderate") is mapped to a **numeric range**.
    - The overlap between the **participant's range** and the **ground truth range** is computed using the formula:
        - **Overlap** = `max(start of participant's range, start of truth range)` to
          `min(end of participant's range, end of truth range)`.
    - The final score for each feature is the **normalized overlap** of the stated and ground truth ranges.
- **Range**: `0.0` (no overlap) to `1.0` (perfect match).

### 3. **Profile Match Score**

- **What it measures**: Compares the **profile selected by the participant** (e.g., “Tool-Worship Focused Zarnak”) to
  the **ground truth profile**.
- **How it's computed**:
    - If the selected profile matches the **main profile**, the score is `1.0`.
    - If it matches one of the **subgroup profiles**, the score is `0.5`.
    - Otherwise, the score is `0.0`.
- **Range**: `0.0` (no match) to `1.0` (exact match with the main profile).

### 4. **Overall Correctness Score**

- **What it measures**: Combines the **importance score**, **value score**, and **profile score** into a **single
  combined score**.
- **How it's computed**:
    - The scores are weighted as:
        - **40%** for the importance score,
        - **40%** for the value score,
        - **20%** for the profile score.
    - The overall score is a weighted sum of these three components.

---

### **Scoring Example Calculation (for a participant)**:

1. **Importance Score**:
    - The participant's feature order is compared with the ground truth.
    - If the order is mostly correct, the score might be around `0.7`.

2. **Value Score**:
    - For each feature’s value range, the overlap is computed with the ground truth range.
    - If the ranges align well, the score might be around `0.8`.

3. **Profile Match Score**:
    - If the selected profile matches the **main profile**, the score would be `1.0`.

4. **Overall Score**:
    - Based on the weighted sum of the individual scores.

---

## Results

### **Metrics Interpretation**:

- **`1.0`**: Perfect alignment with ground truth.
- **`0.8`**: Mostly correct with minor discrepancies.
- **`0.5`**: Some alignment, but major mismatches.
- **`<0.5`**: Poor alignment, often unrelated to ground truth.

---

### **Comparison Table** (HypotheX vs WhatIf)


| participant_id | importance_score(WIT) | importance_score(HX)                                      | value_score(WIT) | value_score(HX)                                           | profile_score(WIT) | profile_score(HX)                                         | overall_score (WIT) | overall_score(HX)                                         |
|----------------|-----------------------|-----------------------------------------------------------|------------------|-----------------------------------------------------------|--------------------|-----------------------------------------------------------|---------------------|-----------------------------------------------------------|
| P02            | 0.92                  | 0.66 <span style="color:red; font-size: 20px;">↓</span>   | 0.24             | 0.36 <span style="color:green; font-size: 20px;">↑</span> | 0.50               | 0.50 <span style="color:red; font-size: 20px;">↓</span>   | 0.56                | 0.51 <span style="color:red; font-size: 20px;">↓</span>   |
| P03            | 0.72                  | 0.72 <span style="color:red; font-size: 20px;">↓</span>   | 0.34             | 0.36 <span style="color:green; font-size: 20px;">↑</span> | 0.50               | 0.50 <span style="color:red; font-size: 20px;">↓</span>   | 0.52                | 0.53 <span style="color:green; font-size: 20px;">↑</span> |
| P04            | 0.96                  | 0.66 <span style="color:red; font-size: 20px;">↓</span>   | 0.32             | 0.00 <span style="color:red; font-size: 20px;">↓</span>   | 0.50               | 0.50 <span style="color:red; font-size: 20px;">↓</span>   | 0.61                | 0.36 <span style="color:red; font-size: 20px;">↓</span>   |
| P05            | 0.68                  | 0.80 <span style="color:green; font-size: 20px;">↑</span> | 0.16             | 0.56 <span style="color:green; font-size: 20px;">↑</span> | 0.50               | 1.00 <span style="color:green; font-size: 20px;">↑</span> | 0.44                | 0.74 <span style="color:green; font-size: 20px;">↑</span> |
| P06            | 0.72                  | 0.92 <span style="color:green; font-size: 20px;">↑</span> | 0.36             | 0.52 <span style="color:green; font-size: 20px;">↑</span> | 0.50               | 0.00 <span style="color:red; font-size: 20px;">↓</span>   | 0.53                | 0.58 <span style="color:green; font-size: 20px;">↑</span> |
| P07            | 0.84                  | 0.86 <span style="color:green; font-size: 20px;">↑</span> | 0.00             | 0.16 <span style="color:green; font-size: 20px;">↑</span> | 0.50               | 0.00 <span style="color:red; font-size: 20px;">↓</span>   | 0.44                | 0.41 <span style="color:red; font-size: 20px;">↓</span>   |
| P08            | 0.66                  | 0.70 <span style="color:green; font-size: 20px;">↑</span> | 0.08             | 0.36 <span style="color:green; font-size: 20px;">↑</span> | 0.50               | 1.00 <span style="color:green; font-size: 20px;">↑</span> | 0.40                | 0.62 <span style="color:green; font-size: 20px;">↑</span> |
| P09            | 0.72                  | 0.64 <span style="color:red; font-size: 20px;">↓</span>   | 0.16             | 0.20 <span style="color:green; font-size: 20px;">↑</span> | 0.50               | 0.50 <span style="color:red; font-size: 20px;">↓</span>   | 0.45                | 0.44 <span style="color:red; font-size: 20px;">↓</span>   |
| P10            | 0.92                  | 0.72 <span style="color:red; font-size: 20px;">↓</span>   | 0.42             | 0.46 <span style="color:green; font-size: 20px;">↑</span> | 0.50               | 1.00 <span style="color:green; font-size: 20px;">↑</span> | 0.64                | 0.67 <span style="color:green; font-size: 20px;">↑</span> |
| P11            | 0.72                  | 0.66 <span style="color:red; font-size: 20px;">↓</span>   | 0.16             | 0.36 <span style="color:green; font-size: 20px;">↑</span> | 0.00               | 1.00 <span style="color:green; font-size: 20px;">↑</span> | 0.35                | 0.61 <span style="color:green; font-size: 20px;">↑</span> |
---

## Average Scores per Tool:


| tool     | importance_score | value_score | profile_score | overall_score |
|:---------|-----------------:|------------:|--------------:|--------------:|
| hypothex |            0.734 |       0.334 |          0.60 |         0.547 |
| whatif   |            0.786 |       0.224 |          0.45 |         0.494 |
---

### Task 2

## Score Calculation Methodology

### 1. **Correctness Score Calculation**

The **correctness score** evaluates how well the participant's hypothesis validation aligns with the expected labels.
Each label corresponds to a weight, and the score is calculated by averaging the weights of the labels provided.

- **Labels and Their Weights**:
    - **"refutes_hypothesis"**: 1.0
    - **"works_in_combination"**: 1.0
    - **"weak_influence"**: 1.0
    - **"no_effect"**: 0.75
    - **"ambiguous"**: 0.5

- **How it's computed**:
    - For each participant, the labels from the hypothesis validation are matched with the corresponding weights.
    - The **average weight** of the labels is calculated to produce the final **correctness score**.
    - If no labels are provided, the score is `0.0`.

- **Range**: From `0.0` (no valid labels) to `1.0` (perfect validation alignment).

---

### 2. **Analysis Score Calculation**

The **analysis score** assesses the quality and depth of the participant's evidence supporting their claims. The score
is calculated based on certain evidence criteria.

- **Evidence Criteria**:
    - **"tested_multiple_classes"**: Adds `0.3` to the score.
    - **"tried_disconfirming_cases"**: Adds `0.2` to the score.
    - **"working_combination_found"**: Adds `0.3` to the score.
    - **Reasoning Bonus**: An additional `0.2` is added if any evidence is found.

- **How it's computed**:
    - Each evidence criterion is evaluated. The score is computed by summing the values for the met criteria.
    - The final score is capped at a **maximum of 1.0**.

- **Range**: From `0.0` (no evidence or minimal analysis) to `1.0` (full evidence with reasoning bonus).

---

### 3. **Final Score Calculation**

The **final score** is a weighted sum of the **correctness score** and **analysis score**.

- **How it's computed**:
    - The **correctness score** contributes **40%** to the final score.
    - The **analysis score** contributes **60%** to the final score.
    - The final score is calculated as:
      ```plaintext
      final_score = 0.4 * correctness_score + 0.6 * analysis_score
      ```

- **Range**: From `0.0` (no correctness or analysis) to `1.0` (perfect correctness and analysis).

## Results

### **Comparison Table** (HypotheX vs WhatIf)


| participant_id | correctness_score_whatif | correctness_score_hypothex                               | analysis_score_whatif | analysis_score_hypothex                                  | final_score_whatif | final_score_hypothex                                     |
|----------------|--------------------------|----------------------------------------------------------|-----------------------|----------------------------------------------------------|--------------------|----------------------------------------------------------|
| P02            | 1.00                     | 0.88 <span style="color:red;font-size: 20px;">↓</span>   | 0.40                  | 0.70 <span style="color:green;font-size: 20px;">↑</span> | 0.64               | 0.77 <span style="color:green;font-size: 20px;">↑</span> |
| P03            | 1.00                     | 0.88 <span style="color:red;font-size: 20px;">↓</span>   | 0.50                  | 0.70 <span style="color:green;font-size: 20px;">↑</span> | 0.70               | 0.77 <span style="color:green;font-size: 20px;">↑</span> |
| P04            | 0.88                     | 0.50 <span style="color:red;font-size: 20px;">↓</span>   | 0.00                  | 0.50 <span style="color:green;font-size: 20px;">↑</span> | 0.35               | 0.50 <span style="color:green;font-size: 20px;">↑</span> |
| P05            | 1.00                     | 1.00 <span style="color:gray;font-size: 20px;">=</span>  | 0.70                  | 0.70 <span style="color:gray;font-size: 20px;">=</span>  | 0.82               | 0.82 <span style="color:gray;font-size: 20px;">=</span>  |
| P06            | 0.75                     | 1.00 <span style="color:green;font-size: 20px;">↑</span> | 0.00                  | 0.70 <span style="color:green;font-size: 20px;">↑</span> | 0.30               | 0.82 <span style="color:green;font-size: 20px;">↑</span> |
| P07            | 1.00                     | 1.00 <span style="color:gray;font-size: 20px;">=</span>  | 0.40                  | 0.00 <span style="color:red;font-size: 20px;">↓</span>   | 0.64               | 0.40 <span style="color:red;font-size: 20px;">↓</span>   |
| P08            | 1.00                     | 0.88 <span style="color:red;font-size: 20px;">↓</span>   | 0.00                  | 0.40 <span style="color:green;font-size: 20px;">↑</span> | 0.40               | 0.59 <span style="color:green;font-size: 20px;">↑</span> |
| P09            | 1.00                     | 1.00 <span style="color:gray;font-size: 20px;">=</span>  | 0.00                  | 0.00 <span style="color:gray;font-size: 20px;">=</span>  | 0.40               | 0.40 <span style="color:gray;font-size: 20px;">=</span>  |
| P10            | 1.00                     | 0.88 <span style="color:red;font-size: 20px;">↓</span>   | 0.80                  | 0.70 <span style="color:red;font-size: 20px;">↓</span>   | 0.88               | 0.77 <span style="color:red;font-size: 20px;">↓</span>   |
| P11            | 1.00                     | 0.88 <span style="color:red;font-size: 20px;">↓</span>   | 0.80                  | 0.50 <span style="color:red;font-size: 20px;">↓</span>   | 0.88               | 0.65 <span style="color:red;font-size: 20px;">↓</span>   |
## Average Scores per Tool:


| tool     | correctness_score | analysis_score | final_score |
|----------|-------------------|----------------|-------------|
| hypothex | 0.890             | 0.49           | 0.649       |
| whatif   | 0.963             | 0.36           | 0.601       |
### Task 3

### **1. Complexity Evaluation**

The **complexity** of a hypothesis is evaluated based on the following factors:

- **Number of Features**: More features increase complexity.
- **Number of Boundary Values**: Boundary conditions (e.g., `>5`, `<4`) raise complexity.
- **Number of Ranges Involved**: More ranges (e.g., low, medium, high) increase complexity.
- **Number of Classes**: More classes in the hypothesis increase complexity.

**Complexity Levels**:

- **Low Complexity**: `0 - 0.33`
- **Moderate Complexity**: `0.33 - 0.66`
- **High Complexity**: `0.66 - 1`

**Formula for Complexity Calculation**:

```
Complexity Score = (0.4 × Boundary) + (0.3 × Range) + (0.2 × Features) + (0.1 × Classes)
```

---

### **2. Correctness Evaluation**

The **correctness** of a hypothesis is evaluated by comparing the **ground truth** evaluation with the **participant's
evaluation**. A **discrepancy score** is calculated using:

**Ground Truth vs. Participant Evaluation**:

- **Confirmed** = 0
- **Weakly Confirmed** = 0.25
- **Partially Disproved** = 0.5
- **Weakly Disproved** = 0.75
- **Disproved** = 1

**Discrepancy Score**:

```
Correctness Score = 1 - | Ground Truth Value - Participant Evaluation Value |
```

---

### **3. Final Score Calculation**

The **final score** combines both **complexity** and **correctness**:

```
Final Score = (0.4 × Normalized Complexity) + (0.6 × Correctness Score)
```

Where:

- **Normalized Complexity Score** is based on the weighted sum of features, boundary values, ranges, and classes.
- **Correctness Score** is based on the discrepancy between the ground truth and participant's evaluation.

---

### **4. Final Report**

The final report includes:

- **Complexity Score**: **Low**, **Moderate**, or **High**.
- **Correctness Score**: A value between **0** and **1**.
- **Final Score**: A combined score based on **complexity** and **correctness**.

## Comparison of WIT and HypotheX Scores


| participant_id | complexity_score (WIT) | complexity_score (HX)                        | correctness_score (WIT) | correctness_score (HX)                   | overall_score (WIT) | overall_score (HX)                           |
| -------------- | ---------------------- | -------------------------------------------- | ----------------------- | ---------------------------------------- | ------------------- | -------------------------------------------- |
| P02            | 0.350877               | 0.921053 <span style="color:green; font-size: 20px;">↑</span> | 0.50                    | 1.00 <span style="color:green; font-size: 20px;">↑</span> | 0.440351            | 0.968421 <span style="color:green; font-size: 20px;">↑</span> |
| P03            | 0.570175               | 0.570175 <span style="color:gray; font-size: 20px;">=</span>  | 1.00                    | 1.00 <span style="color:gray; font-size: 20px;">=</span>  | 0.828070            | 0.828070 <span style="color:gray; font-size: 20px;">=</span>  |
| P04            | 0.263158               | 0.482456 <span style="color:green; font-size: 20px;">↑</span> | 0.25                    | 1.00 <span style="color:green; font-size: 20px;">↑</span> | 0.255263            | 0.792982 <span style="color:green; font-size: 20px;">↑</span> |
| P05            | 0.263158               | 0.482456 <span style="color:green; font-size: 20px;">↑</span> | 1.00                    | 1.00 <span style="color:gray; font-size: 20px;">=</span>  | 0.705263            | 0.792982 <span style="color:green; font-size: 20px;">↑</span> |
| P06            | 0.570175               | 0.482456 <span style="color:red; font-size: 20px;">↓</span>   | 0.75                    | 0.75 <span style="color:gray; font-size: 20px;">=</span>  | 0.678070            | 0.642982 <span style="color:red; font-size: 20px;">↓</span>   |
| P07            | 0.263158               | 0.263158 <span style="color:gray; font-size: 20px;">=</span>  | 0.75                    | 1.00 <span style="color:green; font-size: 20px;">↑</span> | 0.555263            | 0.705263 <span style="color:green; font-size: 20px;">↑</span> |
| P08            | 0.482456               | 0.482456 <span style="color:gray; font-size: 20px;">=</span>  | 0.25                    | 0.75 <span style="color:green; font-size: 20px;">↑</span> | 0.342982            | 0.642982 <span style="color:green; font-size: 20px;">↑</span> |
| P09            | 0.482456               | 0.482456 <span style="color:gray; font-size: 20px;">=</span>  | 1.00                    | 1.00 <span style="color:gray; font-size: 20px;">=</span>  | 0.792982            | 0.792982 <span style="color:gray; font-size: 20px;">=</span>  |
| P10            | 0.833333               | 0.263158 <span style="color:red; font-size: 20px;">↓</span>   | 0.75                    | 0.75 <span style="color:gray; font-size: 20px;">=</span>  | 0.783333            | 0.555263 <span style="color:red; font-size: 20px;">↓</span>   |
| P11            | 0.833333               | 0.833333 <span style="color:gray; font-size: 20px;">=</span>  | 0.50                    | 1.00 <span style="color:green; font-size: 20px;">↑</span> | 0.633333            | 0.933333 <span style="color:green; font-size: 20px;">↑</span> |
## Comparison of WIT and HypotheX Scores


| Tool         | Correctness Score | Complexity Score | Overall Score |
| ------------ | ----------------: | ---------------: | ------------: |
| **HypotheX** |         **0.925** |        **0.526** |     **0.766** |
| WhatIf       |             0.675 |            0.491 |         0.601 |
### Task 4

## Comparison of WIT and HypotheX Scores (Task 4)

| participant_id | complexity_score (WIT) | complexity_score (HX)                        | correctness_score (WIT) | correctness_score (HX)                   | overall_score (WIT) | overall_score (HX)                           |
| -------------- | ---------------------- | -------------------------------------------- | ----------------------- | ---------------------------------------- | ------------------- | -------------------------------------------- |
| P02            | 0.350877               | 0.482456 <span style="color:green; font-size: 20px;">↑</span> | 0.25                    | 1.00 <span style="color:green; font-size: 20px;">↑</span> | 0.290351            | 0.792982 <span style="color:green; font-size: 20px;">↑</span> |
| P03            | 0.482456               | 0.394737 <span style="color:red; font-size: 20px;">↓</span>   | 1.00                    | 1.00 <span style="color:gray; font-size: 20px;">=</span>  | 0.792982            | 0.757895 <span style="color:red; font-size: 20px;">↓</span>   |
| P04            | 0.263158               | 0.482456 <span style="color:green; font-size: 20px;">↑</span> | 1.00                    | 0.75 <span style="color:red; font-size: 20px;">↓</span>   | 0.705263            | 0.642982 <span style="color:red; font-size: 20px;">↓</span>   |
| P05            | 0.921053               | 0.263158 <span style="color:red; font-size: 20px;">↓</span>   | 0.75                    | 0.50 <span style="color:red; font-size: 20px;">↓</span>   | 0.818421            | 0.405263 <span style="color:red; font-size: 20px;">↓</span>   |
| P06            | 0.526316               | 0.263158 <span style="color:red; font-size: 20px;">↓</span>   | 0.50                    | 0.00 <span style="color:red; font-size: 20px;">↓</span>   | 0.510526            | 0.105263 <span style="color:red; font-size: 20px;">↓</span>   |
| P07            | 0.263158               | 0.263158 <span style="color:gray; font-size: 20px;">=</span>  | 0.75                    | 1.00 <span style="color:green; font-size: 20px;">↑</span> | 0.555263            | 0.705263 <span style="color:green; font-size: 20px;">↑</span> |
| P08            | 0.438596               | 0.570175 <span style="color:green; font-size: 20px;">↑</span> | 1.00                    | 0.75 <span style="color:red; font-size: 20px;">↓</span>   | 0.775439            | 0.678070 <span style="color:red; font-size: 20px;">↓</span>   |
| P09            | 0.833333               | 0.482456 <span style="color:red; font-size: 20px;">↓</span>   | 1.00                    | 1.00 <span style="color:gray; font-size: 20px;">=</span>  | 0.933333            | 0.792982 <span style="color:red; font-size: 20px;">↓</span>   |
| P10            | 0.833333               | 0.833333 <span style="color:gray; font-size: 20px;">=</span>  | 1.00                    | 1.00 <span style="color:gray; font-size: 20px;">=</span>  | 0.933333            | 0.933333 <span style="color:gray; font-size: 20px;">=</span>  |
| P11            | 0.526316               | 0.482456 <span style="color:red; font-size: 20px;">↓</span>   | 1.00                    | 0.75 <span style="color:red; font-size: 20px;">↓</span>   | 0.810526            | 0.642982 <span style="color:red; font-size: 20px;">↓</span>   |
## 📊 Average Scores per Tool (Task 4)

| Tool     | Correctness Score | Complexity Score | Overall Score |
| -------- | ----------------: | ---------------: | ------------: |
| HypotheX |             0.775 |            0.452 |         0.646 |
| WhatIf   |             0.825 |            0.544 |         0.713 |

# Self evaluation block

## Row answers

| Participant | Part | Self-Eval Before | Score (out of 2) | Self-Eval After |
|-------------|------|------------------|------------------|-----------------|
| P2 (WIT)    | 1    | 5                | 1                | 2               |
| P2 (HX)     | 2    | 4                | 1                | 2               |
| P3 (WIT)    | 1    | 4                | 2                | 4               |
| P3 (HX)     | 2    | 3                | 1                | 2               |
| P4 (WIT)    | 1    | 3                | 1                | 3               |
| P4 (HX)     | 2    | 3                | 1                | 3               |
| P5 (WIT)    | 1    | 2                | 1                | 2               |
| P5 (HX)     | 2    | 2                | 1                | 2               |
| P6 (WIT)    | 1    | 4                | 1                | 4               |
| P6 (HX)     | 2    | 3                | 1                | 4               |
| P7 (WIT)    | 1    | 2                | 1                | 2               |
| P7 (HX)     | 2    | 3                | 2                | 3               |
| P8 (WIT)    | 1    | 3                | 1                | 2               |
| P8 (HX)     | 2    | 3                | 0                | 2               |
| P9 (WIT)    | 1    | 3                | 1                | 4               |
| P9 (HX)     | 2    | 4                | 2                | 4               |
| P10 (WIT)   | 1    | 3                | 1                | 2               |
| P10 (HX)    | 2    | 4                | 0                | 2               |
| P11 (WIT)   | 1    | 2                | 1                | 3               |
| P11 (HX)    | 2    | 3                | 2                | 4               |

## Approach to analysis

To assess how participants interpret and reflect on their understanding of the model during interaction, we draw on
prior work on the Illusion of Explanatory Depth (IOED). This phenomenon describes how individuals often overestimate
their understanding of complex systems, especially after
limited exposure.
Inspired by classic experimental designs (Rozenblit & Keil, 2002; Fisher & Keil, 2014), we designed several quantitative
metrics to capture confidence dynamics in the context of prediction tasks (predict the class based on features values
like the model would).
Participants rated their subjective understanding both before (pre) and after (post) completing the prediction task. We
then computed the following metrics:

### 1. Persistence_Score – Show if confidence changed (increased or dropped) after the task

``` Persistence_Score = Pre_norm - Post_norm  ```

- **Motivation:**  
  Captures the **raw drop in confidence** across the task. A higher Persistence_Score suggests the participant
  recognized the limits of their understanding after engaging with the task — a signature of *reflective thinking*.

- **Calculation details:**  
  Pre- / post-values were normalized from a 1–5 Likert scale to a 0–1 scale using:
  ```Normalized = (Likert - 1) / 4 ```

### 2. PreCONFvsACC / PostCONFvsACC – Confidence–Accuracy Gap

- **Definitions:**  
  ``` PreCONFvsACC = Pre_norm - Accuracy```
  ``` PostCONFvsACC = Post_norm - Accuracy```
- 
- **Interpretation:**  
- close to 0 → confidence aligned with accuracy
- far from 0 → confidence misaligned with accuracy
- positive → overconfidence
- negative → underconfidence
- 
- **Motivation:**  
  Measures the gap between subjective understanding and objective correctness, before and after task completion.
- High values of `PreCONFvsACC` may indicate **overconfidence** after limited exposure to the model
- High values of `PostCONFvsACC` may indicate persistence of **overconfidence** even after performance feedback
- Low or negative values may indicate **underconfidence** or *metacognitive caution*

---

### 3. AdjustmentScore (Rozenblit-style normalized drop)

- **Definition:**  
  ```AdjustmentScore = Persistence_Score / (1 - Accuracy) # if Accuracy < 1```

- **Motivation:**  
  Follows the original IOED framework: if a participant was wrong, did they adjust their confidence accordingly? Higher
  values reflect stronger adjustment in response to failure.

- **Limitation:**  
  This metric becomes undefined when `Accuracy = 1`. We include it for comparability with prior work but prefer a more
  general form below.

---

### 4. AS_final – Confidence Adjustment Score (Final Version)

- **Definition:**
  ```AS_final = (Pre_norm - Post_norm) * (1 - abs(Accuracy - 1))```


- **Motivation:**  
  A more robust and continuous measure of confidence adjustment that:
- Rewards confidence reduction when performance was poor
- Downweights changes when performance was perfect
- Still captures learning-related confidence gains when accuracy is high

- **Interpretation:**
- Positive → adjusted appropriately downward
- Zero → no change or high accuracy with stable confidence
- Negative → increased confidence despite low accuracy (overconfidence)

---

### 5. Confidence Behavior Label

- **Definition:**  
  A categorical label derived from `Persistence_Score` and `Accuracy`.

- **Possible Labels:**
- `reflective`: confidence dropped appropriately after low accuracy (`Persistence_Score > 0.2` **and** `accuracy < 0.7`)
- `overconfident`: confidence stayed the same or rose despite poor performance (`Persistence_Score ≤ 0.0` **and**
  `accuracy < 0.7` )
- `underconfident`: confidence dropped unnecessarily after high accuracy (`Persistence_Score < -0.2` **and** `accuracy ≥ 0.9` )
- `calibrated`: small change with high performance (`|Persistence_Score| < 0.1` **and** `accuracy ≥ 0.9`)
- `adequat`: persistence score = 
- `neutral`: none of the above (All other cases)

- **Motivation:**  
  To support group-wise or behavioral-type comparisons in following analysis.

### All IOED Metrics Results


| participant_id | IPS (WIT) | IPS (HX) | AS_final (WIT) | AS_final (HX) | Accuracy (WIT) | Accuracy (HX) | IOED Label (WIT) | IOED Label (HX) |
| -------------- | --------- | -------- | -------------- | ------------- | -------------- | ------------- | ---------------- | --------------- |
| P02            | 0.75      | 0.50     | 0.38           | 0.25          | 0.50           | 0.50          | Reflective       | Reflective      |
| P03            | 0.00      | 0.25     | 0.00           | 0.13          | 1.00           | 0.50          | Calibrated       | Neutral         |
| P04            | 0.00      | 0.00     | 0.00           | 0.00          | 0.50           | 0.50          | Overconfident    | Overconfident   |
| P05            | 0.00      | 0.00     | 0.00           | 0.00          | 0.50           | 0.50          | Overconfident    | Overconfident   |
| P06            | 0.00      | âˆ’0.25    | 0.00           | âˆ’0.13         | 0.50           | 0.50          | Overconfident    | Overconfident   |
| P07            | 0.00      | 0.00     | 0.00           | 0.00          | 0.50           | 1.00          | Overconfident    | Calibrated      |
| P08            | 0.25      | 0.25     | 0.13           | 0.00          | 0.50           | 0.00          | Neutral          | Overconfident   |
| P09            | âˆ’0.25     | 0.00     | âˆ’0.13          | 0.00          | 0.50           | 1.00          | Overconfident    | Calibrated      |
| P10            | 0.25      | 0.50     | 0.13           | 0.00          | 0.50           | 0.00          | Neutral          | Overconfident   |
| P11            | âˆ’0.25     | âˆ’0.25    | âˆ’0.13          | âˆ’0.25         | 0.50           | 1.00          | Overconfident    | Underconfident  |
### Average IOED Metrics Per Tool


| Tool     | Pre | Post | Accuracy | IPS  | Preâ€“UvA | Postâ€“UvA | AS (orig.) | AS-final |
| -------- | --- | ---- | -------- | ---- | ------- | -------- | ---------- | -------- |
| HypotheX | 3.2 | 2.8  | 0.55     | 0.10 | 0.00    | âˆ’0.10    | 0.25       | 0.00     |
| WhatIf   | 3.1 | 2.8  | 0.55     | 0.08 | âˆ’0.03   | âˆ’0.10    | 0.17       | 0.04     |
### Average IOED Metrics Per Participant


| Participant | Pre | Post | Accuracy | Pre-Norm | Post-Norm |       IPS | Preâ€“UvA | Postâ€“UvA | AS (orig.) |  AS-final |
| ----------- | --: | ---: | -------: | -------: | --------: | --------: | ------: | -------: | ---------: | --------: |
| **P02**     | 4.5 |  2.0 |     0.50 |     0.88 |      0.25 |  **0.63** |    0.38 |    âˆ’0.25 |       1.25 |  **0.31** |
| **P03**     | 3.5 |  3.0 |     0.75 |     0.63 |      0.50 |      0.13 |   âˆ’0.13 |    âˆ’0.25 |       0.50 |      0.06 |
| **P04**     | 3.0 |  3.0 |     0.50 |     0.50 |      0.50 |      0.00 |    0.00 |     0.00 |       0.00 |      0.00 |
| **P05**     | 2.0 |  2.0 |     0.50 |     0.25 |      0.25 |      0.00 |   âˆ’0.25 |    âˆ’0.25 |       0.00 |      0.00 |
| **P06**     | 3.5 |  4.0 |     0.50 |     0.63 |      0.75 |     âˆ’0.13 |    0.13 |     0.25 |      âˆ’0.25 |     âˆ’0.06 |
| **P07**     | 2.5 |  2.5 |     0.75 |     0.38 |      0.38 |      0.00 |   âˆ’0.38 |    âˆ’0.38 |       0.00 |      0.00 |
| **P08**     | 3.0 |  2.0 |     0.25 |     0.50 |      0.25 |      0.25 |    0.25 |     0.00 |       0.38 |      0.06 |
| **P09**     | 3.5 |  4.0 |     0.75 |     0.63 |      0.75 |     âˆ’0.13 |   âˆ’0.13 |     0.00 |      âˆ’0.50 |     âˆ’0.06 |
| **P10**     | 3.5 |  2.0 |     0.25 |     0.63 |      0.25 |  **0.38** |    0.38 |     0.00 |       0.50 |      0.06 |
| **P11**     | 2.5 |  3.5 |     0.75 |     0.38 |      0.63 | **âˆ’0.25** |   âˆ’0.38 |    âˆ’0.13 |      âˆ’0.50 | **âˆ’0.19** |
### One-Way ANOVA Results for IOED Metrics


| Metric              | F(dfâ‚, dfâ‚‚)    | p-value   | Significance      | Interpretation                                         |
| ------------------- | -------------- | --------- | ----------------- | ------------------------------------------------------ |
| **IPS**             | F(9,10) = 8.91 | **0.001** | âœ… Significant     | Strong individual differences in illusion reduction    |
| **PreUvA**          | F(9,10) = 2.74 | 0.066     | âš ï¸ Trend          | Weak differences in pre-task miscalibration            |
| **PostUvA**         | F(9,10) = 1.56 | 0.250     | âŒ Not significant | Post-task calibration converges                        |
| **AdjustmentScore** | F(9,6) = 9.77  | **0.006** | âœ… Significant     | Strong individual differences in confidence adjustment |
| **AS_final**        | F(9,10) = 6.05 | **0.005** | âœ… Significant     | Robust participant-specific adjustment patterns        |
### IOED Analysis

The most important value for our analysis is the **PreCONFvsACC**, which reflects the discrepancy between the user's 
perceived and actual model understanding after using different tool.

## Individual-Level Interpretation (label based)


| Participant | HypotheX Label  | WhatIf Label  | Notes                                            |
|-------------|-----------------|---------------|--------------------------------------------------|
| P02         | reflective      | reflective    | Consistent reflective behavior                   |
| P03         | neutral         | calibrated    | Slight shift toward better calibration in WhatIf |
| P04         | overconfident   | overconfident | Consistently overconfident                       |
| P05         | overconfident   | overconfident | Consistently overconfident                       |
| P06         | overconfident   | overconfident | Consistently overconfident                       |
| P07         | calibrated      | overconfident | Better adjusted confidence in HypotheX           |
| P08         | overconfident   | neutral       | Better adjusted confidence in WhatIf             |
| P09         | calibrated      | overconfident | Better adjusted confidence in HypotheX           |
| P10         | overconfident   | neutral       | Better adjusted confidence in WhatIf             |
| P11         | underconfident  | overconfident | Shift toward underconfidence in HypotheX         |
Across participants, **6 out of 10** showed **different confidence adjustment styles depending on the tool**, while only
**4 participants** behaved consistently across HypotheX and WhatIf.

> **This suggests that the interface had a measurable effect** on interpretive confidence for the majority of
> participants.
However, the **direction of that effect was not consistent**:

- For some (e.g., P08, P10), **WhatIf** supported better calibration (i.e., reduced overconfidence).
- For others (e.g., P07, P09), **HypotheX** appeared to foster more reflective or cautious adjustment.

While interface differences clearly influenced user behavior, there is **no single direction of benefit** attributable
to one tool. Instead, this variation may reflect interaction effects between **individual reasoning style** and *
*specific interface features**.
This reinforces our broader claim that explanation use is shaped by **cognitively situated reasoning**, where both *
*user traits** and **interface design** interact — but **neither dominates universally**.

## Tool-Level Averages


| Metric            | HypotheX | WhatIf | Interpretation                                                  |
|-------------------|----------|--------|-----------------------------------------------------------------|
| Accuracy          | 0.55     | 0.55   | Equal explanation task performance                              |
| PreCONFvsACC      | 0.00     | -0.03  | Slight overconfidence in WhatIf users pre-task                  |
| Persistence_Score | 0.10     | 0.08   | HypotheX show slightly more tendency to **reflective thinking** |
| AS_final          | 0.00     | 0.04   |                                                                 |
**Conclusion**: The two tools led to **broadly similar interpretive patterns** with minor differences.

---

## One-Way ANOVA Results Summary

### Grouped by Tool

| Metric            | F-value | p-value | Significance |
|-------------------|---------|---------|--------------|
| AS_final          | 0.367   | 0.552   | ❌            |
| AdjustmentScore   | 0.088   | 0.772   | ❌            |
| Persistence_Score | 0.040   | 0.844   | ❌            |
| PreCONFvsACC      | 0.027   | 0.870   | ❌            |
| PostCONFvsACC     | ~0      | 1.000   | ❌            |

**Interpretation**: No statistically significant differences between tools. Behavioral differences in confidence and
understanding are **not tool-driven**.

---

### Grouped by Participant

| Metric            | F-value | p-value | Significance      |
|-------------------|---------|---------|-------------------|
| Persistence_Score | 8.911   | 0.001   | ✅ Strong effect   |
| AS_final          | 6.048   | 0.0048  | ✅ Significant     |
| AdjustmentScore   | 9.769   | 0.0059  | ✅ Significant     |
| PreCONFvsACC      | 2.743   | 0.066   | Marginal trend    |
| PostCONFvsACC     | 1.556   | 0.250   | ❌ Not significant |

**Interpretation**: **Participant identity has a significant impact** on confidence behavior and calibration. Results
support the view that **individual cognitive strategies**, not interface features, primarily drive overconfidence in
model understanding.

---

## Summary of Findings

- Most users showed **limited metacognitive adjustment**, even when their explanations were incorrect.
- Only a few participants (e.g., `P02`) showed **reflective reasoning**.
- **Tool design did not produce significant differences**, but user behavior varied strongly.



# M5: Illusion of Full Pattern Capture
##  for Animal Model

| Rank | Feature Pair                     | Silhouette Score |
|------|----------------------------------|------------------|
| 1    | (Swimming, Art)                  | 0.344925         |
| 2    | (Gardening, Swimming)            | 0.309039         |
| 3    | (Running, Swimming)              | 0.275788         |
| 4    | (Running, Gardening)             | 0.272583         |
| 5    | (Running, Art)                   | 0.269559         |
| 6    | (Gardening, Art)                 | 0.203763         |
| 7    | (Swimming, Detective Stories)    | 0.120282         |
| 8    | (Running, Detective Stories)     | 0.098232         |
| 9    | (Art, Detective Stories)         | 0.079767         |
| 10   | (Gardening, Detective Stories)   | 0.019680         |

| Rank | Feature Pair                     | Davies–Bouldin Score |
|------|----------------------------------|----------------------|
| 1    | (Gardening, Swimming)            | 1.046188             |
| 2    | (Swimming, Art)                  | 1.104325             |
| 3    | (Running, Gardening)             | 1.145908             |
| 4    | (Running, Art)                   | 1.324948             |
| 5    | (Gardening, Art)                 | 1.794250             |
| 6    | (Running, Swimming)              | 2.243333             |
| 7    | (Gardening, Detective Stories)   | 3.094975             |
| 8    | (Swimming, Detective Stories)    | 3.376596             |
| 9    | (Art, Detective Stories)         | 3.512363             |
| 10   | (Running, Detective Stories)     | 5.862948             |

To estimate the visual saliency of individual features, we aggregated silhouette scores from all feature pairs in which each feature appeared. For each feature, we computed the average silhouette score across those pairs, reflecting how consistently that feature contributes to clear class separation in 2D projections.

This yielded the following ranking:
Feature	Avg. Silhouette Score
Swimming	0.2625
Running	0.2290
Art	0.2245
Gardening	0.2013
Detective Stories	0.0795


Higher scores indicate greater visual cluster separability, suggesting these features are more likely to appear salient in scatter plots, regardless of actual model reliance.

feature 	avg_davies_bouldin_score
0 	Gardening 	1.7703
1 	Art 	1.9340
2 	Swimming 	1.9426
3 	Running 	2.6443
4 	Detective Stories 	3.9617

Lower scores => better clustering.
Silhouette score reflects local point-level clarity, which may be more aligned with what users visually perceive in a scatterplot.
Davies–Bouldin index reflects global class compactness and spacing, which may better describe how clearly defined clusters are from a machine learning or statistical perspective.

So final alignment for clustering : swimming, running, art, gardening, detective stories
Feature importance for Duck : gardening, swimming, running, art, detective stories

## for Alien Models

| Rank | Feature Pair                                      | Silhouette Score |
| ---- | ------------------------------------------------- | ---------------- |
| 1    | (Box Collecting, Laser Pointer Chasing)           | 0.224956         |
| 2    | (Plant Telepathy Practice, Box Collecting)        | 0.205498         |
| 3    | (Tool Worship, Box Collecting)                    | 0.162779         |
| 4    | (Reality Show Studies, Box Collecting)            | 0.095444         |
| 5    | (Plant Telepathy Practice, Laser Pointer Chasing) | 0.093741         |
| 6    | (Tool Worship, Plant Telepathy Practice)          | 0.090338         |
| 7    | (Tool Worship, Laser Pointer Chasing)             | 0.063149         |
| 8    | (Reality Show Studies, Laser Pointer Chasing)     | 0.025003         |
| 9    | (Reality Show Studies, Plant Telepathy Practice)  | 0.011975         |
| 10   | (Tool Worship, Reality Show Studies)              | -0.004316        |

| Rank | Feature Pair                                      | Davies–Bouldin Score |
| ---- | ------------------------------------------------- | -------------------- |
| 1    | (Box Collecting, Laser Pointer Chasing)           | 1.374105             |
| 2    | (Tool Worship, Box Collecting)                    | 1.568699             |
| 3    | (Plant Telepathy Practice, Box Collecting)        | 1.658908             |
| 4    | (Tool Worship, Laser Pointer Chasing)             | 1.716602             |
| 5    | (Plant Telepathy Practice, Laser Pointer Chasing) | 1.852680             |
| 6    | (Reality Show Studies, Box Collecting)            | 3.085304             |
| 7    | (Reality Show Studies, Laser Pointer Chasing)     | 3.151052             |
| 8    | (Tool Worship, Plant Telepathy Practice)          | 4.015468             |
| 9    | (Tool Worship, Reality Show Studies)              | 7.975616             |
| 10   | (Reality Show Studies, Plant Telepathy Practice)  | 8.810175             |

| Rank | Feature                  | Avg. Silhouette Score |
| ---- | ------------------------ | --------------------- |
| 1    | Box Collecting           | 0.1722                |
| 2    | Laser Pointer Chasing    | 0.1017                |
| 3    | Plant Telepathy Practice | 0.1004                |
| 4    | Tool Worship             | 0.0780                |
| 5    | Reality Show Studies     | 0.0320                |

| Rank | Feature                  | Avg. DB Score |
| ---- | ------------------------ | ------------- |
| 1    | Box Collecting           | 1.9218        |
| 2    | Laser Pointer Chasing    | 2.0236        |
| 3    | Tool Worship             | 3.8191        |
| 4    | Plant Telepathy Practice | 4.0843        |
| 5    | Reality Show Studies     | 5.7555        |


So final alignment for clustering : BC, LPC, PTP, TW, RSS
Feature importance for Zarnak): BC, TW, LPC, RSS, PTP


| participant_id | visual_align (WIT) | visual_align (HX) | model_align (WIT) | model_align (HX) | Î”(modelâˆ’visual) WIT | Î”(modelâˆ’visual) HX |
| -------------- | -----------------: | ----------------: | ----------------: | ---------------: | ------------------: | -----------------: |
| P02            |               0.80 |              0.88 |              0.84 |             0.92 |               +0.04 |              +0.04 |
| P03            |               0.52 |              0.74 |              0.47 |             0.58 |               âˆ’0.05 |              âˆ’0.16 |
| P04            |               0.76 |              0.92 |              0.84 |             0.96 |               +0.08 |              +0.04 |
| P05            |               0.47 |              0.58 |              0.52 |             0.47 |               +0.05 |              âˆ’0.11 |
| P06            |               0.47 |              0.69 |              0.52 |             0.58 |               +0.05 |              âˆ’0.11 |
| P07            |               0.80 |              0.84 |              0.84 |             0.84 |               +0.04 |               0.00 |
| P08            |               0.20 |              0.70 |              0.20 |             0.45 |                0.00 |              âˆ’0.25 |
| P09            |               0.52 |              0.74 |              0.47 |             0.58 |               âˆ’0.05 |              âˆ’0.16 |
| P10            |               0.84 |              0.88 |              0.88 |             0.92 |               +0.04 |              +0.04 |
| P11            |               0.52 |              0.74 |              0.47 |             0.58 |               âˆ’0.05 |              âˆ’0.16 |
### Average FAMS per tool


| Tool     | FAMS Visual Alignment | FAMS Model Alignment | FAMS Difference (Model âˆ’ Visual) |
| -------- | --------------------: | -------------------: | -------------------------------: |
| HypotheX |                 0.771 |                0.688 |                           âˆ’0.083 |
| WhatIf   |                 0.590 |                0.605 |                           +0.015 |
### Average FAMS per participant


| Participant | FAMS Visual Alignment | FAMS Model Alignment | FAMS Difference |
| ----------- | --------------------: | -------------------: | --------------: |
| P02         |                 0.840 |                0.880 |          +0.040 |
| P03         |                 0.630 |                0.525 |          âˆ’0.105 |
| P04         |                 0.840 |                0.900 |          +0.060 |
| P05         |                 0.525 |                0.495 |          âˆ’0.030 |
| P06         |                 0.580 |                0.550 |          âˆ’0.030 |
| P07         |                 0.820 |                0.840 |          +0.020 |
| P08         |                 0.450 |                0.325 |          âˆ’0.125 |
| P09         |                 0.630 |                0.525 |          âˆ’0.105 |
| P10         |                 0.860 |                0.900 |          +0.040 |
| P11         |                 0.630 |                0.525 |          âˆ’0.105 |
### One-Way ANOVA by Tool


| Metric                        | Factor      | F(df)         | p-value | Significant | Interpretation                                                                                  |
| ----------------------------- | ----------- | ------------- | ------- | ----------- | ----------------------------------------------------------------------------------------------- |
| **FAMS Visual Alignment**     | Tool        | F(1,18)=6.18  | 0.0229  | âœ… Yes       | Explanation tool significantly affects how strongly users align with the **visual explanation** |
| **FAMS Model Alignment**      | Tool        | F(1,18)=0.75  | 0.3988  | âŒ No        | Tool choice does **not** significantly affect alignment with **true model importance**          |
| **FAMS Alignment Difference** | Tool        | F(1,18)=7.15  | 0.0155  | âœ… Yes       | Tool influences whether users align more with **visuals or the model**                          |
| **FAMS Visual Alignment**     | Participant | F(9,10)=1.79  | 0.1889  | âŒ No        | Visual alignment is **consistent across participants**                                          |
| **FAMS Model Alignment**      | Participant | F(9,10)=13.98 | 0.0001  | âœ… Yes       | Strong **individual differences** in understanding the model                                    |
| **FAMS Alignment Difference** | Participant | F(9,10)=1.34  | 0.3267  | âŒ No        | Bias direction does not differ significantly across participants                                |