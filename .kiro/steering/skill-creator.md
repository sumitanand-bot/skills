# Skill Creator Steering

## Metadata

- **Name**: skill-creator
- **Description**: Comprehensive guide for creating, editing, and packaging skills. Skills are modular, self-contained packages that extend Claude's capabilities by providing specialized knowledge, workflows, and tools. Use when building new skills or iterating on existing ones.

## Triggers

Use this steering when:
- User wants to create a new skill
- User needs to edit or improve an existing skill
- User asks to package a skill for distribution
- User mentions "skill development" or "custom skill"
- User wants to understand skill structure and best practices

## Instructions

### About Skills

Skills are modular, self-contained packages that extend Claude's capabilities by providing specialized knowledge, workflows, and tools. Think of them as "onboarding guides" for specific domains or tasks.

### What Skills Provide

1. Specialized workflows - Multi-step procedures for specific domains
2. Tool integrations - Instructions for working with specific file formats or APIs
3. Domain expertise - Company-specific knowledge, schemas, business logic
4. Bundled resources - Scripts, references, and assets for complex tasks

### Core Principles

#### Concise is Key

The context window is a public good. Only add context Claude doesn't already have. Challenge each piece of information: "Does Claude really need this explanation?"

#### Set Appropriate Degrees of Freedom

- **High freedom**: Use when multiple approaches are valid
- **Medium freedom**: Use when a preferred pattern exists
- **Low freedom**: Use when operations are fragile and error-prone

### Anatomy of a Skill

```
skill-name/
├── SKILL.md (required)
│   ├── YAML frontmatter metadata (required)
│   │   ├── name: (required)
│   │   ├── description: (required)
│   │   └── compatibility: (optional)
│   └── Markdown instructions (required)
└── Bundled Resources (optional)
    ├── scripts/          - Executable code
    ├── references/       - Documentation to be loaded as needed
    └── assets/           - Files used in output
```

### Skill Creation Process

1. **Understand the skill with concrete examples**
2. **Plan reusable skill contents** (scripts, references, assets)
3. **Initialize the skill** (run `init_skill.py`)
4. **Edit the skill** (implement resources and write SKILL.md)
5. **Package the skill** (run `package_skill.py`)
6. **Iterate based on real usage**

### Step 3: Initializing the Skill

```bash
scripts/init_skill.py <skill-name> --path <output-directory>
```

The script creates:
- The skill directory at the specified path
- A SKILL.md template with proper frontmatter
- Example resource directories: `scripts/`, `references/`, and `assets/`

### Step 4: Edit the Skill

**Learn Proven Design Patterns:**
- Multi-step processes: See `skills/skill-creator/references/workflows.md`
- Output patterns: See `skills/skill-creator/references/output-patterns.md`

**Writing Guidelines:** Always use imperative/infinitive form.

**Frontmatter:**
- `name`: The skill name
- `description`: Primary triggering mechanism - include what the skill does AND specific triggers/contexts

### Step 5: Packaging a Skill

```bash
scripts/package_skill.py <path/to/skill-folder>
```

The packaging script will:
1. **Validate** the skill automatically
2. **Package** if validation passes, creating a `.skill` file

### Progressive Disclosure Design

Skills use a three-level loading system:
1. **Metadata (name + description)** - Always in context (~100 words)
2. **SKILL.md body** - When skill triggers (<5k words)
3. **Bundled resources** - As needed (unlimited)

Keep SKILL.md body under 500 lines. Split content into separate files when approaching this limit.

## Resources

- `skills/skill-creator/scripts/init_skill.py` - Initialize new skills
- `skills/skill-creator/scripts/package_skill.py` - Package skills for distribution
- `skills/skill-creator/scripts/quick_validate.py` - Validate skill structure
- `skills/skill-creator/references/workflows.md` - Workflow design patterns
- `skills/skill-creator/references/output-patterns.md` - Output format patterns
