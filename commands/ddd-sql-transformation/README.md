# Legacy SQL to DDD Refactoring Pipeline (Generic Stack)

**Methodology:** Domain-Driven Design (DDD) via Test-Driven Development (TDD).
**Enforcement:** Strictly controlled by `GEMINI.md` in the project root.

## 📋 Prerequisites

1.  **Project Configuration:** You must have a `GEMINI.md` file in your root defining your `Technical Stack` and `Project Commands`.
2.  **Extension Commands:**
    *   `/sql:analyze` (SQL Analysis)
    *   `/ddd-sql-transformation:create-user-stories` (Agile Prep)
    *   `/ddd-sql-transformation:logical` (Logical Arch)
    *   `/ddd-sql-transformation:physical` (Physical Arch)
    *   `/ddd-sql-transformation:plan` (Implementation Plan)
    *   `/ddd-sql-transformation:implement` (Build Agent)
    *   `/ddd-sql-transformation:review` (Quality Gate)
    *   `/ddd-sql-transformation:fix` (Remediation)

## 🔄 The Workflow Overview

**CRITICAL:** This pipeline is state-sensitive. After every step, review the output artifact, then type `/clear` to reset the context window. This prevents "Context Pollution."

---

### Step 1: Deep Analysis
*Extracts business rules and test cases from the legacy Stored Procedure.*

*   **Command:** `/sql:analyze {{path/to/legacy_proc.sql}}`
*   **Input:** Raw SQL file.
*   **Output:** `ANALYSIS_[ProcName].md`
*   **Reset:** `/clear`

### Step 2: Logical Architecture
*Transforms the Analysis into a pure Domain Model (Aggregates, Entities, Rules).*

*   **Command:** `/ddd-sql-transformation:logical {{ANALYSIS_[ProcName].md}}`
*   **Input:** The Analysis Markdown file.
*   **Output:** `LOGICAL_ARCHITECTURE.md`
*   **Reset:** `/clear`

### Step 3: Physical Architecture
*Maps the Domain Model to the technology stack defined in `GEMINI.md`.*

*   **Command:** `/ddd-sql-transformation:physical {{LOGICAL_ARCHITECTURE.md}}`
*   **Input:** Logical Architecture Markdown.
*   **Output:** `PHYSICAL_ARCHITECTURE.md`
*   **Reset:** `/clear`

### Step 4: Implementation Planning
*Generates a step-by-step TDD execution plan with hygiene checks.*

*   **Command:** `/ddd-sql-transformation:plan {{PHYSICAL_ARCHITECTURE.md}}`
*   **Input:** Physical & Logical Architectures.
*   **Output:** `IMPLEMENTATION_PLAN.md`
*   **Reset:** `/clear`

### Step 5: Build & Implementation
*Executes the plan using strict Red-Green-Refactor TDD.*

*   **Command:** `/ddd-sql-transformation:implement {{IMPLEMENTATION_PLAN.md}}`
*   **Input:** The Plan, plus read-access to all 3 Architecture/Analysis docs.
*   **Output:** Actual source code in `src/` and tests in `tests/` (following your project's conventions).
*   **Reset:** `/clear`

---

## 🛡️ The Quality Assurance Loop

Once the code is built, do not ship it. Enter the **Review/Fix Loop**.

### Step 6: Code Review (Quality Gate)
*Audits the code for "Laziness", Stubbing, and missing Business Rules.*

*   **Command:** `/ddd-sql-transformation:review`
*   **Input:** The full codebase + `ANALYSIS.md`.
*   **Output:** `REVIEW_REPORT.md`
*   **Status:** Look for `🔴 REJECT` or `🟢 PASS`.
*   **Reset:** `/clear`

### Step 7: Remediation (Self-Healing)
*If Step 6 failed, this agent fixes the specific issues listed in the report.*

*   **Command:** `/ddd-sql-transformation:fix {{REVIEW_REPORT.md}}`
*   **Input:** The Review Report.
*   **Output:** Modified source code.
*   **Next Step:** Go back to **Step 6** (`/ddd-sql-transformation:review`) and run the Review again. Repeat until **PASS**.
*   **Reset:** `/clear`

---

## 📂 Artifacts Reference

| File | Purpose | Source of Truth For... |
| :--- | :--- | :--- |
| `ANALYSIS_*.md` | Legacy Deconstruction | **Test Data** (Inputs/Outputs) |
| `LOGICAL_*.md` | Domain Design | **Business Rules** (Invariants) |
| `PHYSICAL_*.md` | Tech Spec | **Structure** (Classes, Patterns) |
| `IMPLEMENTATION_*.md` | Task List | **Sequence** (What to do next) |
| `REVIEW_REPORT.md` | Audit Log | **Defects** (What to fix) |

## 💡 Pro Tips for Best Results
1.  **Read the Analysis:** The quality of the entire build depends on Step 1. If the Analysis misses a rule, the code will miss it too.
2.  **Don't Combine Contexts:** Always `/clear`. If you feed the Implementation Agent (`/ddd-sql-transformation:implement`) the raw SQL from Step 1, it might hallucinate legacy patterns into your clean code.
3.  **Strict TDD:** The agent will only be as good as the tests it writes. Verify the test command in `GEMINI.md` is correct.
