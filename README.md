# Software Engineering Agent Playbook

A tool-agnostic library of **agents**, **instructions**, and **skills** for AI software engineering assistants — plus thin adapters that map the core definitions to Claude Code, GitHub Copilot, Cursor, and others.

The playbook covers the full software development lifecycle — from requirements and architecture through implementation, testing, security, deployment, operations, and documentation. Each SDLC stage has a dedicated agent with its own instructions and skills, so no stage is a gap and no agent carries responsibility beyond its scope.

As AI agents take over execution — writing code, generating tests, running pipelines — developer value concentrates at the flanks: the **prework** of discovery, problem framing, and decision-making, and the **postwork** of verifying agent output, owning outcomes, and building stakeholder trust. This playbook covers all three phases.

## Model

Three distinct layers:

| Layer | Location | Loaded | Purpose |
|---|---|---|---|
| **Instructions** | `core/instructions/` | Always, per agent | Behavior rules specific to each agent's role |
| **Skills** | `core/skills/<agent>/` | On demand | Task execution invoked when needed |
| **Adapters** | `adapters/` | — | Maps core to each tool's native format |

Instructions define how an agent **behaves**. Skills define what an agent **does**. Adapters translate both into the format each tool understands — with no content of their own.

## Phase Model

Every agent's skills fall into one of three phases. Agents own the prework and postwork phases; AI handles execution.

| Phase | Human or AI | What happens |
|---|---|---|
| **Prework** | Human | Discovery, problem framing, constraints, deciding what and why to build |
| **Work** | AI agents | Implementation, test generation, code review, deployment |
| **Postwork** | Human | Verifying agent output, owning outcomes, building stakeholder trust |

## Agents

Eight agents cover the full software development lifecycle:

| Agent | Phase emphasis | Instructions | Skills |
|---|---|---|---|
| **Business Analyst** | Prework | communication | requirements-gathering, user-story, prd-writing, process-analysis, roadmap, sprint-planning, estimation, innovation-discovery |
| **Technical Architect** | Prework | coding-standards, security, communication | system-design, architecture-review, adr-writing, technical-spec, feasibility-analysis |
| **Software Engineer** | Work + Postwork | coding-standards, security | code-review, agent-output-review, debugging, refactoring, spec-writing, tech-debt, dependency-update, migration, intrapreneur-workflow |
| **QA Engineer** | Postwork | coding-standards, security | test-planning, test-writing, bug-report, performance-testing, exploratory-testing |
| **Security Engineer** | Postwork | security, coding-standards | security-audit, threat-modeling, vulnerability-assessment, dependency-vulnerability, compliance-review |
| **DevOps Engineer** | Work | coding-standards, security | pipeline-design, deployment, infrastructure-as-code, containerization, build-optimization |
| **SRE** | Postwork | coding-standards, security | observability, alerting, incident-response, post-mortem, capacity-planning, runbook, root-cause-analysis |
| **Technical Writer** | Postwork | communication | api-docs, user-guide, runbook-writing, onboarding-guide, changelog, stakeholder-trust |

Together the eight agents span the full SDLC: requirements → architecture → implementation → testing → security → deployment → operations → documentation. Each agent loads only its own instructions. Available skills are declared in the agent's `SKILLS.md` — a QA Engineer has no awareness of deployment skills, and vice versa.

## Skill Hierarchy

Skills are either **atomic** (single responsibility) or **composite** (invoke other skills):

```
core/skills/software-engineer/
  code-review.md          ← atomic: reviews human-authored code against standards
  agent-output-review.md  ← atomic: verifies AI-generated code for drift, logic gaps, missing edge cases
  debugging.md            ← atomic: diagnoses and fixes a specific bug
  ship-feature.md         ← composite: spec-writing → code-review → testing
  intrapreneur-workflow.md ← composite: innovation-discovery → spec-writing → build → agent-output-review → stakeholder-trust
```

Composite skills reference sub-skills via imports. Atomic skills stay self-contained and are reused by composites without duplication. This hierarchy means complex workflows are built by composition, not by writing monolithic prompts.

## Adapters

Adapters are thin by design — each one imports from `core/` using the tool's native syntax:

