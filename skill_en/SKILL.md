---
name: feature-migration
description: Feature Migration Workflow. Deep understanding of local project context, research open-source project overview, and precise migration of open-source features to local projects. Triggers when user provides a GitHub link and expresses migration/integration/reference intent. Trigger words: migrate feature, integrate open-source, reference implementation, port feature, based on open-source.
---

# Feature Migration Workflow

A four-stage workflow for precisely migrating open-source project features to your local project.

## Input Requirements

- **GitHub Link** (required): GitHub URL of the target open-source project
- **Target Feature** (required): Description of the specific feature to migrate

## Workflow Overview

```
Stage 1: Local Context Alignment → Output Integration Environment Profile → Wait for Confirmation
Stage 2: Open-Source Overview Research → Output Technical Overview Map → Wait for Confirmation
Stage 3: Feasibility Analysis → Output Analysis Report → Wait for Confirmation
Stage 4: Source Code Verification & Implementation → Generate Plan + Modify Local Files
```

---

## Stage 1: Local Context Alignment

### Objective
Deeply understand the local project's technical environment and identify integration constraints.

### Execution Steps

1. **Directory Structure Analysis**
   - Use `Glob` to scan project directory structure
   - Identify key folders and files in the project root

2. **Configuration File Parsing**
   - Read dependency configuration files:
     - Python: `requirements.txt`, `pyproject.toml`, `setup.py`, `setup.cfg`
     - Node.js: `package.json`, `yarn.lock`, `pnpm-lock.yaml`
     - Rust: `Cargo.toml`, `Cargo.lock`
     - Go: `go.mod`, `go.sum`
   - Extract dependency version information

3. **Core Entry File Analysis**
   - Read main entry files: `main.py`, `app.py`, `__main__.py`, `index.js`, `src/main.rs`, etc.
   - Identify framework initialization patterns

4. **Framework Usage Pattern Search**
   - Use `Grep` to search for key framework import patterns
   - Identify API style, state management approach, configuration management patterns

5. **Code Style Recognition**
   - Sample 2-3 representative source files
   - Identify naming conventions, comment style, error handling patterns

### Output Format

```markdown
## Integration Environment Profile

### Project Type
[Web Application/CLI Tool/Library/Data Analysis Project/...]

### Core Framework
- Framework: [Flask/Django/FastAPI/React/Vue/...]
- Version: [x.x.x]

### Directory Structure
[Brief description of directory organization]

### Key Modules
- [Module 1]: [Responsibility]
- [Module 2]: [Responsibility]
- ...

### Technical Stack Constraints
| Constraint Type | Details | Risk Level |
|----------------|---------|------------|
| Python Version | 3.8+ | Low |
| Dependency Conflict | xxx conflicts with yyy | High |
| ... | ... | ... |

### Code Style
- Naming Convention: [snake_case/camelCase/...]
- Type Annotations: [Yes/No]
- Documentation Style: [Google/NumPy/Sphinx/...]
```

### Interaction

After output, ask the user:
> **Stage 1 complete. Please confirm if the local environment analysis is accurate. Any additions or corrections needed? Confirm to proceed to Stage 2.**

---

## Stage 2: Open-Source Overview Research (Macro Exploration)

### Objective
Survey the open-source project's core architecture and identify reusable components.

### Execution Steps

1. **DeepWiki Research**
   - Extract owner/repo from GitHub URL
   - Call `mcp__deepwiki__get-deepwiki-index` to get project index
   - Call `mcp__deepwiki__get-deepwiki-page` to read core pages:
     - Architecture documentation
     - API documentation
     - Core module documentation

2. **GitHub Repository Analysis**
   - Use `gh repo view` to get repository basic information
   - Use `gh api` to get directory structure
   - Read README.md to understand project positioning

3. **Core Module Identification**
   - Identify core modules related to target feature
   - Analyze module dependencies
   - Mark key interfaces and data structures

### Output Format

```markdown
## Technical Overview Map

### Project Positioning
[One-sentence description of core value]

### Overall Architecture
[Architecture diagram or description]

### Core Modules
| Module Name | Responsibility | Relevance to Target |
|-------------|----------------|---------------------|
| [Module 1] | [...] | High/Medium/Low |
| ... | ... | ... |

### API Interface Design
[Key API signatures and usage]

### Data Flow
[How core data flows through the system]

### Reusable Components
[Directly reusable / Needs adaptation / Not reusable components]

### Integration Points with Local Project
- Interface 1: [Description]
- Interface 2: [Description]
- ...
```

