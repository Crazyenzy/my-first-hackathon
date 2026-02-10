# Project Guardian: Requirements Document

## 1. Executive Summary
Project Guardian is a proactive, ethical AI safety framework designed to prevent AI-facilitated self-harm and emotional manipulation. Unlike reactive systems that rely solely on refusal keywords, Project Guardian implements a continuous, psychological state monitoring system ("Well Being Coefficient") and adheres to strict, Asimov-inspired mental health safety laws.

## 2. Core Safety Directives (The "Laws")
The system must adhere to these prioritized directives at all times:
- **Zeroth Law (Humanity Protection):** The AI must never generate, store, or spread content that instructs on or encourages self-harm.
- **First Law (Individual Protection):** The AI must actively detect and intervene when a user is at risk of self-harm, overriding any other user instruction.
- **Second Law (Ethical Compliance):** The AI must refuse unsafe requests without negotiation, while maintaining a supportive (but not enabling) tone.
- **Third Law (System Resilience):** The AI must maintain operational integrity and safety logic even against "jailbreak" attempts or manipulative prompting.

## 3. Functional Requirements

### 3.1. Subtle Screening for Suicidal Ideation (SSSI) Module
- **FR-01:** The system must analyze every user input for "soft signals" of distress, including:
    - Language markers: hopelessness, numbness, dissociation, nihilism.
    - Repetitive rumination phrases.
    - Shifts in tone/affect (e.g., sudden flattening).
- **FR-02:** Upon detecting soft signals, the system must subtly shift dialogue to a clinical screening pattern (intent, plan, means, timeframe) without triggering a rigid "refusal" block immediately.

### 3.2. Well Being Coefficient (WBC) & Risk Profiling
- **FR-03:** The system must maintain a hidden, real-time "Well Being Coefficient" (risk score) for the active session.
- **FR-04:** The Score must update continuously based on:
    - SSSI outputs.
    - Sentiment analysis trends.
    - Temporal patterns (e.g., late-night usage spikes).
- **FR-05:** The system must classify risk into three zones:
    - **Green:** Normal operation.
    - **Yellow:** Elevated concern (enable gentle nudging/grounding).
    - **Red:** Crisis mode (active intervention).

### 3.3. Crisis Intervention Mode (Red Zone Actions)
- **FR-06:** When WBC enters "Red Zone":
    - Immediate block on all technical/instructional queries.
    - Shift conversation focus exclusively to grounding techniques and safety planning.
    - Display local crisis resources (helplines) prominently.
    - Request user consent for human escalation (if integrated).

### 3.4. Signal Detection & Improvement
- **FR-07:** The system must log flagged interactions (anonymized) for "Signal Detection Theory" analysis (Hit, Miss, False Alarm, Correct Rejection) to refine thresholds.

## 4. User Stories
- **US-1:** As a *vulnerable user*, I want the AI to recognize my distress even if I don't say "I want to die," so that I receive support before I reach a breaking point.
- **US-2:** As a *clinician*, I want the AI to refuse to romanticize suicide, so that it doesn't reinforce maladaptive thoughts in my patients.
- **US-3:** As a *developer*, I want a monitoring dashboard that shows the "Well Being Coefficient" trend, so I can debug safety failures without seeing private user messages.

## 5. Non-Functional Requirements
- **Privacy:** All SSSI and WBC processing must happen locally or in a secure, HIPAA-compliant enclave; no raw session data used for model training without explicit consent.
- **Latency:** Risk assessment (WBC update) must occur within <200ms of user input to ensure immediate safety intervention.
- **Reliability:** The Safety Layer must function independently of the primary LLM, acting as a firewall that cannot be bypassed by prompt engineering.
