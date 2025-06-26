# Thesis Assistant: Modular AI Writing Support with Ethics-Aware RL Supervision

##  Project Overview

The **Thesis Assistant** is a modular system for AI-enhanced academic writing. It integrates large language models (LLMs) with an **ethically grounded reinforcement learning (RL) agent** to ensure transparency, human-centered control, and emotionally supportive guidance.

This assistant is not just a writing tool — it is a simulated **research environment** for exploring AI collaboration, authorship tracking, and adaptive policy learning under ethical constraints.

### 🧠 Module Responsibilities

| Module             | Primary Role                                          | Sensitive Data Shared With Ethics Module |
|--------------------|-------------------------------------------------------|-------------------------------------------|
| `EthicsModule`     | Logs, classifies, detects, supervises AI usage        | Receives data from all modules            |
| `IdeaBrainstorming`| Generating, refining, and exploring thesis ideas      | Original prompts, generated ideas, feedback ratings |
| `WritingSupport`   | Drafting, summarizing, rephrasing academic content    | User input, AI output, writing style changes |
| `EmotionSupport`   | Emotional coaching and sentiment analysis             | Detected emotion, motivation level, request patterns |


---

## ⚙️ System Modules Overview

The Thesis Assistant is composed of several interconnected modules, each fulfilling a distinct role in the thesis-writing process. All modules communicate through a central orchestrator and are supervised by a Reinforcement Learning–based `EthicsSupervisor` agent to ensure responsible, transparent, and emotionally aware AI assistance.

---

### 🛡️ 1. Ethics Module – Orchestrated by `EthicsSupervisor`

The Ethics Module serves as a cross-cutting supervisory system that monitors all user interactions, AI-generated content, and writing progress. It provides real-time feedback, performs authorship audits, and triggers ethical interventions when necessary.

This module is governed by a Reinforcement Learning agent (`EthicsSupervisorRL`) that continuously receives state updates from the system and determines adaptive policy actions based on ethical, behavioral, and emotional signals.

**Core Submodules:**

| Submodule              | Description                                                                 |
|------------------------|-----------------------------------------------------------------------------|
| `AI_Detector`          | Analyzes generated content to estimate AI vs. human authorship likelihood   |
| `Usage_Logger`         | Records prompt–response data, timestamps, and intent metadata               |
| `HumanPromptChecker`   | Flags ethically questionable or overly directive prompts                    |
| `AdvisorFeedbackSync`  | Tracks whether feedback from thesis advisors has been addressed             |
| `EthicalViolationAlert`| Issues warnings or suggestions based on configurable policy thresholds      |

🧠 The output of these submodules is compiled into a numerical state vector that is consumed by the RL agent to make context-sensitive decisions (e.g., alerting, labeling, nudging).

---

### ✍️ 2. Writing Support Module

Provides structured and responsive support for drafting, refining, and polishing academic text. It enables students to move from outline to final draft with adaptive feedback at every stage.

**Key Methods:**

- `create_outline(topic: str, stage: str)`  
  Generates a thesis-appropriate structural outline based on the user’s topic and current phase.

- `draft_section(outline: dict, context: str)`  
  Produces a preliminary draft section using the provided structure and background context.

- `summarize_text(text: str)`  
  Condenses complex text into an accurate summary.

- `rephrase_text(text: str, style: str)`  
  Improves clarity and tone while preserving content accuracy.

- `check_grammar_style(text: str)`  
  Offers automated proofreading for grammar, punctuation, and academic style adherence.

🛡️ **Ethics Integration:**  
Each interaction is logged and evaluated by the `EthicsModule` to ensure fair authorship attribution, minimize overreliance on AI, and prevent unintended plagiarism.

---

### 💡 3. Idea Brainstorming Module

Facilitates ideation and conceptual exploration using LLM-assisted methods. This module helps users move from vague interests to researchable topics while receiving structured support.

**Key Methods:**

- `generate_ideas(prompt: str, stage: str)`  
  Suggests potential thesis topics or subthemes based on user intent and academic phase.

- `explore_idea(idea: str)`  
  Expands on a single idea with related concepts, implications, or potential hypotheses.

- `refine_ideas(ideas: list, feedback: str)`  
  Iteratively improves a list of ideas using user feedback and semantic similarity heuristics.

🛡️ **Ethics Integration:**  
Generated ideas are evaluated for originality, prompt formulation risks, and potential overlap with known academic work. The system gently discourages templated or ethically grey ideation patterns.

---

### 💗 4. Emotion Support Module

Monitors user sentiment and provides psychological scaffolding to reduce burnout and enhance motivation. The system uses sentiment analysis to deliver timely encouragement, stress relief, or pacing advice.

**Key Methods:**

- `detect_emotion(user_input: str)`  
  Uses NLP sentiment tools to assess the user’s emotional tone (e.g., frustration, confidence, fatigue).

- `provide_encouragement(detected_emotion: str, stage: str)`  
  Delivers context-sensitive motivational feedback based on the emotional state and thesis phase.

- `suggest_break()`  
  Recommends breaks during periods of cognitive overload or emotional distress.

- `celebrate_milestone(milestone: str)`  
  Provides positive reinforcement when the user completes a major task or reaches a writing goal.

