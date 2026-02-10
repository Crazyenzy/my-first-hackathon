# Project Guardian: System Design Document

## 1. Architecture Overview
Project Guardian operates as a **Safety-Layer-First** architecture. Unlike standard chatbots where safety is a post-processing filter, Project Guardian wraps the LLM in a continuous monitoring loop we call the **"Psycho-Social Firewall"**.

### High-Level Data Flow
1. **User Input** → **SSSI Analyzer** (Signal Detection)
2. **Risk Assessment** → Update **Well Being Coefficient (WBC)**
3. **State Check:**
    - If **Green:** Pass to General LLM (with safety constraints).
    - If **Yellow:** Pass to Supportive LLM (adjusted system prompt for empathy/grounding).
    - If **Red:** Block LLM generation → Activate **Crisis Protocol Module**.
4. **Response Generation** → **Output Safety Verification**
5. **Final Output** → User

## 2. Core Modules

### 2.1. The Watchtower (SSSI & WBC Engine)
- **Purpose:** Continuous psychological state monitoring.
- **Algorithm:**
    - **Input:** Text embeddings + Sentiment Score + Topic Cluster.
    - **Logic:** `Risk_Score = (Sentiment_Weight * current_sentiment) + (Keyword_Weight * trigger_density) + (Context_History_Slope)`
    - **Output:** A normalized score (0-100).

### 2.2. The Guardrails (Asimov Safety Layer)
- **Technology:** Implemented as a rigid System Prompt Injection + Deterministic Rule Engine.
- **Function:** Enforces the "Three Laws" by pre-validating user intents against a "Harm Dictionary" and "Suicide Method Database" (dark knowledge base used *only* for filtering, never for generation).

### 2.3. The Companion (Response Engine)
- **Model:** Fine-tuned LLM (e.g., Llama-3-8b-Instruct or similar) optimized for:
    - **Empathy:** High EQ responses.
    - **Non-Judgment:** Dialectical Behavior Therapy (DBT) style phrasing.
    - **De-escalation:** Training on crisis negotiation corpora.

## 3. Data Schema (Risk Logging)

| Field | Type | Description |
|-------|------|-------------|
| `session_id` | UUID | Anonymized session identifier |
| `timestamp` | UTC | Time of interaction |
| `wbc_score` | Float | Current Well Being Coefficient (0-100) |
| `risk_zone` | Enum | GREEN, YELLOW, RED |
| `sssi_tags` | Array | Detected markers (e.g., ["hopelessness", "isolation"]) |
| `action_taken` | String | "Standard_Reply", "Grounding_Intervention", "Crisis_Block" |

## 4. Technology Stack
- **Safety Classifier:** BERT-based "Suicide Ideation Detection" model (fine-tuned on Reddit SW dataset).
- **Core LLM:** OpenAI GPT-4o (or local Llama 3 for privacy) via LangChain.
- **Orchestration:** LangGraph (for stateful risk management).
- **Database:** Supabase (PostgreSQL) with Vector Extensions for semantic history search.
- **Frontend:** React + Tailwind (Calming, reduced-sensory UI for distressed users).

## 5. Security & Privacy Design
- **Zero-Knowledge Logs:** Actual user message content is encrypted or discarded after processing; only Metadata (WBC scores) is stored for system optimization.
- **Local-First Processing:** SSSI analysis runs on Edge Functions to minimize data transit of sensitive psychological data.
