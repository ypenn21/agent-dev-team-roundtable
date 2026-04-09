# Project: Universal Gemini Swarm

This workspace utilizes a **Stack-Agnostic Multi-Agent Swarm** for autonomous software development. The swarm follows a rigorous **Plan -> Act -> Verify** state machine, ensuring quality and consistency across any programming language or runtime.

## 🤖 The Swarm Architecture

Managed by the **Supervisor** (`system.md`), the swarm coordinates three specialized agents:

1.  **Architect (`agents/architect.md`)**: The Planner. Investigates the codebase and creates TDD implementation plans in `plans/`.
2.  **Engineer (`agents/engineer.md`)**: The Builder. Executes plans using strict Red-Green-Refactor TDD.
3.  **Auditor (`agents/auditor.md`)**: The Gatekeeper. Verifies code against the plan, ensures tests pass, and prevents "AI shortcuts".

---

## ⚙️ Stack & Runtime Configuration

To enable the swarm to work with your specific technology stack, you **MUST** define your project's commands below. The agents will read this file to determine how to build, test, and deploy your application.

### Technical Stack
- **Language/Framework:** TypeScript/Node.js (for CLI extension)
- **Testing Framework:** Vitest
- **Runtime Environment:** Gemini CLI

### Project Commands
- **Build Command:** `npm run build`
- **Test Command:** `npm test`
- **Lint/Check Command:** `npm run lint`
- **Deployment Command:** `gemini extensions install .`

---

## 🏗️ The Swarm Lifecycle

1.  **Discovery**: Dispatch the `codebase_investigator` to map the architecture and stack.
2.  **Strategic Planning**: The Architect updates the `plans/00_MASTER_ROADMAP.md`.
3.  **Tactical Planning**: The Architect creates detailed task plans in `plans/TASK_ID_NAME.md`.
4.  **Human Review Gate**: **STOP.** User must approve the plan and stack config.
5.  **Construction Loop**:
    - **Engineer**: Implements the plan step-by-step using strict Red-Green-Refactor.
    - **Auditor**: Verifies the implementation using the **Project Commands** above.
6.  **Git & Deployment**:
    - **Supervisor**: Manages the `git commit` process (after user approval).
    - **Supervisor**: Executes the **Deployment Command** and verifies health.

---

## 🛠️ Development Conventions

- **Protocol over Speed**: Never skip steps in the state machine.
- **Artifact-Driven**: The `plans/` directory is the Single Source of Truth.
- **Strict Sub-Agent Delegation**:
    - Use `codebase_investigator` for all architectural research and bug analysis.
    - Use `generalist` for repetitive batch tasks or high-volume test fixing.
- **TDD Mandatory**: Write the test first. No code without a corresponding test.
- **Zero Placeholders**: Never allow `TODO`, `FIXME`, or stubbed implementations.
- **Atomic Commits**: Every task implementation is verified and committed individually.

## 🚀 Getting Started

1.  **Initialize**: Run `/swarm:init` to download the Supervisor (`system.md`). (Note: Client projects must provide their own `GEMINI.md` in root or `.gemini/`).
2.  **Configure**: Ensure your `GEMINI.md` defines your technology stack and commands.
3.  **Activate**: Run the CLI with `GEMINI_SYSTEM_MD=true gemini`.
4.  **Execute**: Ask the swarm to "Start a new task" or "Map the project".
