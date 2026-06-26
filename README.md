# HypotheX User Study description

## Goal
This user study accompanies the paper *Evaluating Interpretation Risks in Interactive What-If Scenarios and Mitigating with HypotheX*. It investigates **bias-related interpretation risks** in Hypothetical Scenario (HS)–based XAI — interactive *what-if* exploration in which users manipulate model inputs and observe the resulting changes in model outputs.

The study takes a human-centered view of explanation: understanding does not follow automatically from an explanation artifact but emerges as users actively form, test, and revise hypotheses about model behavior. This exploratory interaction is not cognitively neutral. Biases such as **anchoring, availability, and salience/overconfidence** shape how users select scenarios, sample inputs, compare outcomes, and sequence their actions. Crucially, these biases surface not as incorrect explanations but as **characteristic interaction patterns** that signal an elevated risk of misinterpretation, even when the underlying explanation is faithful.

The study addresses two research questions:
1. **How do bias-related interpretation risks manifest** as observable interaction patterns during HS-based exploration?
2. **To what extent can interface design reduce** their prevalence?

To examine design-level mitigation, the study compares two HS-based tools: the **What-If Tool** as a baseline, and **HypotheX**, an HS-based XAI system that adds interface safeguards intended to discourage bias-prone exploration. Bias-compatible interaction patterns are derived from prior literature and quantified with interaction-based metrics.

## Components of the User Study

The User Study is structured around the following main components:

### 1. Tools
- **What-If Tool**: A well-known XAI tool developed by Google, offering visualization and manipulation of individual data points to explore model predictions.  
  [Paper: *The What-If Tool: Interactive Probing of Machine Learning Models*](https://arxiv.org/abs/1907.04135)
- **HypotheX Tool**: The HS-based XAI system introduced in this work. It supports the hypothetical-scenario exploration methodology and adds interface-level safeguards intended to reduce bias-prone interaction patterns.  
  Available on our clarifAI platform: [https://explainable-ai.gfz.de/clarifAI/](https://explainable-ai.gfz.de/clarifAI/)


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


### 4. Exploration Tasks
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
- **Quantitative analysis**: Interaction-based metrics that quantify bias-compatible interaction patterns — e.g., the number and type of hypothesis checks, exploration breadth, and the correctness of result interpretation.
- **Qualitative analysis**: Assessing the hypothesis check strategies, their diversity, approaches to pre-exploration and reasoning, and hypothesis shifts during the checking process.
- **Cross-tool and cross-participant comparisons**: Understanding how different tool designs impact exploration effectiveness, cognitive resilience, and strategic behaviors during model investigation.

