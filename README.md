# 🧠 Prompt Engineering — Project 1
### Zero-Shot & Few-Shot Data Extraction Pipeline
**DecodeLabs Industrial Training | Batch 2026**

---

## 📌 Project Overview

This project demonstrates **deterministic prompt engineering** — the discipline of programming a Large Language Model (LLM) to behave like a strict data extraction engine rather than a conversational chatbot.

Given a chaotic, unstructured customer support email, the engineered prompt instructs the model to extract exactly **five structured variables** and return them as **valid JSON** — with zero conversational filler, zero hallucination, and `null` returned for any missing field.

> **Core Insight:** Stop talking to the AI. Start programming the compilation engine.

---

## 🎯 The Mission

Extract the following five fields from a raw customer support email:

| Field | Type | Description |
|-------|------|-------------|
| `customer_name` | `String \| null` | Full name as written in the email |
| `order_number` | `String \| null` | Alphanumeric order reference |
| `complaint_type` | `Enum` | DAMAGED_ITEM, WRONG_ITEM, MISSING_ITEM, LATE_DELIVERY, BILLING_ERROR, OTHER |
| `severity_level` | `Integer (1–5)` | Inferred from tone: 1 = minor, 5 = extreme urgency |
| `contact_phone` | `String \| null` | Phone number if present — never hallucinated |

---

## ⚙️ The 4 Engineering Pillars

### 1. 🌡️ Temperature = 0.0
Sets the model to deterministic mode. Identical inputs always produce identical outputs. Eliminates token drift and format hallucination.

### 2. 🔒 Delimiters (###)
Wraps raw user data in ### markers to isolate instructions from data. Prevents prompt injection attacks where email content could override system instructions.

### 3. 📦 Strict JSON Output
System prompt uses positive constraints to enforce output format:
- Output starts with { and ends with }
- No markdown wrappers
- No conversational prefixes

### 4. 🎯 Few-Shot Examples (3 Perfect Pairs)
Provides the model with 3 structurally perfect input/output examples before the live task. Pushes format adherence from ~60% (zero-shot) to over 99%.

---

## 🧾 The Engineered Prompt

See prompt.txt for the full system prompt.

---

## ✅ Gatekeeper Test Result: PASS

Test email intentionally omitted the contact phone number.
Pipeline correctly returned null for contact_phone without hallucinating a value.

See test_cases/ folder for full input and expected output.

---

## 🛠️ Tools & Stack

| Tool | Purpose |
|------|---------|
| Claude (Anthropic) | LLM used for extraction |
| Temperature 0.0 | Deterministic output control |
| Few-Shot Prompting | Format conditioning via examples |
| Delimiters (###) | Instruction-data isolation |
| JSON Schema | Output validation contract |

---

## 💡 Key Learnings

- Prompting is programming. A prompt is a set of executable instructions — not a question.
- Temperature is a control variable. 0.0 eliminates hallucination in structured pipelines.
- Delimiters prevent injection. Without them, email content can override system instructions.
- Positive constraints outperform negative ones. "Output JSON only" beats "Do not include filler."
- Few-shot beats zero-shot for precision. 2–3 examples push accuracy from ~60% to over 99%.
- Null fallback logic is non-negotiable. Missing data must return null — never a guess.

---

## 👤 Author

**Precious Adeyemi**