### Interaction

After output, ask the user:
> **Stage 2 complete. Open-source project overview analyzed. Confirm to proceed with feasibility analysis?**

---

## Stage 3: Integration Feasibility Analysis

### Objective
Evaluate technical feasibility of integration, identify risks, and design integration approach.

### Execution Steps

1. **MVP Code Set Identification**
   - Determine minimum required code based on target feature
   - List files and dependencies that must be migrated

2. **Compatibility Risk Assessment**
   - Compare local tech stack with open-source project tech stack
   - Identify version conflicts, API incompatibilities, paradigm differences
   - Assess dependency introduction risks

3. **Integration Logic Design**
   - Design inter-module calling relationships
   - Define adapter layers (if needed)
   - Plan configuration management approach

### Output Format

```markdown
## Feasibility Analysis Report

### Implementation Path
[Overall migration strategy description]

### MVP Code Set
| File/Module | Purpose | Required |
|-------------|---------|----------|
| [...] | [...] | Yes/No |
| ... | ... | ... |

### Compatibility Risks
| Risk Item | Description | Impact | Mitigation |
|-----------|-------------|--------|------------|
| [Risk 1] | [...] | High/Medium/Low | [...] |
| ... | ... | ... | ... |

### Dependency Analysis
- New Dependencies: [List]
- Version Conflicts: [List and solutions]

### Integration Design
#### Module Structure
[Module structure design after migration]

#### Interface Adaptation
[Interfaces needing adaptation and approach]

#### Configuration Management
[Configuration item design and management]

### Work Estimation
- New Files: [N]
- Modified Files: [N]
- Estimated Effort: [Small/Medium/Large]
```

### Interaction

After output, ask the user:
> **Stage 3 complete. Feasibility analysis output. Please confirm if the approach is viable. Confirm to proceed with source code verification and implementation.**

---

## Stage 4: Source Code Verification & Implementation (Micro Verification)

### Objective
Deeply verify source code details and generate implementation code conforming to local conventions.

### Execution Steps

1. **Deep Source Code Analysis**
   - Use `gh api` to get key file contents
   - Cross-verify DeepWiki descriptions with actual code
   - Confirm:
     - Variable definitions and types
     - Exception handling logic
     - Context dependencies (Context/Hooks/Utils)
     - Edge cases and boundary handling

2. **Implementation Plan Generation**
   - Write code based on local code conventions
   - Adapt to local project's naming, style, patterns
   - Add necessary comments and documentation

3. **Code Implementation**
   - Use `Write` to create new files
   - Use `Edit` to modify existing files
   - Update configuration files (dependencies, configuration items, etc.)

4. **Verification Checks**
   - Check syntax correctness
   - Confirm import paths are correct
   - Verify interface signature consistency

### Output Format

```markdown
## Implementation Plan

### Core Source Code Verification
[Key source code snippets and analysis]

### Code Implementation

#### New Files
- `[File Path]`: [Purpose]

#### Modified Files
- `[File Path]`: [Modification description]

### Key Code Snippets
[Core implementation code]

### Usage Instructions
[How to use the new feature in local project]

### Follow-up Tasks
- [ ] Unit tests
- [ ] Integration tests
- [ ] Documentation updates
- [ ] ...
```

---

## Important Notes

1. **Progressive Confirmation**: Must wait for user confirmation after each stage output, cannot skip
2. **Code Convention Alignment**: Generated code must conform to local project's code style
3. **Minimal Changes**: Prioritize reusing existing local patterns, avoid introducing unnecessary complexity
4. **Dependency Prudence**: New dependencies must demonstrate necessity, avoid dependency bloat
5. **Documentation Sync**: Update related comments and documentation when modifying code

## Error Handling

- If DeepWiki has no index for the project, skip DeepWiki in Stage 2 and use GitHub analysis only
- If GitHub access is restricted, prompt user to provide source code or documentation
- If target feature doesn't match open-source project, clearly indicate in Stage 2 or 3 and suggest adjustments