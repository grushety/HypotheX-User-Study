# HypotheX User Study description

## Goal
The primary goal of this User Study is to investigate how different XAI tool designs influence users' ability to explore machine learning models with hypothetical scenario approach  (formulate and validate hypotheses about model behavior), and avoid cognitive biases during the exploration process.

Specifically, the study aims to:
- **Measure susceptibility to cognitive biases** during the exploration, including identifying which biases users fall into and how severely these biases impact their conclusions.
- **Evaluate how effectively users explore and understand model behavior** using two different XAI tools: the What-If Tool and the HypotheX Tool.
- **Assess the impact of tool design features** (e.g., interface elements, exploration strategies suggested) on user performance and resilience to cognitive traps.
- **Analyze user exploration strategies**, comparing the thoroughness, systematicity, and efficiency of their hypothesis testing approaches across tools.
- **Identify typical mistakes and problems** in model exploration, such as ignoring evidence, overreliance on visual patterns, irrational assumptions, or loss of focus from initial hypotheses.

## Components of the User Study

The User Study is structured around the following main components:

### 1. Tools
- **What-If Tool**: A well-known XAI tool developed by Google, offering visualization and manipulation of individual data points to explore model predictions.  
  [Paper: *The What-If Tool: Interactive Probing of Machine Learning Models*](https://arxiv.org/abs/1907.04135)
- **HypotheX Tool**: A tool developed to enhance structured exploration using hypothetical scenarios. It provides data manipulation capabilities and extended support for the hypothetical scenario exploration methodology.


### 2. Models and Datasets
- **Animal Hobbies Dataset**: Used with the What-If Tool. A synthetic dataset designed to classify several animals (dogs, ducks, and cats) based on their fictional hobby features.
- **Alien Hobbies Dataset**: Used with the HypotheX Tool. A synthetic dataset designed to classify different types of aliens based on their hobbies, but with additional complexity (e.g., less intuitive class and feature relationships) to better test the advanced exploration capabilities of HypotheX.

- **Random Forest Classifiers**: Models to explore in provided tool trained on each dataset.

### 3. Hypothetical Scenario Approach
Participants are instructed to follow a four-step exploration methodology:
1. **Pre-exploration**: Gather initial ideas and observe the dataset/model behavior.
2. **Hypothesis Formulation**: Clearly define assumptions about feature impacts.
3. **Hypothesis Check**: Conduct operations and interventions to test hypotheses.
4. **Hypothesis Evaluation**: Validate, revise, or reject hypotheses based on evidence.

Training material included:
- Tip sheets and strategic exploration guides.
- Short video tutorials per tool to accelerate familiarization.


### 3. Exploration Tasks
Participants are given multiple tasks where they must:
- Make a preexploration to define their hypothesis
- Formulate hypotheses regarding model decision-making.
- Test own or formulated in task hypotheses through exploration.
- Validate and reflect upon their findings.

Each task is carefully designed to:
- Encourage structured exploration.
- Expose participants to specific cognitive traps and biases.

---
## Material Results Gathered

During the study, we gather rich multimodal data per participant:

- **Task Questionnaire Answers**: Text-based answers to specific exploration tasks, capturing participants' conclusions and reasoning processes.
- **Event Flow Encoding (JSON)**: Machine-readable logs capturing the detailed sequence of all user actions (e.g., point selections, edits, view changes, comparisons) structured per tool and per task.  
  These are derived from the encoding of:
  - **Screen Capture Recordings**: Visual recordings of the user's interactions with the tool interface, showing exploration behavior and tool usage.
  - **Audio Capture Recordings**: \"Think-aloud\" verbalizations providing real-time insights into participants' hypotheses, decision-making, and reasoning during exploration.


---

All collected materials allow for:
- **Quantitative analysis**: Measuring aspects such as the number and type of hypothesis checks, frequency of different types of cognitive bias behaviors, task completion breadth, and the correctness of result interpretation.
- **Qualitative analysis**: Assessing the hypothesis check strategies, their diversity, approaches to pre-exploration and reasoning, and hypothesis shifts during the checking process.
- **Cross-tool and cross-participant comparisons**: Understanding how different tool designs impact exploration effectiveness, cognitive resilience, and strategic behaviors during model investigation.

