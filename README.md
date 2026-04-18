Here’s your content cleanly formatted in Markdown:

---

# MindCanvas
## Built w/o vibecoding- https://github.com/nagh2312/Claude_Hackathon_mspm
## How We Built With Claude

---

## 1. What We Built and Why Claude Is Central to It

MindCanvas is a daily emotional journaling companion designed for the 300 million people living with anxiety who either cannot access therapy or have long gaps between sessions. The product turns journaling — something clinically proven but notoriously hard to stick with — into a meaningful, rewarding, and clinically connected daily habit.

Claude is not a feature bolt-on here. It is the engine. Every meaningful user interaction in the product is powered by Claude. Without it, MindCanvas is a blank notes app. With it, it becomes something a person might actually open every morning.

Below is an honest account of where and how we used Claude — from the API calls we designed to the creative prompts we agonised over to the safety architecture we built around it.

---

## 2. The Core API Integrations

### 2a. Emotional interpretation of journal entries

The most fundamental call we make to Claude is asking it to read a journal entry and understand what the person was feeling — not what they literally wrote, but the emotional texture of the moment.

We pass in the raw entry and ask Claude to return a structured emotional profile:

Dominant mood
Secondary mood
Intensity level
A brief narrative reflection

**Prompt design note**
We spent a lot of time making sure Claude didn't therapise the user or tell them how they felt.

**Instruction:**

 Reflect back what you sense in the writing. Do not diagnose. Do not advise. Respond as a thoughtful reader, not a clinician.

That single framing shift made the outputs feel human rather than clinical.

---

### 2b. Generating personal artwork from emotional state

After reading the entry, Claude produces a description of the artwork that represents that emotional moment.

We use a structured output call that returns:

Mood
Palette
Compositional feel

This is passed downstream to an image generation model.

Claude plays two roles here:

1. Interpreting emotional nuance
2. Translating it into aesthetic language

Routing through Claude (instead of direct text → image) significantly improved output quality and personal resonance.

**Examples**

| Entry Tone                | Description                                                                 |
| ------------------------- | --------------------------------------------------------------------------- |
| High anxiety / fragmented | "Turbulent geometry, fractured planes, deep indigo and electric white"      |
| Quiet grief               | "Still water, muted greys, single point of warm amber light at the horizon" |
| Cautious hope             | "Soft dawn palette, one open window, light entering diagonally"             |

---

### 2c. Surfacing evidence-based guidance (RAG + Claude)

This is the most technically involved integration.

We built a **RAG layer** grounded in:

Peer-reviewed psychology literature
Anonymised treatment data

When Claude identifies a mood pattern:

1. It queries the retrieval layer
2. Surfaces a relevant intervention

   * Grounding exercise
   * Behavioral activation
   * Breathing technique

**Constraint we enforced**

Every suggestion must cite its source
No hallucinated techniques
If confidence is low → Claude explicitly says so

**Why this mattered**
We could have allowed free-form suggestions. We chose not to.

For a mental health product, **traceability is non-negotiable**.
This constraint made the difference between something usable vs something trustworthy.

---

### 2d. Monthly therapist report generation

At the end of each month, Claude synthesizes 30 days of journal data into a clinician-readable summary.

**Inputs**

Emotional profiles
Keywords
Patterns

**Output structure**

Mood trajectory
Recurring triggers
Notable turning points

We interviewed three therapists to shape this.

**What they wanted**

Trajectory first
Then triggers
Then raw highlights

**What they did NOT want**

Diagnoses
Clinical conclusions

The report ends with:

**“Questions to explore”**
→ prompts users can bring into therapy sessions

---

## 3. The Safety Architecture — Where Claude Does Its Most Important Work

We designed a **multi-agent system** to separate responsibilities:

| Agent            | Role                                                                                           |
| ---------------- | ---------------------------------------------------------------------------------------------- |
| Companion Agent  | Handles journaling, reflections, guidance, artwork briefs. Optimized for warmth.               |
| Safety Agent     | Monitors distress signals, self-harm indicators. Runs in parallel. Invisible unless triggered. |
| Escalation Agent | Handles crisis handoff. Surfaces resources. Does not attempt therapy.                          |

**Key design insight**
One model cannot simultaneously:

Be warm and open
Be clinically vigilant

So we separated those concerns.

**Design principle**

When in doubt → Safety Agent flags
Escalation is handled with warmth, not alarm

---

## 4. How We Approached Prompting

Prompting is the craft layer of this product.

The difference between generic and meaningful output came almost entirely from instruction design.

### Principles we followed

**1. Give Claude a role, not just a task**

 You are a thoughtful reader who has known this person for a long time.
 You are not a therapist.
 You reflect with care.

---

**2. Constrain output format tightly**

Explicit JSON schemas
Structured outputs improved reliability significantly

---

**3. Negative instructions matter**

Do not diagnose
Do not use clinical terminology
Do not express concern unless certain

These were as important as positive instructions.

---

**4. Keep reasoning for complex calls**
For RAG-based recommendations:

Claude reasons first
Then outputs

This improved both:

Accuracy
Debuggability

---

## 5. Claude Code in the Development Process

We used Claude Code beyond boilerplate — for real system building.

### What we built with it

**RAG pipeline**

Retrieval + re-ranking
API integration layer
Reduced build time from days → hours

---

**Prompt testing harness**

Synthetic data generation
Test runner
Scoring heuristics

---

**Structured output parsing**

JSON validation
Retry logic
Edge case handling

---

**Multi-agent orchestration**

Parallel execution (Companion + Safety)
Routing logic

---

**Summary**
Claude Code collapsed the gap between:

Product thinking
Working implementation

---

## 6. What Worked Well — and What Was Hard

### What worked

Claude’s emotional intelligence is strong when prompted well
Structured outputs were highly reliable
Multi-agent separation improved system control and safety

---

### What was hard

**Safety calibration**

Most difficult problem
Tradeoff: sensitivity vs trust

---

**Artwork generation**

Default outputs were generic
Required few-shot prompting for nuance

---

**Latency**

Parallel agents increased response time
Mitigated via streaming on Companion side

---

## 7. Screenshots

(Add here)
<img width="1440" height="900" alt="image" src="https://github.com/user-attachments/assets/c77cc3a5-1810-49fd-8746-d8261917d661" />

<img width="197" height="900" alt="image" src="https://github.com/user-attachments/assets/a8af374b-7840-4017-be56-4cb1ffe070cc" />

<img width="142" height="900" alt="image" src="https://github.com/user-attachments/assets/4277a8c5-b642-4d98-8c7d-f4a7cf692cc4" />

<img width="238" height="896" alt="image" src="https://github.com/user-attachments/assets/82951f17-b3c0-47b3-b649-063e93e36805" />

<img width="167" height="900" alt="image" src="https://github.com/user-attachments/assets/fcd95468-b4fe-4b6b-9f97-fa174d82aa1f" />

---

## 8. Closing

MindCanvas exists because of:

Claude’s emotional intelligence
Strong structured generation
Speed of development via Claude Code

The product is not just faster to build because of Claude — it is fundamentally different because of it.

We built this with a clear bar:

 If someone is having a hard day, this should feel worth opening.

That standard shaped every layer of the system.

---

**MindCanvas | Confidential | 2025**

---