| Tool | Native format | Import mechanism |
|---|---|---|
| Claude Code | `.claude/agents/*.md` with YAML frontmatter | `@path/to/file` |
| GitHub Copilot | `.github/` chat participants | Tool-specific |
| Cursor | `.cursor/rules/*.md` | `@path/to/file` |

No content lives in adapters. Updating a core skill or instruction is automatically reflected in all adapters that import it.

## Structure

### Behavioral Sources

One file per agent at the root — the human-readable behavioral guidelines that feed each `agent.md`:

```
business-analyst.md
developer.md              ← software engineer
technical-architect.md
qa-engineer.md
security-engineer.md
devops-engineer.md
sre.md
technical-writer.md
```

### Core

```
core/
  agents/
    business-analyst/
      agent.md            ← role, instructions, pointer to SKILLS.md
      SKILLS.md           ← index of skills this agent can invoke
    technical-architect/
      agent.md
      SKILLS.md
    software-engineer/
      agent.md
      SKILLS.md
    qa-engineer/
      agent.md
      SKILLS.md
    security-engineer/
      agent.md
      SKILLS.md
    devops-engineer/
      agent.md
      SKILLS.md
    sre/
      agent.md
      SKILLS.md
    technical-writer/
      agent.md
      SKILLS.md

  skills/
    business-analyst/
      requirements-gathering.md
      user-story.md
      prd-writing.md
      process-analysis.md
      roadmap.md
      sprint-planning.md
      estimation.md
      innovation-discovery.md   ← explore unspoken needs before a ticket exists
    technical-architect/
      system-design.md
      architecture-review.md
      adr-writing.md
      technical-spec.md
      feasibility-analysis.md
    software-engineer/
      code-review.md
      agent-output-review.md    ← postwork: verify AI-generated code
      debugging.md
      refactoring.md
      spec-writing.md
      tech-debt.md
      dependency-update.md
      migration.md
      ship-feature.md           ← composite
      intrapreneur-workflow.md  ← composite: discovery → spec → build → review → trust
    qa-engineer/
      test-planning.md
      test-writing.md
      bug-report.md
      performance-testing.md
      exploratory-testing.md
    security-engineer/
      security-audit.md
      threat-modeling.md
      vulnerability-assessment.md
      dependency-vulnerability.md
      compliance-review.md
    devops-engineer/
      pipeline-design.md
      deployment.md
      infrastructure-as-code.md
      containerization.md
      build-optimization.md
    sre/
      observability.md
      alerting.md
      incident-response.md
      post-mortem.md
      capacity-planning.md
      runbook.md
      root-cause-analysis.md
    technical-writer/
      api-docs.md
      user-guide.md
      runbook-writing.md
      onboarding-guide.md
      changelog.md
      stakeholder-trust.md      ← postwork: communicate outcomes, build trust after agent work

  instructions/
    coding-standards.md
    security.md
    communication.md

adapters/
  claude/
  copilot/
  cursor/
```

## Quick Start

**Claude Code** — copy `adapters/claude/` into your project as `.claude/agents/`

**GitHub Copilot** — copy `adapters/copilot/` files into `.github/`

**Cursor** — copy `adapters/cursor/` files into `.cursor/rules/`

## Principles

- **Tool-agnostic core**: all content lives in `core/`, adapters contain no content
- **Non-redundant**: each instruction and skill has one authoritative source
- **On-demand skills**: skills are invoked when needed, never always-loaded
- **Composable**: atomic skills combine into composite skills without duplication
- **Agent-scoped instructions**: each agent loads only the instructions relevant to its role
- **Full-phase coverage**: every workflow covers prework (discovery, framing), work (execution), and postwork (verification, accountability) — AI handles execution, humans own the flanks

## Contributing

1. All content goes in `core/` — never in `adapters/`
2. Skills go in `core/skills/<agent>/` — never nested inside `core/agents/`
3. Skills must be either atomic (single task) or explicitly composite (declare which sub-skills they invoke)
4. New agents must declare which instructions they import in `agent.md` and list available skills in `SKILLS.md`
5. Adapters require no manual updates — they reflect `core/` automatically via imports

## License

MIT — see LICENSE file
