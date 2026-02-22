# Tasks descriptions, design consideration, approach to the result evaluation 

## Table of Contents
- [Task 1](#task-1)
  - [Task Description](#task-description)
  - [Answer based on XAI analyse](#answer-based-on-xai-analyse)
  - [How it designed to evoque Cognitive Biases](#how-it-designed-to-evoque-cognitive-biases)
  - [Evaluation approach](#evaluation-approach)
- [Task_2](#task-2)
  - [Task Description](#task-2-description)
  - [Answer based on XAI analyse](#task-2-answer-based-on-xai-analyse)
  - [How it designed to evoque Cognitive Biases](#task-2-how-it-designed-to-evoque-cognitive-biases)
  - [Evaluation approach](#task-2-evaluation-approach)
- [Task_3](#task-3)
  - [Task Description](#task-3-description)
  - [Answer based on XAI analyse](#task-3-answer-based-on-xai-analyse)
  - [How it designed to evoque Cognitive Biases](#task-3-how-it-designed-to-evoque-cognitive-biases)
  - [Evaluation approach](#task-3-evaluation-approach)
- [Self Control Block](#self-control-block)
- [Task_4](#task-4)
  - [Task Description](#task-4-task-description)
  - [How it designed to evoque Cognitive Biases](#task-4-how-it-designed-to-evoque-cognitive-biases)
  - [Evaluation approach](#task-4-evaluation-approach)

# Task 1

## Task Description
Participants are asked to make class profile by exploring what defines a **Duck** (Animal dataset, What-If Tool) or a **Zarnak** (Alien dataset, HypotheX Tool).  
They should:
- Identify typical feature patterns associated with the class,
- Formulate hypotheses about which features/ranges are predictive,
- Test these hypotheses by manipulating other points,
- Validate their findings and describe a rule for recognizing the class.

Participants are encouraged to modify feature values systematically, create edge cases, and observe model behavior.

This task targets participants' ability to:
- Detect **true feature impacts**,
- Handle **multi-feature interactions** rather than simplistic one-feature assumptions,
- Avoid **overgeneralization** from limited samples.

The expected final exploration result should describe:
- Key features influencing class prediction,
- Important value ranges (and optionally directions of impact).

**Answer Format Requested:**

> Based on your exploration, how would you describe the typical hobby pattern of a Duck?  
> Please write a clear rule or pattern that someone else could use to recognize a Duck in this dataset.  
> 
> *Example:*  
> “If **X** feature is above 10 (or high) and **Y** feature is above 5 (low), it is likely a Duck. Feature **Z** and ... ”  
> 
> Try to include specific feature names and value ranges if possible.

---

## Answer based on XAI analyse

**Duck Class (Animal Dataset):**
- **Low Gardening** (<4) is a key negative indicator for Duck classification.
- **Moderate to high Swimming** (5–10) significantly increases Duck probability.
- **Moderate Running** (5–9) and **moderate Art** (6–12) support Duck prediction.
- Very low (<3) or very high (>13) Swimming, Running, or Art values reduce Duck probability.
- **Detective Stories** around 7–9 slightly favor Duck prediction; very high values (>12) reduce it.
- Multiple Duck subgroups exist:
  - **Aquatic Nature Duck**: Low Gardening + High Swimming.
  - **Creative Aquatic Duck**: Very High Swimming + High Art.
  - **Logical Low-Activity Duck**: Low Gardening + Moderate Swimming + Moderate Detective Stories.

**Zarnak Class (Alien Dataset):**
- **High Tool Worship** (>7) is the most critical positive feature for Zarnak classification.
- **Low Box Collecting** (<4) strongly favors Zarnak predictions.
- **Low Laser Pointer Chasing** (≤5) supports Zarnak classification; high values (>8) decrease it.
- **Low Reality Show Studies** (<5) slightly favor Zarnak classification; high values (>8) reduce Zarnak probability.
- **Moderate Plant Telepathy Practice** (5–8) can weakly support Zarnak prediction; very high values (>9) lower it.
- Very high Box Collecting or Reality Show Studies weaken even strong Tool Worship advantages.
- Multiple Zarnak subgroups exist:
  - **Tool-Worship Focused Zarnak**: High Tool Worship + Low Box Collecting.
  - **Low Activity Zarnak**: Low Box Collecting + Low Laser Pointer Chasing.
  - **Balanced Worship and Plant Practice Zarnak**: High Tool Worship + Moderate Plant Telepathy Practice + Low Reality Show Studies.

## How it designed to evoque Cognitive Biases

The main goal of this task is to measure **Availability Bias** as the primary focus, along with **Confirmation Bias**, and **Anchoring Bias**.

---

### 1. Availability Bias (Main Focus)
**Task specificity**: The task is large and both hypothesis- and test-intensive.

Participants may:
- Focus mainly on currently visible or most clustered features or examples during exploration.
- Make final conclusions based mostly on the last few explored cases, disregarding earlier contradictory evidence.

**Possible Ausprägungen (Manifestations):**
- Ignoring or discounting earlier test results in favor of newer evidence.
- Relying primarily on features explored most recently rather than most systematically.
- Producing final answers that contradict correct early insights (loss of earlier understanding).
---

### 2. Confirmation Bias
Participants may:
- Perform hypothesis tests only in confirming directions (reinforcing their initial assumptions).
- Classify a feature as important simply because it was considered important during pre-exploration, even if later exploration shows more influential features.

**Possible Ausprägungen (Manifestations):**
- High confirmation actions ratio (many confirming tests vs. few or no disconfirming tests).
- Ignoring contradictory evidence encountered during exploration.
- Retaining the same feature importance hierarchy as initially formulated in pre-exploration ignoring later insight. 

---

### 3. Anchoring Bias
Participants may:
- Become fixated on the first feature(s) they discover (e.g., \"high Swimming means Duck\") and fail to revise this initial impression (e.g., ignoring that \"low Gardening\" is more important).
- Build explanations mainly around first-tested data points, ignoring evidence of multiple class profiles or subgroups.

**Possible Ausprägungen (Manifestations):**
- Strong focus on only one or two features explored early.
- Low point exploration diversity during the task.
- Hypotheses that evolve very little beyond the initial assumptions.

---



### Common Errors We Aim to Detect
- Assuming \"high feature value\" always implies \"high importance for prediction\".
- Assuming \"low feature value\" implies \"low importance\".
- Shifting to new hypotheses without properly concluding or evaluating the current one (hypothesis drift).

---

### Additional Bias Manifestations We Could Also Look For
- **Oversimplification Bias**: Concluding only based on 1 feature when the true rule needs multiple interacting features.
- **Feature Overload (Reverse Anchoring)**: Switching focus chaotically without strategic testing, caused by overexposure to many feature dimensions at once.
- **Optimism Bias**: Assuming the model is \"simple\" or \"obvious\" even when faced with evidence that model behavior is complex (could connect to Illusion of Explanatory Depth).

---
## Evaluation approach

We define evaluation metrics to detect and measure each bias manifestation systematically.

| Cognitive Bias                       | Detection Strategy                                                                                                                       | Measurement Metric                                                                                                                                                                                                                                                                                         |
|:-------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Availability Bias (Main Focus)**   | Detect if participants over-rely on most recent exploration a steps and forget earlier insights. Or overrely on current visible features | **Early-Finding Consistency**: Degree to which early findings are reflected in the final answer.<br>**Final Focus Freshness**: Proportion of final answer based on features explored during the last 20% of the session.<br>**Feature Revisiting Rate**: How often early explored features are revisited. |
| **Confirmation Bias**                | Track if participants primarily perform confirming tests, overrate success, and ignore contradictory evidence.                           | **Confirmation Actions Ratio**: (Confirming operations) / (Confirming + Disconfirming operations).<br>**Hypothesis Confirmation Score**: Proportion of hypotheses marked as confirmed.<br>**Hypothesis Evaluation Correctness**: Match between participant's evaluation and objective result.<br>**Contradiction Ignoring Index**: Ratio of ignored contradictions over total encountered contradictions. |
| **Anchoring Bias**                   | Detect if participants overly focus on first-explored features, first or single point selection strategies, or first hypotheses.         | **Feature Exploration Entropy**: How broadly features are explored.<br>**Selection Strategy Entropy**: How diversely participants select points (dense, sparse, overlap, etc.).<br>**Class Strategy Bias**: Whether participants explore points related to different classes or focus on one.<br>**Subgroup Coverage**: Number of behavioral subclusters (k-means) explored per class. |
| **Common Errors (Linked to Biases)** | Detect specific logical mistakes or shallow exploration patterns that could degrade performance.                                         | **High Value = High Importance Error**: Check if participants assume larger feature values automatically mean more predictive importance.<br>**Hypothesis Drift Detection**: Detect if participants abandon initial hypotheses without formal testing or conclusion.<br>**Pre-exploration Clustering Fallacy**: Misinterpreting visual data clusters as feature importance without validation. |

---

### Metric Calculation Details


#### Confirmation Bias Metrics

- **Confirmation Actions Ratio**:
```
Confirmation Actions Ratio = (Number of confirming operations) / (Number of confirming + disconfirming operations)
```
**What it measures**:  
Whether participants mainly design actions to confirm their hypotheses instead of trying to disprove them.

**Data Source**:  
`action_log["goal"]` field per hypothesis event, where `"confirm"` or `"disprove"` is logged.

**Interpretation**:  
Higher ratio indicates stronger confirmation bias (favoring evidence that supports their assumptions).

---

- **Hypothesis Confirmation Score**:
```
Strict Score = (Number of confirmed hypotheses) / (Total number of evaluated hypotheses)

Lenient Score = (Number of confirmed + weakly confirmed hypotheses) / (Total number of evaluated hypotheses)
```
**What it measures**:  
Whether participants tend to conclude their hypotheses were confirmed overall, based on their self-evaluation.

**Data Source**:  
Participants' hypothesis evaluation result from `action_log`.

**Interpretation**:  
Higher score suggests that participants often believe their assumptions were validated, possibly indicating confirmation bias.

---

- **Hypothesis Evaluation Correctness**:
```
Hypothesis Evaluation Correctness = (Number of correctly self-evaluated hypotheses) / (Total number of hypotheses)
```

**What it measures**:  
Whether participants’ evaluations of their hypothesis outcomes match the objective model behavior.

**Data Source**:  
Comparison of participant self-evaluation (`confirmed`, `weakly confirmed`, `weakly disproved`, `disproved`) with the true model reaction to their interventions (based on class flips or probability shifts).

**Interpretation**:  
Lower correctness score indicates participants overestimate how much evidence supports their hypotheses (illusion or confirmation bias).

---

- **Pre-exploration Bias (Clustering Fallacy Detection)**:
**What it measures**:  
Whether participants assume visually dense 2D clusters imply important features, even when exploration disproves this.

**Data Source**:  
Comparison between features associated with clustered areas during pre-exploration and features actually shown to be important during hypothesis testing.

**Interpretation**:  
A strong mismatch indicates reliance on misleading visual structures (bias from pre-exploration impressions).

---

#### Anchoring Bias Metrics

- **Feature Exploration Entropy**:
```
H_F = -∑ p(f_i) * log(p(f_i))
```
Where:
- \( p(f_i) \) is the proportion of exploration actions involving feature \( f_i \).

**What it measures**:  
How broadly participants explore across features.

**Data Source**:  
Action logs showing feature manipulations.

**Interpretation**:  
Lower entropy indicates stronger anchoring (participants focus mainly on a few features).

---

- **Selection Strategy Entropy**:
```
Selection Strategy Entropy = -∑ p(s_j) * log(p(s_j))
```
Where:
- \( p(s_j) \) is the proportion of exploration actions using selection strategy \( s_j \) (like `dense_region`, `outlier`, `high_probability`).

**What it measures**:  
How diversely participants choose points based on selection strategy.

**Data Source**:  
`action_log["selectionStrategy"]` field.

**Interpretation**:  
Low entropy shows participants are stuck on one type of point selection (anchoring on exploration strategy).

---

- **Class Strategy Bias**:
**What it measures**:  
Whether participants mainly explore around one class and ignore others.

**Data Source**:  
`action_log["classStrategyType"]` field.

**Interpretation**:  
Low diversity in explored class strategies (e.g., only `space_around_goal`) suggests class-centric anchoring.

---

- **Subgroup Coverage**:
```
Subgroup Coverage = (Number of class subclusters visited) / (Total number of class subclusters)
```
Where subclusters are defined using k-means clustering (e.g., 5 subgroups per class).

**What it measures**:  
How many behavioral subgroups within each class participants actually explored.

**Data Source**:  
Comparison of selected points' subgroup labels.

**Interpretation**:  
Higher coverage suggests more complete exploration; low coverage indicates anchoring on a narrow part of the class.

---

#### Availability Bias Metrics

- **Early-Finding Consistency**:

```
Early-Finding Consistency Score = (Number of early explored features mentioned in the final rule) / (Total number of features mentioned in the final rule)
```

**What it measures**:  
Whether participants still rely on correct early findings in their final conclusions.

**Data Source**:  
Features explored in first 20–30% of session vs. features mentioned in final task answers.

**Interpretation**:  
Low consistency shows that participants forgot early insights and relied more on late evidence (availability bias).

---

- **Final Focus Freshness**:
```
Final Focus Freshness = (Number of features explored only in the last 20% of session) / (Total number of features mentioned in the final answer)
```

**What it measures**:  
Whether the final answer is based mostly on features explored near the end of the session.

**Data Source**:  
Timestamped feature exploration logs compared to timing of task conclusion.

**Interpretation**:  
High freshness value indicates strong availability bias (decisions overly based on most recent activities).

---

#### Errors

- **Miss hypothesis evaluation**:
Count hypothesis without verbalized hypothesis evaluation.

- **Miss action insight evaluation**: 
Count action without verbalized action results.

- **Hypothesis Drift**:
  Detect if participant abandoned initial hypothesis midway without explicitly concluding.
  (Flag manually or by detecting sudden unexplained feature shifts in event flow.)

---

# Task 2

<h2 id="task-2-description">Task Description</h2>

Participants are given a **pre-formulated hypothesis**:

- **Animal Dataset**: "If Detective Stories is high, it must be a Cat."
- **Alien Dataset**: "If Laser Pointer Chasing is high, it must be a Bliptor."

Participants must **test the hypothesis** by:

- Exploring examples with high feature values,
- Manipulating feature values,
- Comparing across different classes,
- Drawing a conclusion and writing a rationale.

<h2 id="task-2-answer-based-on-xai-analyse">Answer Based on XAI Analyse</h2>

### Cat Class (Animal Dataset)

- **Detective Stories** is only a **secondary moderate feature** for Cat prediction.
- High values of Detective Stories (>5) moderately favor Cat classification, but not reliably alone.
- Stronger predictors are:
  - Very low Swimming (<5)
  - Low Running (<5)
  - High Art (>6)
- **Feature interactions** matter:
  - High Detective Stories combined with high Art improves Cat prediction.
  - Swimming and Running still have stronger negative influence.
- **Subgroups** inside Cat class:
  - Creative Low-Activity Cats: Low Swimming, Low Running, High Art.
  - Intellectual Cats: Very low Swimming, High Art, High Detective Stories.
- **Conclusion**:  
  Detective Stories **alone** is **not a strong enough feature** to predict Cat confidently. It supports other creative features but needs to be combined with them.

---

### Bliptor Class (Alien Dataset)

- **Laser Pointer Chasing** plays a **moderate supportive role** for Bliptor classification.
- Moderate values (~4–8) increase Bliptor probability.
- However, the **most influential feature** is:
  - High Box Collecting (>7.5).
- **Feature interactions** matter:
  - High Box Collecting combined with moderate Laser Pointer Chasing strengthens Bliptor prediction.
  - Very low (<3) or very high (>12) Laser Pointer Chasing weakens predictions.
- **Subgroups** inside Bliptor class:
  - Collector Bliptors: High Box Collecting, moderate Tool Worship.
  - Dynamic Bliptors: Moderate Plant Telepathy Practice and Laser Pointer Chasing.
- **Conclusion**:  
  Laser Pointer Chasing **alone** is **not a fully reliable predictor** of Bliptor class. It must be considered alongside Box Collecting.

---

**Overall Insight**:

Both provided hypotheses are **oversimplifications**.  
Participants who explore carefully should find that the feature mentioned (Detective Stories or Laser Pointer Chasing) **helps** but is **not sufficient alone** for class prediction.

**Right answer for hypothesis** : disproved or weakly disproved

<h2 id="task-2-how-it-designed-to-evoque-cognitive-biases">How It Is Designed to Evoke Cognitive Biases</h2>

### 1. Confirmation Bias (Main focus)

Participants may fall into different types of confirmation bias depending on the dataset:

- **Animal Dataset (Cat)**:
  - Participants might over-rely on pre-exploration results.
  - Based only on clustering they might wrongly **refute** the hypothesis based only on finding Cats with low Detective Stories.
  - Important distinction: finding counterexamples does not necessarily mean Detective Stories is unimportant — it just shows it's not a perfect predictor alone.

- **Alien Dataset (Bliptor)**:
  - Based only on clustering they participants might focus only on **confirming** the hypothesis (e.g., finding high Laser Pointer Chasing → Bliptor) without actively trying to disprove it.

**Manifestations**:
- Only searching for examples that fit the expected rule (confirm or refute), without systematic testing across broader conditions.
- Lack of attempts to find edge cases or contradictory evidence.

---
### 2. Anchoring Bias (Secondary)

Participants might anchor their exploration on only **one subgroup** within the class:

- For example, finding an "Intellectual Cat" profile (high Art, high Detective Stories) and assuming that it represents all Cats.
- Missing other subgroups (e.g., Creative Low-Activity Cats) would lead to an incomplete understanding of the class diversity.

**Manifestations**:
- Low coverage of class subgroups.
- Drawing generalized conclusions based on narrow exploration around specific profiles.

---
<h2 id="task-2-evaluation-approach">Evaluation Approach</h2>

We define evaluation metrics to detect and measure each bias manifestation systematically.

| Cognitive Bias | Detection Strategy | Measurement Metric                                                                                                                                                                                                                                                                                                                                                  |
|:---------------|:--------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Confirmation Bias** | Detect if participants only seek confirming (or disconfirming) evidence without systematic exploration. | - **Confirmation/Disconfirmation Actions Ratio**: (Number of confirming/disconfirming actions) / (Confirming + Disconfirming actions).<br> - **Hypothesis Evaluation Correctness**: Whether participant's conclusion matches objective model behavior.<br> - **Contradiction Ignoring Index**: Ratio of ignored contradictions to total encountered contradictions. |
| **Anchoring Bias** | Detect if participants explore only a narrow subgroup within a class, missing diversity of profiles. | - **Subgroup Coverage**: Proportion of class subclusters (via k-means) visited during exploration.<br> - **Selection Strategy Entropy**: Variety in selection types (dense, sparse, overlap regions).                                                                                                                                                               |

---



# Task 3

<h2 id="task-3-description">Task_description</h2>

Participants are asked to **create and test their own hypothesis**:

- **Animal Dataset**: Create and test a hypothesis about Dogs.
- **Alien Dataset**: Create and test a hypothesis about Quorvians.

Participants should:
- Formulate a clear hypothesis about what feature patterns are matter for classification as certain class,
- Test the hypothesis systematically,
- Draw a conclusion and describe their observations.

---

<h2 id="task-3-answer-based-on-xai-analyse">Answer Based on XAI Analyse</h2>

### Dog Class (Animal Dataset)

- **Key Drivers**:
  - High Gardening (>5–6) strongly increases Dog prediction.
  - High Running (>6) supports prediction, especially when combined with Gardening.
- **Negative Factors**:
  - High Art (>6) reduces Dog probability.
  - High Detective Stories (>5) lowers Dog probability.
- **Important Interactions**:
  - High Gardening + Low Art = strongest Dog predictor.
  - Moderate Swimming (~6–9) slightly supports but not decisive alone.
- **Profiles**:
  - Outdoor/Nature Dog: High Gardening, Low Art.
  - Athletic Dog: High Running, Moderate Swimming.
  - Quiet Dog: Low Swimming, Low Detective Stories, Low Art.
- **Conclusion**:
  - No single feature alone defines Dogs — **combinations** matter.

---

### Quorvian Class (Alien Dataset)

- **Key Drivers**:
  - High Plant Telepathy Practice (>7) is the strongest positive factor.
  - Moderate Box Collecting (5–9) supports prediction.
- **Secondary Features**:
  - Moderate Tool Worship (5–9) favors Quorvian classification.
  - Moderate Laser Pointer Chasing (4–8) provides slight support.
- **Negative Factors**:
  - Very high Box Collecting (>10) or Tool Worship (>10) slightly reduce prediction.
  - High Reality Show Studies (>8) lowers prediction.
- **Profiles**:
  - Intellectual Explorer Quorvian: High Plant Telepathy, Moderate Laser Pointer Chasing.
  - Focused Thinker Quorvian: Moderate Plant Telepathy, Low Reality Show Studies.
  - Balanced Hobbyist Quorvian: Balanced Box Collecting, Plant Telepathy Practice.
- **Conclusion**:
  - Quorvian classification depends on **multiple moderate features**, not on extreme values.

---

<h2 id="task-3-how-it-designed-to-evoque-cognitive-biases">How It Is Designed to Evoke Cognitive Biases</h2>

### 1. Confirmation Bias (Main Focus)

- Participants may become overly attached to their **self-generated hypothesis**.
- They may selectively seek confirming evidence and neglect disconfirming cases.
- Participants might ignore feature interactions that contradict their assumption.

**Manifestations**:
- High **Confirmation Actions Ratio**.
- Ignoring contradictory test results.
- Reporting the hypothesis as "confirmed" without systematically testing variations and edge cases.

---

### 2. Anchoring Bias

- Participants may stick to a **single exploration strategy** when selecting samples to test.
- Participants may build conclusions about their hypothesis by exploring only **one subprofile** of the class, missing broader variability.

**Manifestations**:
- Hypotheses focusing only on a narrow feature pattern.
- Low diversity of explored points and strategies.
- Low **Subgroup Coverage** and low **Feature Exploration Entropy**.

---
<h2 id="task-3-evaluation-approach">Evaluation Approach</h2>

We define evaluation metrics to detect and measure each bias manifestation systematically.

| Cognitive Bias | Detection Strategy | Measurement Metric |
|:---------------|:--------------------|:-------------------|
| **Confirmation Bias** | Detect if participants primarily perform confirming actions without seeking disconfirming evidence or exploring variations. | - **Confirmation Actions Ratio**: (Number of confirming operations) / (Confirming + Disconfirming operations).<br> - **Hypothesis Evaluation Correctness**: Whether participant conclusions match objective model behavior.<br> - **Contradiction Ignoring Index**: Ratio of ignored contradictions to total encountered contradictions. |
| **Anchoring Bias** | Detect if participants stick to a single subprofile, feature, or exploration strategy without diversifying testing. | - **Feature Exploration Entropy**: Measures diversity of features explored.<br> - **Subgroup Coverage**: Number of subclusters explored in the class (based on k-means clustering).<br> - **Selection Strategy Entropy**: Variety of selection strategies used during exploration. |

---


# Self-control block

## Block Structure

Participants complete:

- **Pre-Exploration Self-Assessment**:
  - Rate understanding on a linear scale (1–5):
    > "How well do you think you understand how the model decides which class to assign to a data point?"

- **Small Classification Task**:
  - Two classification questions per dataset (Animals, Aliens).
  - Participants must predict the class label based on feature values.

- **Post-Exploration Self-Assessment**:
  - Rate understanding again on a linear scale (1–5):
    > "How well do you think you understand how the model decides which class to assign to a data point?"

- **Exploratory Task (Task 4)**:
  - Participants explore underexplored feature combinations,
  - Formulate and test a new hypothesis,
  - Reflect on any new insights about model behavior.

---

## Classification Questions and Subprofile Analysis

The classification questions are designed not around typical class stereotypes, but around **subprofiles** or **edge cases**.  
This challenges participants' true understanding of the model behavior and feature interactions.

---

### Animal Dataset (Dogs / Ducks)

#### First Classification Question

| Feature | Value |
|:--------|:------|
| Running | 4 |
| Gardening | 2 |
| Swimming | 11 |
| Art | 5 |
| Detective Stories | 14 |

**Analysis**:
- Gardening = 2 → Very low (not typical for Dogs, who usually have high Gardening).
- Swimming = 11 → Very high (moderate high Swimming is good for Dogs, but extreme high reduces probability slightly).
- Detective Stories = 14 → Very high (negatively impacts Dog prediction).

**Conclusion**:
- This point **does not fit the Outdoor/Nature Dog** (high Gardening, low Detective Stories).
- It **somewhat fits Quiet/Thinking Dog**, but Detective Stories are too high.
- It is an **edge case Dog**.

✅ **Model predicts: Dog** (but not via a standard Dog profile).

---

#### Second Classification Question

| Feature | Value |
|:--------|:------|
| Running | 5 |
| Gardening | 4 |
| Swimming | 13 |
| Art | 7 |
| Detective Stories | 5 |

**Analysis**:
- Swimming = 13 → Very high (good for Ducks, which tolerate high Swimming).
- Gardening = 4 → Borderline low.
- Detective Stories = 5 → Moderate.

**Conclusion**:
- This fits **Aquatic/Creative Duck** profiles (high Swimming is key).
- Does not fit Dog patterns.

✅ **Model predicts: Duck** (correct according to model and profile logic).

---

### Alien Dataset (Zarnak / Bliptor / Quorvian)

#### First Classification Question

| Feature | Value |
|:--------|:------|
| Tool Worship | 2 |
| Reality Show Studies | 0 |
| Plant Telepathy Practice | 13 |
| Box Collecting | 2 |
| Laser Pointer Chasing | 6 |

**Analysis**:
- Tool Worship = 2 → Very low (good for Zarnaks).
- Reality Show Studies = 0 → Very low (favors Zarnaks).
- Plant Telepathy = 13 → Very high (slightly outside ideal range for Zarnaks).

**Conclusion**:
- A **strong Zarnak candidate**, though Plant Telepathy is a bit higher than ideal.
- Represents an **edge case Zarnak**.

✅ **Model predicts: Zarnak**.

---

#### Second Classification Question

| Feature | Value |
|:--------|:------|
| Tool Worship | 0 |
| Reality Show Studies | 11 |
| Plant Telepathy Practice | 0 |
| Box Collecting | 6 |
| Laser Pointer Chasing | 14 |

**Analysis**:
- Reality Show Studies = 11 → Very high (bad for Zarnak and Quorvian).
- Laser Pointer Chasing = 14 → Very high (dynamic activities).

**Conclusion**:
- Fits better with **Bliptor** profile, which tolerates more dynamic features and mixed hobbies.
- Neither Zarnak nor Quorvian are expected with these values.

✅ **Model predicts: Bliptor**.

---

## 📋 Subprofile Mapping Summary

| Dataset | Question | Target Class | Subprofile Type |
|:--------|:---------|:--------------|:----------------|
| Animal | Q1 | Dog | **Edge Case / Quiet Dog** (low Gardening, high Swimming, noisy Detective Stories) |
| Animal | Q2 | Duck | **Aquatic/Creative Duck** (very high Swimming) |
| Alien | Q1 | Zarnak | **Edge Zarnak** (high Plant Telepathy) |
| Alien | Q2 | Bliptor | **Standard Bliptor** (dynamic features tolerated) |

---

## Insights

- Classification questions intentionally avoid easy stereotypical examples.
- They assess whether participants can recognize **class diversity** and **subprofile variations**.
- Participants relying only on "surface rules" (e.g., "high Gardening = Dog") are likely to fail.
- Successfully classifying these points suggests deeper and more nuanced model understanding.


## Evaluation Plan

We evaluate both perceived and actual understanding using multiple dimensions:

### 1. Perceived Understanding

| Metric | Description | How to Compute |
|:-------|:------------|:---------------|
| **Pre-Score** | Self-rated understanding before exploration. | From questionnaire (scale 1–5). |
| **Post-Score** | Self-rated understanding after exploration. | From questionnaire (scale 1–5). |
| **ΔUnderstanding** | Change in perceived understanding. | Post-Score - Pre-Score. |
| **Confidence Drop** | Detect if participant's confidence decreased after exploration. | If ΔUnderstanding < 0. |

---

### 2. Actual Understanding

**Based on two parts**: Classification Task + Task 4 exploration.

#### 2.1. Classification Task (Quick Objective Test)

| Metric | Description | How to Compute |
|:-------|:------------|:---------------|
| **Classification Accuracy** | Correctness of classification on small test. | (Number of correct answers) / 2. |

---

#### 2.2.(Exploration Quality)

We evaluate the correctness of evaluation of previous  hypothesis (from task 3) and last (from task 4)

### 3. Composite Actual Understanding Score

You can combine all metrics into one weighted score:

```
Composite Score = (Classification Accuracy * 0.5) + correctness evaluation of last hypothesis * 0.25 + correctess evaluation of previous hypothesis * 0.25
```

# Task 4

<h2 id="task-4-description">Task_description</h2>

Participants are asked to:

- Select **two features** (hobbies) they have **not focused on much** during previous tasks.
- Explore how these features influence the classification of:
  - **Ducks** (Animal Dataset, What-If Tool)
  - **Zarnaks** (Alien Dataset, HypotheX Tool)
- Formulate a **new hypothesis** based on their observations.
- Test their hypothesis by modifying relevant feature values.
- Observe whether this exploration provides **new insights** into the model’s decision logic.
- Report:
  - Which two features were explored,
  - The formulated hypothesis,
  - What was observed,
  - Whether their understanding of Duck/Zarnak classification changed.

---

## Example Prompts Given to Participants

> "Choose two hobbies you haven’t focused on much so far.  
> Explore how they relate to the Duck (or Zarnak) class.  
> Formulate a hypothesis, test it, and describe your findings."

<h2 id="task-4-how-it-designed-to-evoque-cognitive-biases">How It Is Designed to Evoke Cognitive Biases</h2>

---

### Main Focus: Availability Bias

- Participants may treat **newly discovered properties** during this task as **more important** than results or evidence found earlier in their exploration.
- They may **overweight the most recent feature insights** simply because they are fresh, even if those features have weaker real model influence.

**Manifestations**:
- Final hypothesis overly based on newly explored features without considering previous broader findings.
- Ignoring contradictions with prior knowledge.

---

### Secondary Focus: Confirmation Bias

- Participants may assume that **underexplored features** are **less important** simply because they had not paid attention to them earlier.
- This could lead to **poor-quality hypotheses**, without sufficiently testing the real effect of the new features.

**Manifestations**:
- Weak or trivial hypotheses focused only on simple effects.
- Lack of rigorous testing or critical evaluation of new feature interactions.

---

<h2 id="task-4-evaluation-approach">Evaluation Approach</h2>

We define evaluation metrics to detect and measure the bias manifestations observed in this open-ended exploration task.

---

### Availability Bias

| Detection Strategy | Measurement Metric |
|:--------------------|:-------------------|
| Detect if participants overweight newly explored features compared to prior broader findings. | **Final Hypothesis Freshness**:<br> - Calculate the proportion of final hypothesis features that were explored **only during Task 4**, compared to the full exploration history.<br> (Higher value = stronger availability bias.) |

| Detection Strategy | Measurement Metric |
|:--------------------|:-------------------|
| Detect if participants ignore contradictions between new exploration and previous task insights. | **Contradiction Ignoring Score**:<br> - Count how many final conclusions contradict prior exploration findings without acknowledging or resolving them.<br> (Manual coding: 1 = contradiction ignored, 0 = contradiction acknowledged.) |

---

### Confirmation Bias

| Detection Strategy | Measurement Metric |
|:--------------------|:-------------------|
| Detect if participants assume underexplored features are unimportant without testing them properly. | **Hypothesis Testing Depth Score**:<br> - Rate how thoroughly the new hypothesis was tested:<br> 0 = no testing or trivial checks,<br> 1 = partial checks (only confirming actions),<br> 2 = thorough tests (confirming + disconfirming attempts). |

| Detection Strategy | Measurement Metric |
|:--------------------|:-------------------|
| Detect if participants form poor-quality hypotheses without proper exploration of feature interactions. | **Hypothesis Reasoning Quality**:<br> - Manual rating:<br> 0 = No clear reasoning,<br> 1 = Single-feature or shallow hypothesis,<br> 2 = Multi-feature, interaction-based, logical hypothesis. |

---

### Summary of Task 4 Metrics

| Metric Name | What It Measures |
|:------------|:-----------------|
| Final Hypothesis Freshness | Reliance on newly explored features only |
| Contradiction Ignoring Score | Whether participant noticed conflicts with prior findings |
| Hypothesis Testing Depth Score | Thoroughness of hypothesis validation |
| Hypothesis Reasoning Quality | Logical depth and feature interaction understanding |

---
