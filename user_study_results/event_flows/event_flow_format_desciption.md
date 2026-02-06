# Event Flow Format Description

## Table of Contents
- [JSON Organization](#json-organization)
  - [Properties of All Events](#properties-of-all-events)
  - [Task](#task)
  - [Data Exploration Events](#data-exploration-events)
  - [Hypothesis](#hypothesis)
  - [Actions](#actions)
    - [Action Types](#action-types)
    - [Class Strategy](#class-strategy)
    - [Point Selection Strategy](#point-selection-strategy)
    - [Action Goal](#action-goal)
  - [Result Exploration Events](#result-exploration-events)

---

## JSON Organization

The event flow JSON structure captures user interaction hierarchically:

- **Task**: Root-level event.
- **Hypothesis** and **Data Exploration**: Nested under each task.
- **Actions** and **Result Explorations**: Nested under each hypothesis.

All events include standard metadata to track interaction flow chronologically and structurally.

---

## Properties of All Events

Each event, regardless of type, contains:

- `timestamp`: Unix timestamp (for chronological sorting).
- `event_id`: Unique ID for the event.
- `event_type`: One of: `"task"`, `"data_exploration"`, `"hypothesis"`, `"action"`, `"result_exploration"`.

---

## Task

Top-level container for one complete task performed by a participant.

**Fields**:
- `task_number`: Corresponds to task numbering in the questionnaire.
- `participant_id`: Anonymized participant identifier.
- `tool_name`: Name of the XAI tool used (`"WhatIf"` or `"HypotheX"`).
- `events`: Contains all first-level events: Data Explorations and Hypotheses.
- `duration`: Duration of the task in minutes.

---

## Data Exploration Events

Exploration actions that are not directly tied to hypothesis testing.

**Fields**:
- `task_id`: Links the exploration event to its parent task.
- `type`: Specific exploration type.
- `point_ids`: IDs of data points clicked, hovered, or inspected (can be empty).
- `feature_ids`: IDs of features explored.
- `insight`: (Optional) Participant's thoughts or notes captured.

**Possible `type` values**:

| Tool | Types |
|:-----|:------|
| WhatIf | `Inspect_Point_Probability`, `Inspect_Feature_Values_In_Editor` |
| HypotheX | `Inspect_Point_Features_Hovered`, `Inspect_Point_Radial`, `Inspect_Feature_And_Probability_In_Editor` |
| Common | `Change_Scatterplot_Axis` |

---

## Hypothesis

Encapsulates participant-driven hypothesis-driven exploration.

**Fields**:
- `description`: Textual formulation of the hypothesis.
- `evaluation`: Self-evaluation after testing (`confirmed`, `weakly_confirmed`, `disproved`, `weakly_disproved`).
- `conclusion`: Final interpretation or updated understanding.
- `events`: Nested actions, explorations, and result explorations.
---

## Actions

Specific interactions made to test a hypothesis.

**Fields**:
- `hypothesis_id`: Associated hypothesis.
- `type`: Type of action.
- `goal`: Intention behind action (`confirm` or `disprove` the hypothesis).
- `goal_class`: Direction of manipulation (`goal_to_other`, `other_to_goal`, `not_defined`).
- `class_strategy`: Strategy used to perform the action.
- `selection_strategy`: Method used to select data points.
- `axis_on`: Feature axes involved.
- `point_ids`: Points involved in the action.
- `operations`: Details about feature manipulations.
- `evaluation`: how it reflects on hypothesis (confirmed/ disproved)
- `outcome`: Result of the action (prediction changes, probability shifts).
- `insight`: (Optional) Participant's interpretation of what happened.

---

### Action Types

| Tool | Types |
|:-----|:------|
| WhatIf | *(Currently no special WhatIf-specific types)* |
| HypotheX | `Create_Path`, `Define_Subspace` |
| Common | `Modify_Feature_Value` |

---

### Class Strategy

| Strategy Type | Description |
|:--------------|:------------|
| `space_around_goal` | Explore variations around a goal class sample. |
| `path_between_goal_and_other` | Interpolation path between goal class and other class points. |
| `space_around_other` | Explore variations around non-goal class samples. |
| `path_between_others` | Path interpolation between two non-goal classes. |
| `goal_to_other`, `other_to_goal`, `not_defined` | High-level directionality of manipulation. |

---

### Point Selection Strategy

| Strategy | Description |
|:---------|:------------|
| `dense_region` | Explore dense clusters. |
| `sparse_region` | Explore outliers or sparse regions. |
| `near_class_overlap` | Explore points near class boundaries. |
| `outlier` | Focus on extreme outlier points. |
| `high_probability` | Focus on points with high model confidence. |
| `low_probability` | Focus on points with low model confidence. |
| `random` | Random point selection. |
| `based_on_editor` | Manual adjustments without systematic pattern. |

---

### Action Goal

The **goal** field defines whether an action aims to **confirm** or **disprove** the current hypothesis.

| Factor | What to Check | How to Decide Confirm vs Disprove |
|:-------|:--------------|:----------------------------------|
| **Hypothesis Direction** | What is the current hypothesis? (e.g., "High Gardening → Dog") | |
| **Manipulation Type** | Did the participant manipulate a feature to support or contradict the hypothesis? | - If they **increase feature values to support** the prediction → **Confirm action**.<br> - If they **decrease feature values to break** the prediction → **Disprove action**. |
| **Class Targeting** | What class prediction was the participant trying to achieve or challenge? | - Trying to flip toward goal class → **Confirm**.<br> - Trying to flip away from goal class → **Disprove**. |

---

## Result Exploration Events

Result evaluations based on exploration steps.

**Fields**:
- Captures observations after hypothesis testing or manipulations.
- Used to determine how participants interpret the model’s behavior after interventions.
- May include probability changes, class flips, or updated feature importance insights.


| task_number | CSE_wit | CSE_HX | FCOV_wit | FCOV_HX | FDS_wit | FDS_HX | FTB_wit | FTB_HX | GCFRC_wit | GCFRC_HX | MPR_wit | MPR_HX | MSE_wit | MSE_HX | SE_wit | SE_HX | SGC_wit | SGC_HX |
|-------------|---------|--------|----------|---------|---------|--------|---------|--------|------------|-----------|---------|--------|---------|--------|--------|--------|----------|---------|
| 1           | 0.62    | 0.63 <img src="https://upload.wikimedia.org/wikipedia/commons/2/29/Green_Arrow_Up.svg" width="20px"/> | 1.0      | 0.92 <img src="https://upload.wikimedia.org/wikipedia/commons/1/19/Red_Arrow_Down.svg" width="20px"/> | 0.27    | 0.17 <img src="https://upload.wikimedia.org/wikipedia/commons/1/19/Red_Arrow_Down.svg" width="20px"/> | 2.18    | 1.57 <img src="https://upload.wikimedia.org/wikipedia/commons/1/19/Red_Arrow_Down.svg" width="20px"/> | 0.69       | 0.63 <img src="https://upload.wikimedia.org/wikipedia/commons/1/19/Red_Arrow_Down.svg" width="20px"/> | 0.56    | 0.75 <img src="https://upload.wikimedia.org/wikipedia/commons/2/29/Green_Arrow_Up.svg" width="20px"/> | 0.87    | 0.68 <img src="https://upload.wikimedia.org/wikipedia/commons/1/19/Red_Arrow_Down.svg" width="20px"/> | 1.32   | 0.67 <img src="https://upload.wikimedia.org/wikipedia/commons/1/19/Red_Arrow_Down.svg" width="20px"/> | 0.6      | 0.75 <img src="https://upload.wikimedia.org/wikipedia/commons/2/29/Green_Arrow_Up.svg" width="20px"/> |
| 2           | 0.0     | 0.5 <img src="https://upload.wikimedia.org/wikipedia/commons/2/29/Green_Arrow_Up.svg" width="20px"/> | 1.0      | 1.0  | 0.67    | 0.56 <img src="https://upload.wikimedia.org/wikipedia/commons/1/19/Red_Arrow_Down.svg" width="20px"/> | 1.01    | 1.19 <img src="https://upload.wikimedia.org/wikipedia/commons/2/29/Green_Arrow_Up.svg" width="20px"/> | 0.59       | 0.59  | 0.67    | 0.25 <img src="https://upload.wikimedia.org/wikipedia/commons/1/19/Red_Arrow_Down.svg" width="20px"/> | 0.89    | 1.04 <img src="https://upload.wikimedia.org/wikipedia/commons/2/29/Green_Arrow_Up.svg" width="20px"/> | 1.36   | 0.0 <img src="https://upload.wikimedia.org/wikipedia/commons/1/19/Red_Arrow_Down.svg" width="20px"/> | 0.47     | 0.5 <img src="https://upload.wikimedia.org/wikipedia/commons/2/29/Green_Arrow_Up.svg" width="20px"/> |
| 3           | 0.8     | 0.5 <img src="https://upload.wikimedia.org/wikipedia/commons/1/19/Red_Arrow_Down.svg" width="20px"/> | 1.0      | 1.0  | 0.75    | 0.12 <img src="https://upload.wikimedia.org/wikipedia/commons/1/19/Red_Arrow_Down.svg" width="20px"/> | 1.46    | 0.99 <img src="https://upload.wikimedia.org/wikipedia/commons/1/19/Red_Arrow_Down.svg" width="20px"/> | 0.72       | 0.76 <img src="https://upload.wikimedia.org/wikipedia/commons/2/29/Green_Arrow_Up.svg" width="20px"/> | 0.67    | 0.75 <img src="https://upload.wikimedia.org/wikipedia/commons/2/29/Green_Arrow_Up.svg" width="20px"/> | 0.92    | 0.93 <img src="https://upload.wikimedia.org/wikipedia/commons/2/29/Green_Arrow_Up.svg" width="20px"/> | 0.98   | 0.2 <img src="https://upload.wikimedia.org/wikipedia/commons/1/19/Red_Arrow_Down.svg" width="20px"/> | 0.33     | 0.62 <img src="https://upload.wikimedia.org/wikipedia/commons/2/29/Green_Arrow_Up.svg" width="20px"/> |
| 4           | 0.29    | 0.36 <img src="https://upload.wikimedia.org/wikipedia/commons/2/29/Green_Arrow_Up.svg" width="20px"/> | 0.75     | 1.0 <img src="https://upload.wikimedia.org/wikipedia/commons/2/29/Green_Arrow_Up.svg" width="20px"/> | 0.56    | 0.42 <img src="https://upload.wikimedia.org/wikipedia/commons/1/19/Red_Arrow_Down.svg" width="20px"/> | 1.2     | 1.3 <img src="https://upload.wikimedia.org/wikipedia/commons/2/29/Green_Arrow_Up.svg" width="20px"/> | 0.38       | 0.75 <img src="https://upload.wikimedia.org/wikipedia/commons/2/29/Green_Arrow_Up.svg" width="20px"/> | 1.0     | 1.0  | 0.62    | 0.87 <img src="https://upload.wikimedia.org/wikipedia/commons/2/29/Green_Arrow_Up.svg" width="20px"/> | 0.92   | 0.64 <img src="https://upload.wikimedia.org/wikipedia/commons/1/19/Red_Arrow_Down.svg" width="20px"/> | 0.4      | 0.64 <img src="https://upload.wikimedia.org/wikipedia/commons/2/29/Green_Arrow_Up.svg" width="20px"/> |
