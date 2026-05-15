# Skill Schema Definition

Every `SKILL.md` file MUST follow this exact structure to support portable AI-agent execution, cross-agent compatibility, and deterministic workflows.

## Frontmatter Metadata

All skills MUST begin with YAML frontmatter containing machine-readable metadata:

```yaml
---
# Identification
name: skill-name-kebab-case
description: Single-sentence summary of when and why to use this skill
version: x.x.x

# Classification
category: [frontend|backend|architecture|dev-tools|ui-ux|code-quality]
tags: [keyword1, keyword2, keyword3]
skill_type: [workflow|architecture|security|debugging|review|generation|migration]

# Authorship & Licensing
author: GitHub username or team
license: MIT

# Agent Compatibility
compatible_agents: [claude-code, cursor, copilot, codex]
estimated_context_tokens: 1200

# Execution Safety & Requirements
dangerous: false
requires_review: false
security_level: [safe|review-required|dangerous]

# Dependencies & Composition
dependencies: [related-skill-name]
triggers: [keyword1, keyword2]

# Operational Constraints
permissions:
  filesystem:
    read: true
    write: false
  network:
    outbound: false
  shell:
    execute: false

# Contracts & Validation
input_requirements: [existing codebase, frontend html]
output_contract: [no inline scripts, csp enforced]
failure_conditions: [required library unavailable, legacy framework conflict]

# Metadata
last_updated: YYYY-MM-DD
---
```

## Required Sections (in order)

### 1. Purpose
Clear, single-paragraph explanation of what this skill achieves and why it matters.

### 2. When to use
Bulleted list of exact conditions triggering this skill:
- Specific scenario 1
- Specific scenario 2

### 3. When NOT to use
Bulleted list of scenarios where this skill does NOT apply:
- Anti-use case 1
- Anti-use case 2

### 4. Inputs required
Bulleted list of prerequisites:
- Required input 1
- Required input 2

### 5. Workflow
Numbered, actionable steps:
1. [Specific, imperative instruction]
2. [Next step with clear outcome]
3. [Verify result state]

### 6. Rules
Imperative, non-negotiable constraints:
- MUST/NEVER statements only
- Use strong language: "must," "required," "prohibited"

### 7. Anti-patterns
Specific mistakes to avoid with explanations:
- **Anti-pattern Name**: Description of why it fails

### 8. Failure conditions
Critical situations requiring agent abort:
- Condition 1 (agent must stop)
- Condition 2 (agent must reject execution)

### 9. Validation checklist
Concrete, testable verification items:
- [ ] Specific check 1
- [ ] Specific check 2

### 10. Output format
Strict definition of expected output:
- File structure
- Code style
- Format examples

### 11. Security considerations
Explicit security guidance:
- Threat model (if applicable)
- Mitigations
- Constraints

### 12. Agent execution notes
Explicit instructions for AI agents:
- What agent may modify
- What agent must never modify
- What requires confirmation
- What must be validated

### 13. Example
Real-world, before/after, or concrete code example:
- ❌ Anti-pattern example
- ✅ Correct pattern example

---

## Template

```markdown
---
name: skill-name-kebab-case
description: Single-sentence summary
version: 1.0.0
category: [category]
tags: [tag1, tag2]
skill_type: [workflow]
author: username
license: MIT
compatible_agents: [claude-code, cursor, copilot]
estimated_context_tokens: 1200
dangerous: false
requires_review: false
security_level: safe
dependencies: []
triggers: []
permissions:
  filesystem: { read: true, write: false }
  network: { outbound: false }
  shell: { execute: false }
input_requirements: []
output_contract: []
failure_conditions: []
last_updated: 2026-05-15
---

# Skill Title

## Purpose
[Single paragraph explaining purpose and value]

## When to use
- [Condition 1]
- [Condition 2]

## When NOT to use
- [Anti-use case 1]
- [Anti-use case 2]

## Inputs required
- [Required input 1]
- [Required input 2]

## Workflow
1. [Step 1: Specific action]
2. [Step 2: Specific action]
3. [Verify result]

## Rules
- MUST follow constraint 1
- NEVER violate constraint 2
- REQUIRED: specific behavior

## Anti-patterns
- **Anti-Pattern Name**: Why it fails and what to do instead

## Failure conditions
- Condition where agent MUST abort
- Condition requiring human review

## Validation checklist
- [ ] Check 1: Concrete verification
- [ ] Check 2: Concrete verification

## Output format
[Specification of expected output structure, file types, naming conventions]

## Security considerations
[Explicit threat model, mitigations, safety constraints]

## Agent execution notes
- Agent MAY: [allowed operations]
- Agent MUST NEVER: [prohibited operations]
- Agent MUST ASK: [what requires confirmation]
- Agent MUST VALIDATE: [what must be verified before completion]

## Example

**❌ Anti-pattern:**
[Code or workflow example showing what NOT to do]

**✅ Correct pattern:**
[Code or workflow example showing best practice]
```

---

## Metadata Field Reference

### compatible_agents
List of AI systems this skill is designed for:
- `claude-code` → Claude with code execution
- `cursor` → Cursor IDE
- `copilot` → GitHub Copilot
- `codex` → OpenAI Codex
- `gemini` → Google Gemini

### skill_type
Category of operation:
- `workflow` → Multi-step operational procedure
- `architecture` → Structural/design guidance
- `security` → Security hardening
- `debugging` → Troubleshooting/investigation
- `review` → Code/design review checklists
- `generation` → Code/content generation
- `migration` → Refactoring/system upgrade

### dangerous
`true` if skill involves:
- Destructive filesystem operations
- Network requests to external systems
- Shell execution with user input
- Dependency installation
- Database migrations
- Otherwise, `false`

### requires_review
`true` if:
- Output must be human-reviewed before execution
- Touches system-critical code
- Involves destructive operations
- Otherwise, `false`

### security_level
- `safe` → Non-destructive, no security risks
- `review-required` → Requires human verification
- `dangerous` → May affect system integrity, credentials, or user data

### permissions
Machine-readable permission model:
```yaml
permissions:
  filesystem:
    read: [true|false]
    write: [true|false]
  network:
    outbound: [true|false]
  shell:
    execute: [true|false]
```

### input_requirements
List of prerequisites:
- Existing codebase state
- Required files or configurations
- Required libraries/dependencies

### output_contract
List of guarantees about generated output:
- Style constraints (e.g., "no inline styles")
- Security guarantees (e.g., "sanitized HTML only")
- Structural requirements

### failure_conditions
List of critical stop conditions:
- Missing required dependencies
- Incompatible framework versions
- Conflicting architectural constraints

---

## Validation Rules

1. **Name**: Must be kebab-case, lowercase, max 40 characters
2. **Description**: Must be a single sentence, max 100 characters
3. **Version**: Must follow semver (x.y.z)
4. **Category**: Must match one of the predefined categories
5. **Workflow steps**: Must be numbered, imperative, and outcome-focused
6. **Rules**: Must use MUST/NEVER language only
7. **Validation checklist**: All items must be testable and concrete
8. **Security considerations**: REQUIRED if dangerous=true or security_level!=safe
9. **Agent execution notes**: REQUIRED for all skills
10. **Examples**: Must show both anti-pattern and correct pattern