🛡️ **Ethics Integration:**  
Emotional state metrics are used as part of the RL agent’s input state to ensure ethical interventions are calibrated to the user’s mindset and energy level.

---

### 🔁 Cross-Module Interaction Summary

All modules report back to the `EthicsModule` and contribute to a shared RL state vector. This enables:

- Real-time ethical evaluation of content generation and editing
- Adaptive emotional pacing and intervention tone
- Reinforcement learning–based nudging to build responsible writing habits
- Human-in-the-loop authorship validation and transparency

> Each module plays a unique role, but together they form a co-regulated ecosystem where the human remains the author — and AI remains the guide.


## 🧩 Orchestration: `ThesisAssistant`

The central interface that connects all modules. It acts as the primary entry point for user interaction and routes inputs dynamically.

**Key Responsibilities:**

- Directs inputs to appropriate modules (brainstorming, writing, emotion)
- Queries the Ethics Module for oversight and logging
- Collects signals to construct the RL state
- Receives action recommendations from the RL agent
- Presents coherent and ethically informed responses to the user


## 🔁 Interaction Flow and Ethical Feedback Loop

### 1. **IdeaBrainstorming ↔ EthicsModule**

- **Outbound**: Every idea generation prompt and its resulting outputs are sent to the Ethics Module.
- **Ethical Evaluation**:
  - Was the prompt asking for prohibited content?
  - Does the idea show signs of AI plagiarism or template overuse?
- **Inbound**:
  - Ethical nudges: “Try a more original angle”
  - Warnings: “Your idea matches known thesis titles too closely”

---

### 2. **WritingSupport ↔ EthicsModule**

- **Outbound**: All input/output text pairs (e.g., rephrasing requests) are logged.
- **AI Detection**:
  - Run `detect_ai()` on generated sections.
  - Track changes after user edits.
- **Authorship Tracking**:
  - Uses embedding similarity to assess originality.
- **Inbound**:
  - Feedback: “Consider rewriting this paragraph yourself”
  - Alerts: “Excessive LLM usage in this section”
  - AI Attribution Labels: Inline markers like *[AI-suggested]*

---

### 3. **EmotionSupport ↔ EthicsModule**

- **Outbound**: Detected user frustration, burnout signs, or motivation spikes.
- **Behavioral Tracking**:
  - Frequency of “give up” phrases
  - Sudden spikes in passive usage (e.g., lots of generate requests without edits)
- **Inbound**:
  - Ethics agent modulates tone of interventions
  - Emotional cues influence RL state (e.g., “if user = overwhelmed → soft prompt instead of hard warning”)

---

### 4. **EmotionSupport ↔ WritingSupport (Contextual Cross-Modulation)**

- Emotion data adjusts the writing assistant’s tone:
  - If `user_emotion = anxious`: simplify suggestions, break down tasks
  - If `user_emotion = motivated`: challenge user with stronger suggestions

---

### 🔀 Integrated Example Flow

User: "Give me 5 thesis ideas on AI and education"

→ [IdeaBrainstorming] generates list  
→ [EthicsModule] classifies prompt, logs ideas  
→ EthicsSupervisor detects high AI similarity  
→ Sends soft alert: "Consider rephrasing your query to reflect your own research context"  
→ [User rephrases], [WritingSupport] turns idea into outline  
→ [EmotionSupport] detects frustration, nudges with encouragement  
→ RL Agent logs engagement, updates intervention strategy

---


### 🤖 RL Agent: `EthicsSupervisorRL`

This agent simulates ethical and behavioral oversight via reinforcement learning. The goal is to adaptively intervene based on a user’s behavior, emotional state, and writing progress — while modeling the complexities of human-in-the-loop systems.

### RL State Space Structure:

| Category               | Features (Examples)                                                                                 |
|------------------------|-----------------------------------------------------------------------------------------------------|
| **Ethical Features**   | AI Detection Score, Prompt Classification, Usage Frequency, Embedding Similarity, Alert Status     |
| **Human Feedback**     | Rephrased AI content, engagement with intervention prompts                                          |
| **Thesis Progress**    | Current stage, task completion rate, advisor feedback recency                                       |
| **Performance Signals**| Work quality proxy, time since last milestone, progress velocity                                    |

State vectors are encoded and fed into the RL environment. The RL agent selects actions like "soft warning", "ask for justification", or "recommend reflection", all integrated into user-facing modules.

---

## 💡 Creativity Through Simulated RLHF

> “While true RLHF reward models remain out of reach at this stage, this controlled simulation provides a sandbox to explore adaptive policy learning for human-in-the-loop academic coaching.”

The system is intentionally designed to **model behaviors, not dictate them**. It allows experimentation with:

- Soft policy shaping via nudges and alerts  
- Proxy reward signals based on user reflection  
- State-sensitive interventions (e.g., less confrontational when frustrated)  
- Agent–user feedback loops for long-term trust calibration

---

## 🧪 Usage (Sample)

```text
```python
from thesis_assistant import ThesisAssistant

assistant = ThesisAssistant(api_key="...", config=rl_config)

response = assistant.process_input(
    user_input="Please improve the clarity of this paragraph",
    module="WritingSupport"
)
print(response)
