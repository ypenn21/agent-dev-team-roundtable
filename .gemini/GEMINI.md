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
- **Language/Framework:** [e.g., TypeScript/Node.js, Go, Python/FastAPI, Rust]
- **Testing Framework:** [e.g., Vitest, Pytest, Go Test]
- **Runtime Environment:** [e.g., Cloud Run (Serverless), GKE (Kubernetes), GCE (Compute Engine), AWS Lambda]

### Project Commands
- **Build Command:** `[e.g., npm run build, go build ./...]`
- **Test Command:** `[e.g., npm test, pytest]`
- **Lint/Check Command:** `[e.g., npm run lint, ruff check .]`
- **Deployment Command:** `[e.g., gcloud run deploy, kubectl apply -f k8s/]`

---

## 🏗️ The Swarm Lifecycle

1.  **Discovery**: Dispatch a scout to map the architecture and stack.
2.  **Strategic Planning**: The Architect updates the `plans/00_MASTER_ROADMAP.md`.
3.  **Tactical Planning**: The Architect creates detailed task plans (e.g., `plans/feat_auth.md`).
4.  **Human Review Gate**: **STOP.** User must approve the plan and stack config.
5.  **Construction Loop**:
    - **Engineer**: Implements the plan step-by-step, writing tests first.
    - **Auditor**: Verifies the implementation using the **Project Commands** above.
6.  **Git & Deployment**:
    - **Supervisor**: Manages the `git commit` process (after user approval).
    - **Supervisor**: Executes the **Deployment Command** and verifies runtime health.

---

## 🛠️ Development Conventions

- **TDD Mandatory**: No code is written without a corresponding test.
- **Zero Placeholders**: No `TODO`, `FIXME`, or `NotImplementedException`.
- **Atomic Commits**: Every task implementation is verified and committed individually.
- **Artifact-Driven**: The `plans/` directory is the Single Source of Truth.

## 🚀 Getting Started

1.  **Initialize**: Run `/swarm:init` to download the Supervisor.
2.  **Configure**: Update the **Project Commands** section in this `GEMINI.md` file.
3.  **Activate**: Run the CLI with `GEMINI_SYSTEM_MD=true gemini`.
4.  **Execute**: Ask the swarm to "Start a new task" or "Map the project".
