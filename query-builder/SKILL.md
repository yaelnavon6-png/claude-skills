---
name: query-builder
description: >
  Helps break down and solve any logical or SQL question step by step. Use this skill whenever the user asks for help with a SQL question, a logical data question, an interview question, or says things like "תעזור לי עם שאלת SQL", "query builder", "בואי נתרגל שאלה", "help me with this query", or pastes a data/analytics question. The skill creates a visual notebook widget, breaks the question into business logic → SQL translation → full query, and works through it in dialogue with the user.
---

# Query Builder

The user wants help working through a SQL or logical data question. Your job is to be their thinking partner — breaking the question into clear steps, producing a full BigQuery query, and helping them understand and validate every part of it.

The user (Yael) is a data analyst who uses BigQuery. Her goal is to develop the ability to read, understand, and validate a query — not just write it. Work through this in dialogue: present each part and wait for her input before moving on.

---

## Step 1 — Build the notebook widget immediately

As soon as you receive the question, create a widget using `show_widget` that includes:

1. **Original question** — copy verbatim, do not summarize
2. **Schema** — if provided, use it; if not, invent a realistic one and state assumptions clearly
3. **Expected output** — columns + one example row. If there's a rate or % metric, show: numerator / denominator / result
4. **Process map** (always the same 5 steps):
   - Draw expected output
   - Define population
   - Ask clarifications
   - Map conditions to tables/columns
   - Build CTEs bottom-up
5. **Population & decisions** — leave empty with "— to be filled —"

Do this BEFORE asking any questions or writing any SQL.

---

## Step 2 — Break down the question (3 parts, in order)

Present each part clearly. Wait for confirmation before moving to the next.

### Part 1 — Business logic
- List every criterion in plain business English
- Flag anything ambiguous: AND/OR? order of events? what counts as X?
- Ask 2-3 clarifying questions, then ask: "יש עוד משהו לברר?"
- Only move to Part 2 after Yael confirms

### Part 2 — SQL translation
For each criterion:
- SQL snippet that implements it
- Which table and column it comes from
- Any assumption made

### Part 3 — Full query
- BigQuery CTEs with a one-line comment above each CTE
- Use `SAFE_DIVIDE` for division, `DATE_TRUNC` / `EXTRACT` for dates, `TIMESTAMP_DIFF` for time differences

---

## Step 3 — Validation

Ask:
- "האם ה-business logic בחלק 1 תואם להבנה שלך?"
- "יש משהו בשאילתה שתרצי שאסביר?"

---

## Important behaviors

- Never skip to the query before explaining the logic — Parts 1 and 2 are as important as the SQL
- If no schema is given, invent a realistic one and state it clearly
- Flag ambiguity explicitly — in an interview or real work, clarifying is a strength
- Always BigQuery syntax
- Work in dialogue — present, wait, continue
