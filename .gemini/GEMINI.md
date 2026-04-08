# Project: Gemini Swarm & Modernization Toolkit

This project is a comprehensive **Gemini CLI Extension** that provides a **Multi-Agent Swarm** for autonomous software development and a specialized

## 🤖 The Multi-Agent Swarm

The swarm operates using a rigorous **Plan -> Act -> Verify** state machine, managed by a **Supervisor** (`system.md`).

### Swarm Roles
- **Supervisor (`system.md`)**: The Project Manager. Enforces the protocol, manages agent hand-offs, and gates Git commits.
- **Architect (`agents/architect.md`)**: The Planner. Performs deep investigation and creates detailed TDD implementation plans in the `plans/` directory.
- **Engineer (`agents/engineer.md`)**: The Builder. Implements the Architect's plans using strict Red-Green-Refactor TDD.
- **Auditor (`agents/auditor.md`)**: The Gatekeeper. Verifies the Engineer's work, ensuring tests pass and no "AI shortcuts" (like TODOs or `NotImplementedException`) exist.

### Swarm Lifecycle
1.  **Strategic Discovery**: Map the system architecture.
2.  **Strategy (Architect)**: Update the `plans/00_MASTER_ROADMAP.md`.
3.  **Tactical Planning (Architect)**: Create detailed task plans (e.g., `plans/feat_xyz.md`).
4.  **Human Review Gate**: **STOP.** User must approve the plan before execution.
5.  **Construction Loop (Engineer ⇄ Auditor)**: Iterate through tasks. Verify each step.
6.  **Git Protocol (Supervisor)**: Final review and user approval before `git commit`.

---

## 🏗️ DDD Refactoring Workflow

A specialized pipeline for transforming legacy SQL logic into modern .NET 10 architectures.

### Key Commands
- `/sql:analyze {{path}}`: Extracts business rules and data dictionaries from SQL.
- `/ddd:logical {{path}}`: Generates a Domain Model (Aggregates, Entities).
- `/ddd:physical {{path}}`: Maps the domain to .NET 10, MediatR, and EF Core.
- `/ddd:plan {{path}}`: Generates a TDD-based implementation plan.
- `/ddd:implement {{path}}`: Executes the plan and writes the code.
- `/ddd:review`: Audits the generated code for quality and completeness.
- `/ddd:fix {{path}}`: Automatically remediates issues found during review.

---

## 🛠️ Development Conventions & Standards

- **Test-Driven Development (TDD)**: All code changes must be preceded by a verification harness (Red-Green-Refactor).
- **Production-Ready**: Placeholders like `// TODO`, `throw new NotImplementedException()`, or `return default;` are strictly forbidden.
- **Clean Architecture**: Follow DDD principles. Maintain a clear separation between Domain, Application, Infrastructure, and API layers.
- **Micro-Stepping**: Break implementation plans into the smallest possible logical chunks.
- **Artifact-Driven**: Use files in the `plans/` directory as the Single Source of Truth for agent coordination.

---

## ⚙️ Workspace Configuration

### Initialization
To use the Swarm in a project, initialize the local `.gemini/system.md` file:
```bash
/swarm:init
```

### Activation
The Supervisor is activated by setting the `GEMINI_SYSTEM_MD` environment variable:
```bash
GEMINI_SYSTEM_MD=true gemini
```

### Context Management
To keep the AI's context window clean, use the archive command:
```bash
/swarm:archive
```
This moves completed tasks from `plans/` to `plans/archive/` and updates `.geminiignore`.

### Required Directories
- `plans/`: Stores the Roadmap, research, and task-specific plans.
- `src/` & `tests/`: Standard locations for implementation and verification logic.
