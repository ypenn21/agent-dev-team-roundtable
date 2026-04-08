# Generic Feature Planning & Implementation Pipeline

A universal, stack-agnostic workflow for designing and building any software feature (API endpoints, UI components, IaC, scripts, etc.). This pipeline uses `GEMINI.md` as the source of truth for your project's technical commands.

## 📋 Prerequisites
1. **GEMINI.md:** Must exist in the root and define your `Technical Stack` and `Project Commands`.
2. **Feature Input:** A description, design doc, or path to existing code for the new capability.

## 🔄 The Planning Workflow
This pipeline is state-sensitive and artifact-driven.

### Step 1: Strategic Planning (User Stories)
*Analyze the requirement and generate INVEST-compliant user stories with Gherkin scenarios.*
- **Command:** `/plan:create-user-stories {{feature_description_or_path}}`
- **Output:** `USER_STORIES.md`

### Step 2: Tactical Planning (Execution Plan)
*Translate user stories into a step-by-step TDD implementation plan.*
- **Command:** `/plan:plan {{USER_STORIES.md}}`
- **Output:** `IMPLEMENTATION_PLAN.md`

### Step 3: Construction (Build)
*Execute the plan step-by-step using strict TDD.*
- **Command:** `/plan:implement {{IMPLEMENTATION_PLAN.md}}`
- **Output:** Source code and tests.

---

## 🛡️ The Quality Assurance Loop

### Step 4: Quality Gate (Review)
*Audit the code for architectural integrity and business logic compliance.*
- **Command:** `/plan:review {{USER_STORIES.md}}`
- **Output:** `REVIEW_REPORT.md`

### Step 5: Self-Healing (Fix)
*Remediate blocking issues found in the review.*
- **Command:** `/plan:fix {{REVIEW_REPORT.md}}`
- **Next Step:** Return to **Step 4** (`/plan:review`) until you receive a **PASS**.

## 💡 Best Practices
1. **Zero Placeholders:** The agents are strictly forbidden from writing `TODO` or stubs.
2. **Test First:** No code is written without a corresponding test case.
3. **Artifact-Driven:** Use the generated Markdown files as the single source of truth for the development cycle.
