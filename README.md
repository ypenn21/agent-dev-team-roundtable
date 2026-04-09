# Universal Gemini Swarm & Modernization Toolkit

A comprehensive Gemini CLI Extension that provides a **Multi-Agent Swarm** for autonomous software development, alongside specialized, **stack-agnostic** pipelines for **Feature Planning** and **SQL-to-DDD Refactoring**.

**See** [Gemini CLI Extensions](https://github.com/google-gemini/gemini-cli/blob/main/docs/extensions/index.md) for more details.

**Credits**: [@dandobrin](https://github.com/ddobrin), [@jjdelorme](https://github.com/jjdelorme) & [@cedricyao](https://github.com/cedricyao). Parts of this work were adapted from Dan's [production serverless repository](https://github.com/GoogleCloudPlatform/serverless-production-readiness-java-gcp/tree/main/genai/quotes-llm/.gemini/commands), and Jason's [plan-commands](https://github.com/jjdelorme/plan-commands)

## Prerequisites
Install the [Gemini CLI](https://github.com/google-gemini/gemini-cli)

## Extension Installation
From your command line:

```bash
gemini extensions install https://github.com/ypenn21/agent-dev-team-roundtable.git
```

### Activating the Swarm Supervisor (Per-Workspace)

While the agents (`architect`, `engineer`, `auditor`) are installed globally by the extension, the **Supervisor** (`system.md`) must be activated locally in each project you want to use it in.

1. Navigate to your project directory.
2. Run the initialization command:
   ```bash
   /swarm:init
   ```
   *(This downloads the `system.md` file into your local `.gemini/` folder and a `GEMINI.md` template into your root).*
3. **Restart** the Gemini CLI with the system override enabled:
   ```bash
   GEMINI_SYSTEM_MD=true gemini
   ```

---

## 🤖 1. The Autonomous Swarm

This extension packages a portable, framework-agnostic AI agent swarm designed to manage the software development lifecycle using a rigorous **Plan -> Act -> Verify** state machine.

### The Agents
*   **Supervisor (`system.md`)**: The Project Manager. Enforces the state machine, manages hand-offs, and gates Git commits.
*   **Architect (`architect`)**: The Planner. Reads research, creates comprehensive step-by-step TDD implementation plans in the `plans/` directory.
*   **Engineer (`engineer`)**: The Builder. Strictly follows the Architect's plans, writing tests and implementing changes via Red-Green-Refactor.
*   **Auditor (`auditor`)**: The Gatekeeper. Verifies the Engineer's work. Compiles code, runs tests, and hunts for lazy AI shortcuts (TODOs, commented-out tests).

### 🔄 Protocol Lifecycle
The system moves through distinct phases, enforced by the Supervisor.

```mermaid
graph TD
    %% Roles
    subgraph Phase 1 & 2: Strategy
        Scout[Scout/Investigator: Research & Map]
        Architect[Architect: Plan & Strategy]
    end

    subgraph Phase 3: Construction
        Engineer[Engineer: Implement]
        Auditor[Auditor: Verify]
    end

    %% Flow
    Start([User Start]) --> Scout
    Scout --> Architect
    Architect --> Review{User Approval}
    
    Review -- Reject --> Architect
    Review -- Approve --> Engineer
    
    Engineer --> Auditor
    
    %% The Three-Way Fork
    Auditor -- Code Broken? --> Engineer
    Auditor -- Plan Wrong? --> Architect
    Auditor -- Verified --> Commit([Git Commit])
    
    Commit --> Engineer
```

### Workspace Maintenance: Archiving Plans
As the Swarm executes tasks, your `plans/` directory will accumulate executed task files, research reports, and review feedback. To keep the agent's context window clean and focused, you can archive completed items:

```bash
/swarm:archive
```

---

## 🏗️ 2. Generic Feature Planning & Implementation
A universal, stack-agnostic workflow for designing and building any software feature (API endpoints, UI components, IaC, scripts, etc.).

### The Workflow
**CRITICAL:** This pipeline is artifact-driven. After every step, review the output, then type `/clear`.

#### Step 1: Strategic Planning (User Stories)
*Analyze the requirement and generate INVEST-compliant user stories.*
- **Command:** `/plan:create-user-stories {{feature_description_or_path}}`
- **Output:** `USER_STORIES.md`

#### Step 2: Tactical Planning (Execution Plan)
*Translate user stories into a step-by-step TDD implementation plan.*
- **Command:** `/plan:plan {{USER_STORIES.md}}`
- **Output:** `IMPLEMENTATION_PLAN.md`

#### Step 3: Construction (Build)
*Execute the plan step-by-step using strict TDD.*
- **Command:** `/plan:implement {{IMPLEMENTATION_PLAN.md}}`
- **Output:** Source code and tests.

#### Step 4: Quality Gate (Review & Fix)
*Audit the code and remediate issues until PASS.*
- **Review Command:** `/plan:review {{USER_STORIES.md}}`
- **Fix Command:** `/plan:fix {{REVIEW_REPORT.md}}`

---

## 🏗️ 3. DDD Refactoring Commands (SQL-to-Modernization)
A specialized workflow for refactoring legacy code (specifically SQL) into a modern, **Domain-Driven Design (DDD)** architecture.

**Architecture:** Stack-Agnostic (supports .NET, Java, Go, Python, TypeScript, etc. via `GEMINI.md`).
**Methodology:** Domain-Driven Design (DDD) via Test-Driven Development (TDD).

### The Workflow
#### Step 1: Deep Analysis (SQL)
- **Command:** `/sql:analyze {{path/to/legacy_proc.sql}}`
- **Output:** `ANALYSIS_[ProcName].md`

#### Step 2: Logical & Physical Architecture
- **Logical Command:** `/ddd-sql-transformation:logical {{ANALYSIS_[ProcName].md}}`
- **Physical Command:** `/ddd-sql-transformation:physical {{LOGICAL_ARCHITECTURE.md}}`

#### Step 3: Implementation Planning
- **Command:** `/ddd-sql-transformation:plan {{PHYSICAL_ARCHITECTURE.md}}`
- **Output:** `IMPLEMENTATION_PLAN.md`

#### Step 4: Build & Implementation
- **Command:** `/ddd-sql-transformation:implement {{IMPLEMENTATION_PLAN.md}}`
- **Output:** Actual source code and tests.

#### Step 5: Review & Fix
- **Review Command:** `/ddd-sql-transformation:review`
- **Fix Command:** `/ddd-sql-transformation:fix {{REVIEW_REPORT.md}}`
