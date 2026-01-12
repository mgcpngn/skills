---
name: mcp-builder
description: Use when building MCP (Model Context Protocol) servers to enable LLM interaction with external services. Use for creating API integrations, tool definitions, and server implementations.
---

# MCP Server Development Guide

## Overview

Create MCP (Model Context Protocol) servers that enable LLMs to interact with external services through well-designed tools.

**Core principle:** The quality of an MCP server is measured by how well it enables LLMs to accomplish real-world tasks.

## When to Use

**Use when:**
- Building integrations between LLM and external APIs
- Creating tool servers for Claude or other LLM clients
- Implementing remote/local MCP servers
- Need to expose APIs as LLM-callable tools

## The Process

### Phase 1: Research and Planning

#### 1.1 Understand Modern MCP Design

**API Coverage vs. Workflow Tools:**
- Balance comprehensive API endpoint coverage with specialized workflow tools
- Prioritize comprehensive API coverage when uncertain
- Workflow tools for specific high-frequency tasks

**Tool Naming and Discoverability:**
- Clear, descriptive names: `github_create_issue`, `github_list_repos`
- Consistent prefixes by service
- Action-oriented naming

**Context Management:**
- Concise tool descriptions
- Support filtering/pagination in results
- Return focused, relevant data

**Error Messages:**
- Actionable guidance toward solutions
- Specific suggestions and next steps

#### 1.2 Study MCP Documentation

Key resources:
- MCP Specification: `https://modelcontextprotocol.io/specification/draft.md`
- Transport mechanisms (HTTP, stdio)
- Tool, resource, and prompt definitions

#### 1.3 Plan Implementation

**Understand the API:**
- Review service's API documentation
- Identify key endpoints, auth requirements, data models

**Tool Selection:**
- Prioritize comprehensive API coverage
- List endpoints to implement, starting with common operations

### Phase 2: Implementation

#### 2.1 Project Structure

**Recommended stack:**
- **Language**: TypeScript (best SDK support, good for LLM code generation)
- **Transport**: Streamable HTTP for remote, stdio for local

```
my-mcp-server/
├── src/
│   ├── index.ts           # Server entry point
│   ├── tools/             # Tool implementations
│   ├── client/            # API client
│   └── utils/             # Shared utilities
├── package.json
└── tsconfig.json
```

#### 2.2 Implement Tools

For each tool:

**Input Schema:**
```typescript
const schema = z.object({
  query: z.string().describe("Search query"),
  limit: z.number().optional().default(10).describe("Max results (1-100)")
});
```

**Tool Description:**
- Concise summary of functionality
- Parameter descriptions with examples
- Return type schema

**Implementation:**
```typescript
server.tool({
  name: "search_items",
  description: "Search for items by query",
  schema: searchSchema,
  handler: async ({ query, limit }) => {
    const results = await client.search(query, limit);
    return {
      content: [{ type: "text", text: JSON.stringify(results) }],
      structuredContent: results
    };
  }
});
```

**Annotations:**
```typescript
annotations: {
  readOnlyHint: true,      // Does not modify data
  destructiveHint: false,  // Does not delete data
  idempotentHint: true,    // Safe to retry
  openWorldHint: false     // Limited scope
}
```

### Phase 3: Testing

1. **Unit tests** for individual tools
2. **Integration tests** against real/mock APIs
3. **LLM testing** - have Claude use the tools
4. **Error scenario testing** - verify actionable error messages

### Phase 4: Documentation

Create clear README with:
- Setup instructions
- Tool reference
- Example usage
- Configuration options

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Vague tool names | Use `service_action_object` pattern |
| Missing error handling | Return actionable error messages |
| No pagination | Add limit/offset for list operations |
| Overly complex schemas | Keep inputs simple, provide defaults |

## Quick Reference

| Component | Pattern |
|-----------|---------|
| Tool naming | `{service}_{action}_{object}` |
| Input schema | Zod (TS) or Pydantic (Python) |
| Error format | `{ error: string, suggestion: string }` |
| Transport | HTTP (remote), stdio (local) |

## Related Skills

- **test-driven-development** - Write tests for tools
- **systematic-debugging** - Debug tool issues
