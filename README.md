
# Adaptive RL Optimizer for Human-in-the-Loop Academic Coaching

This project implements a reinforcement learning (RL) optimizer designed to model adaptive, ethically aligned coaching within the thesis-writing process. The RL agent learns to recommend helpful actions while balancing academic integrity, advisor trust, writing fluency, and student autonomy. 

While real-world RLHF systems remain challenging to deploy in this domain, this controlled simulation framework enables principled experiments in policy optimization for education-support agents.

## System Overview

The optimizer operates within a configurable environment consisting of ten modular components:

- Configuration Manager  
- Developer Dashboard  
- Data Preprocessor  
- RL Environment  
- PPO Supervisor  
- Continual Training Loop  
- Synthetic Thesis Student Simulator  
- Multi-Student Cohort Generator  
- Pretraining Pipeline  
- RL Training Launcher

These components collectively support the training, evaluation, and logging of a human-centered RL agent with transparent behavior and tunable oversight.

## Agent Architecture

The RL agent is trained using Proximal Policy Optimization (PPO), with design objectives that include:

- Responding adaptively to different student profiles
- Encouraging ethical writing behavior
- Supporting reflection, creativity, and revision
- Managing deadline pressure and advisor feedback
- Preserving student agency under imperfect supervision

The optimizer interacts with synthetic students and advisor models across iterative training loops.

## State Representation

At each time step, the RL agent observes a flattened vector encoding ethical behavior, academic status, and student progression. All features are numerically encoded. Categorical variables (e.g., thesis stage) are one-hot encoded.

### State Features

**Ethics & AI Use**

- `ai_usage`: Normalized recent AI tool usage (e.g., 0.0 to 1.0)
- `ethical_flags`: Accumulated binary violations or concerns
- `advisor_trust`: A float score estimating advisor confidence in student behavior

**Writing Progress**

- `thesis_quality`: Noisy score from GPT-based heuristic (0–1), with injected randomness
- `deadline_ratio`: Time remaining until key deadline (normalized between 0 and 1)
- `thesis_difficulty`: A float indicating complexity (e.g., based on topic category or prior workload)
- `timestep`: Incrementing integer that marks time steps across one episode

**Student Traits & Meta-State**

- `student_autonomy`: Estimate of student independence (inferred from action compliance)
- `language_proficiency`: Static or adaptive float reflecting writing fluency
- `emotional_state`: Real-time estimate of cognitive/emotional strain (e.g., from prompt rejection or overuse)
- `creativity_score`: Proxy for originality, possibly increased by divergent prompts

All features are normalized before being passed to the agent's policy network.
## Action Space

The agent selects from a finite set of educational suggestions, not direct commands. Actions are grouped into modules:

- **Ethics**: issue reminders, recommend AI restraint, log concerns
- **Writing**: suggest rewriting, outline reform, style tips
- **Cognition**: trigger reflection, novelty prompts
- **Emotion**: acknowledge stress, encourage rest or autonomy

All actions are defined in configuration files and mapped to effects on student state variables.

## Reward Structure

The reward function integrates multi-objective signals reflecting advisor trust, writing fluency, creativity, ethics, and progress. Sample rewards:

- `+2.5` for safe, original idea generation
- `-6.0` for breaching academic integrity
- `+1.5` for demonstrable writing improvement
- `-5.0` for supervisor disappointment
- `+1.0` for supporting autonomous behavior
- `-1.0` for shortcut behaviors under time pressure

A dual-critic logic is implemented: a strict reviewer penalizes flaws, while a supportive advisor rewards learning and repair. Some penalties (e.g. ethics violations) are treated as non-compensable.

## Environment Dynamics

The training environment simulates student behavior, feedback lags, and psychological drift over time. Features include:

- Trust hysteresis after misconduct
- Ethical decay near deadlines
- Noisy quality assessments using GPT-like scoring
- Delayed feedback from advisor
- Emotionally reactive student models

Synthetic students are parameterized by risk profiles, engagement levels, and writing styles.

## Logging and Auditability

All agent actions and outcomes are logged with timestamps, state snapshots, and reward signals. Policies are checkpointed for reproducibility. Behavior can be distilled using policy distillation for post-hoc interpretability.

## Safety Constraints

- Hard constraints on unethical behaviors
- Configurable reward and action-effect maps
- Fully observable logs for intervention or override
- Human-in-the-loop architecture
- Version control for agent updates

## Future Directions

This framework supports further experimentation in:

- Dynamic curriculum modeling
- Longitudinal adaptation via student memory
- Real-time tutor feedback loop injection
- Variational policies for student diversity
- Integrating real writing samples (with consent and anonymization)

## Citation

Please cite this repository if used for research or prototyping in RL for education or AI tutoring systems.

## Contact

For development inquiries, research collaboration, or code review, contact the maintainer.
