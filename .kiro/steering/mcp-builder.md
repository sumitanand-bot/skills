# MCP Builder Steering

## Metadata

- **Name**: mcp-builder
- **Description**: Guide for creating high-quality MCP (Model Context Protocol) servers that enable LLMs to interact with external services through well-designed tools. Use when building MCP servers to integrate external APIs or services, whether in Python (FastMCP) or Node/TypeScript (MCP SDK).

## Triggers

Use this steering when:
- User wants to build an MCP server
- User needs to integrate external APIs or services with LLMs
- User mentions "Model Context Protocol" or "MCP"
- User asks about creating tools for Claude or other LLMs
- User wants to build Python or TypeScript MCP servers

## Instructions

### Overview

Create MCP (Model Context Protocol) servers that enable LLMs to interact with external services through well-designed tools. The quality of an MCP server is measured by how well it enables LLMs to accomplish real-world tasks.

### High-Level Workflow

#### Phase 1: Deep Research and Planning

**1.1 Understand Modern MCP Design:**
- Balance comprehensive API endpoint coverage with specialized workflow tools
- Use clear, descriptive tool names with consistent prefixes
- Design tools that return focused, relevant data
- Provide actionable error messages

**1.2 Study MCP Protocol Documentation:**
- Start with sitemap: `https://modelcontextprotocol.io/sitemap.xml`
- Fetch pages with `.md` suffix for markdown format
- Review: Specification overview, transport mechanisms, tool definitions

**1.3 Study Framework Documentation:**

Recommended stack:
- **Language**: TypeScript (high-quality SDK support)
- **Transport**: Streamable HTTP for remote, stdio for local

**Reference Files:**
- `skills/mcp-builder/reference/mcp_best_practices.md` - Core guidelines
- `skills/mcp-builder/reference/node_mcp_server.md` - TypeScript patterns
- `skills/mcp-builder/reference/python_mcp_server.md` - Python patterns

**1.4 Plan Your Implementation:**
- Review the service's API documentation
- List endpoints to implement, starting with common operations

#### Phase 2: Implementation

**2.1 Set Up Project Structure**

See language-specific guides for project setup.

**2.2 Implement Core Infrastructure**

Create shared utilities:
- API client with authentication
- Error handling helpers
- Response formatting
- Pagination support

**2.3 Implement Tools**

For each tool:

**Input Schema:**
- Use Zod (TypeScript) or Pydantic (Python)
- Include constraints and clear descriptions

**Output Schema:**
- Define `outputSchema` where possible
- Use `structuredContent` in tool responses

**Implementation:**
- Async/await for I/O operations
- Proper error handling with actionable messages
- Support pagination where applicable

**Annotations:**
- `readOnlyHint`, `destructiveHint`, `idempotentHint`, `openWorldHint`

#### Phase 3: Review and Test

**Code Quality:**
- No duplicated code (DRY principle)
- Consistent error handling
- Full type coverage
- Clear tool descriptions

**Build and Test:**
- TypeScript: `npm run build` + MCP Inspector
- Python: `python -m py_compile` + MCP Inspector

#### Phase 4: Create Evaluations

Create 10 evaluation questions that are:
- Independent, Read-only, Complex
- Realistic, Verifiable, Stable

**Output Format:**
```xml
<evaluation>
  <qa_pair>
    <question>...</question>
    <answer>...</answer>
  </qa_pair>
</evaluation>
```

## Resources

- `skills/mcp-builder/reference/mcp_best_practices.md` - Universal MCP guidelines
- `skills/mcp-builder/reference/python_mcp_server.md` - Python implementation guide
- `skills/mcp-builder/reference/node_mcp_server.md` - TypeScript implementation guide
- `skills/mcp-builder/reference/evaluation.md` - Evaluation creation guide
- `skills/mcp-builder/scripts/evaluation.py` - Evaluation runner
- `skills/mcp-builder/scripts/connections.py` - Connection utilities
