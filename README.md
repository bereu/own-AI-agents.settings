# AI Agent Primitives & Settings

This repository houses custom AI agent profiles, workflows, skills, guidelines, and quality assurance configurations managed by the **Agent Package Manager (APM)**. It defines and builds agentic structures for platforms like Claude and Copilot.

---

## 📂 Project Structure

The project relies on a modular directory structure under `.apm` to maintain clean separation of concerns for agent primitives:

```text
├── apm.yml                 # APM configuration, targets, and dependencies
├── .apm/
│   ├── agents/             # Agent definitions & system instructions (e.g., Planner, Executor, Validator)
│   ├── hooks/              # Automation gates and lifecycle rules (hooks.json)
│   ├── instructions/       # Development flows, code review rules, and naming guides
│   └── skills/             # Reusable skill definitions (e.g., qa-features-skills, plan-coding)
```

- **`apm.yml`**: Defines the package name, targets (e.g., `claude`, `copilot`), and external APM or MCP dependencies.
- **`.apm/agents/`**: Contains frontmatter-configured markdown profiles defining agent behavior and active tools.
- **`.apm/skills/`**: Composable skills detailing operational guidelines and checklists that agents execute for specific tasks.
- **`.apm/hooks/`**: Defines post-tool execution triggers to enforce linting, validation, and testing rules automatically.

---

## 🚀 Getting Started

### 1. Prerequisites
Ensure the `apm` CLI is installed on your local system:
```bash
apm --version
```

### 2. Installation

#### A. Local Development Setup
To install all package dependencies and MCP servers defined locally in your `apm.yml`:
```bash
apm install
```

#### B. Installation in Other Projects
To consume these agent primitives, skills, and settings in another project, install them directly from this GitHub repository using the APM CLI:

```bash
# Install the entire settings bundle
apm install bereu/own-AI-agents.settings 
```
```bash
# Install the entire settings bundle to claude
apm install bereu/own-AI-agents.settings --target claude
```
```bash
# Install only a specific skill (e.g., plan-coding) from this bundle
apm install bereu/own-AI-agents.settings --skill plan-coding
```


### 3. Compilation
Compile local agent primitives and custom instructions into distributed files for your configured targets:
```bash
apm compile
```
- Use `apm compile --validate` to verify syntax and schema correctness.
- Use `apm compile --dry-run` to preview compile decisions and placement layouts without writing changes.

### 4. Code Quality & Hooks
This repository utilizes standard validation hooks defined in `.apm/hooks/hooks.json`. When local tools execute writes/edits or when workflows complete, quality gates (such as linting and checking Storybook configurations) are run automatically to ensure compliance.
