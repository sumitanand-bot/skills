# Kiro Steering Files

This directory contains steering files converted from the SKILL.md format used in the Anthropic skills repository. These steering files are designed to work with Kiro and provide guidance for AI assistants on specialized tasks.

## What are Steering Files?

Steering files are markdown documents that guide AI assistants in completing specific tasks. They contain:

- **Metadata**: Name and description of the steering
- **Triggers**: Conditions that indicate when to use this steering
- **Instructions**: Detailed guidance for completing the task
- **Resources**: References to related files and documentation

## Available Steerings

| Steering File | Description | Original Skill |
|--------------|-------------|----------------|
| [theme-factory.md](steering/theme-factory.md) | Apply professional themes to artifacts | `skills/theme-factory/` |
| [pptx.md](steering/pptx.md) | Create, edit, and analyze PowerPoint files | `skills/pptx/` |
| [docx.md](steering/docx.md) | Create, edit, and analyze Word documents | `skills/docx/` |
| [xlsx.md](steering/xlsx.md) | Create, edit, and analyze Excel spreadsheets | `skills/xlsx/` |
| [doc-coauthoring.md](steering/doc-coauthoring.md) | Collaborative document writing workflow | `skills/doc-coauthoring/` |
| [algorithmic-art.md](steering/algorithmic-art.md) | Create generative art with p5.js | `skills/algorithmic-art/` |
| [web-artifacts-builder.md](steering/web-artifacts-builder.md) | Build React/Tailwind artifacts | `skills/web-artifacts-builder/` |
| [internal-comms.md](steering/internal-comms.md) | Write internal communications | `skills/internal-comms/` |
| [slack-gif-creator.md](steering/slack-gif-creator.md) | Create Slack-optimized GIFs | `skills/slack-gif-creator/` |
| [skill-creator.md](steering/skill-creator.md) | Create and package skills | `skills/skill-creator/` |
| [frontend-design.md](steering/frontend-design.md) | Design distinctive web interfaces | `skills/frontend-design/` |
| [brand-guidelines.md](steering/brand-guidelines.md) | Apply Anthropic brand styling | `skills/brand-guidelines/` |
| [mcp-builder.md](steering/mcp-builder.md) | Build MCP servers for LLM integrations | `skills/mcp-builder/` |
| [pdf.md](steering/pdf.md) | Process, create, and manipulate PDFs | `skills/pdf/` |
| [canvas-design.md](steering/canvas-design.md) | Create visual art and designs | `skills/canvas-design/` |
| [webapp-testing.md](steering/webapp-testing.md) | Test web applications with Playwright | `skills/webapp-testing/` |

## How to Use in Kiro

### Automatic Triggering

Kiro steering files are designed to be triggered automatically based on the user's request. Each steering file contains a "Triggers" section that defines when it should be activated.

For example, the `pptx.md` steering will trigger when a user:
- Mentions "deck", "slides", "presentation", or ".pptx"
- Wants to create, read, edit, or modify a PowerPoint file
- Needs to extract text or content from a presentation

### Manual Reference

You can also explicitly reference a steering by mentioning its name or domain:
- "Use the pptx steering to create a presentation"
- "Follow the frontend-design guidelines"
- "Apply the brand-guidelines steering"

### Resource References

Each steering file references resources from the original skill directories. These paths are relative to the repository root:

```
skills/
├── theme-factory/
│   ├── SKILL.md          # Original skill definition
│   ├── themes/           # Theme definition files
│   └── theme-showcase.pdf
├── pptx/
│   ├── SKILL.md
│   ├── editing.md        # Referenced guide
│   ├── pptxgenjs.md      # Referenced guide
│   └── scripts/          # Helper scripts
...
```

## Steering File Structure

Each steering file follows this structure:

```markdown
# [Name] Steering

## Metadata
- **Name**: steering-name
- **Description**: What this steering does and when to use it

## Triggers
Use this steering when:
- [Condition 1]
- [Condition 2]
- ...

## Instructions
[Detailed guidance for completing tasks]

## Resources
- [Links to related files and documentation]
```

## Conversion from SKILL.md Format

These steering files were converted from the original SKILL.md format, which uses YAML frontmatter:

**Original SKILL.md Format:**
```markdown
---
name: skill-name
description: Description of the skill
---

# Skill Instructions
...
```

**Converted Steering Format:**
```markdown
# Skill Name Steering

## Metadata
- **Name**: skill-name
- **Description**: Description of the skill

## Triggers
Use this steering when:
- [Extracted from description]
- [Additional trigger conditions]

## Instructions
# Skill Instructions
...

## Resources
- [Links to skill resources]
```

## Contributing

To add new steering files:

1. Create a new `.md` file in the `steering/` directory
2. Follow the standard structure (Metadata, Triggers, Instructions, Resources)
3. Extract trigger conditions from the skill's description
4. Reference any related resources from the original skill directory
5. Update this README with the new steering entry

## License

The steering files inherit the licenses from their original skill sources. Most skills in this repository are Apache 2.0 licensed, with some proprietary skills (docx, xlsx, pdf, pptx) being source-available. See the LICENSE.txt file in each skill directory for specific terms.
