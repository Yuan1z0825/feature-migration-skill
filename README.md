# Feature Migration Skill

[中文文档](./README_zh.md)

A Claude Code skill for precisely migrating open-source project features to your local project through a structured four-stage workflow.

## Features

- **Deep Context Analysis**: Automatically analyzes your local project's framework, dependencies, and code conventions
- **Open-Source Research**: Uses DeepWiki and GitHub API to understand open-source project architecture
- **Feasibility Assessment**: Identifies compatibility risks and determines minimum viable code set
- **Precise Implementation**: Generates code that conforms to your project's conventions

## Prerequisites

### 1. Install DeepWiki MCP Server

DeepWiki provides deep analysis of open-source projects. Install it with:

```bash
claude mcp add -s user -t http deepwiki https://mcp.deepwiki.com/mcp
```

This command registers DeepWiki MCP server globally for all your Claude Code sessions.

### 2. Install GitHub CLI (gh)

The skill uses `gh` command to access GitHub repositories:

**macOS:**
```bash
brew install gh
```

**Linux (Debian/Ubuntu):**
```bash
sudo apt install gh
```

**Linux (Fedora/RHEL):**
```bash
sudo dnf install gh
```

**Verify installation:**
```bash
gh --version
```

**Authenticate GitHub CLI:**
```bash
gh auth login
```

## Installation

### Method 1: Manual Installation

1. Clone or download this repository:
```bash
git clone https://github.com/your-username/feature-migration-skill.git
```

2. Copy the skill to your Claude Code skills directory:
```bash
# For English version
cp -r feature-migration-skill/skill_en ~/.claude/skills/feature-migration

# For Chinese version
cp -r feature-migration-skill/skill_zh ~/.claude/skills/feature-migration
```

### Method 2: Direct Download

Download the `SKILL.md` file and place it in `~/.claude/skills/feature-migration/SKILL.md`.

## Usage

### Trigger Keywords

The skill activates when you provide a GitHub link and express migration intent:

- "Migrate XXX feature from https://github.com/..."
- "Integrate https://github.com/... into my project"
- "Reference https://github.com/... to implement XXX"
- "Port the XXX functionality from https://github.com/..."

### Example Usage

```
User: I want to migrate the attention visualization feature from
https://github.com/mahmoodlab/CLAM to my project's vis_scripts directory
```

The skill will guide you through four stages:

#### Stage 1: Local Context Alignment
Analyzes your project structure, dependencies, and code conventions.

#### Stage 2: Open-Source Overview Research
Researches CLAM's architecture and identifies relevant modules.

#### Stage 3: Feasibility Analysis
Evaluates compatibility and designs migration approach.

#### Stage 4: Implementation
Generates code and modifies your local files.

## Workflow Details

### Stage 1: Local Context Alignment

**What it does:**
- Scans your project directory structure
- Parses dependency files (requirements.txt, package.json, etc.)
- Identifies frameworks and their versions
- Recognizes code style conventions

**Output Example:**
```markdown
## Integration Environment Profile

### Project Type
ML Research Project

### Core Framework
- Framework: PyTorch 2.0
- Python: 3.10

### Key Modules
- feature_extractor: WSI feature extraction
- modules: MIL model implementations
- vis_scripts: Visualization utilities

### Code Style
- Naming Convention: snake_case
- Type Annotations: Partial
- Documentation Style: Google
```

### Stage 2: Open-Source Overview Research

**What it does:**
- Queries DeepWiki for project documentation
- Analyzes GitHub repository structure
- Identifies core modules and their responsibilities
- Maps data flow and API interfaces

**Output Example:**
```markdown
## Technical Overview Map

### Core Modules
| Module | Responsibility | Relevance |
|--------|---------------|-----------|
| model_utils | Attention weights extraction | High |
| visualization | Heatmap generation | High |
| data_processing | Slide preprocessing | Low |

### Integration Points
- Attention extraction: Can be adapted to existing feature pipeline
- Visualization: Needs style adaptation for local conventions
```

### Stage 3: Feasibility Analysis

**What it does:**
- Determines minimum viable code set
- Identifies version conflicts
- Assesses dependency risks
- Designs integration architecture

**Output Example:**
```markdown
## MVP Code Set
| File | Purpose | Required |
|------|---------|----------|
| attention_utils.py | Attention extraction | Yes |
| heatmap.py | Visualization | Yes |
| config.yaml | Configuration | Needs adaptation |

## Compatibility Risks
| Risk | Impact | Mitigation |
|------|--------|------------|
| NumPy version conflict | Medium | Use virtual environment |
| Matplotlib style | Low | Adapt to local style |
```

### Stage 4: Implementation

**What it does:**
- Deep-dives into source code
- Generates conforming code
- Creates new files
- Modifies existing files
- Updates configurations

**Output Example:**
```markdown
## Implementation Complete

### New Files
- vis_scripts/attention_heatmap.py: Attention visualization module
- vis_scripts/heatmap_utils.py: Utility functions

### Modified Files
- vis_scripts/__init__.py: Added imports

### Usage
from vis_scripts.attention_heatmap import generate_heatmap
heatmap = generate_heatmap(attention_weights, slide_coords)
```

## Troubleshooting

### DeepWiki Not Available

If DeepWiki doesn't have the project indexed:
- The skill will skip DeepWiki and use GitHub API only
- You may provide additional documentation manually

### GitHub Access Issues

If `gh` commands fail:
- Check authentication: `gh auth status`
- Re-authenticate: `gh auth login`
- Verify repository access permissions

### Large Projects

For large open-source projects:
- Stage 2 may take longer to analyze
- Consider specifying a particular module or feature scope

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

## License

MIT License - see LICENSE file for details.

## Acknowledgments

- [DeepWiki](https://deepwiki.com) for open-source project analysis
- [Claude Code](https://claude.ai) for the skill framework
- All open-source projects that make this workflow possible
