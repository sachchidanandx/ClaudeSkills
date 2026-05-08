---
name: confluence-reader
description: Use this skill whenever the user asks about Confluence content, wiki pages, documentation hosted in Confluence, or references a Confluence page/space. This includes questions like "what does the wiki say about...", "find the confluence page for...", "look up our docs on...", "what's in space X", or any request that involves reading information from Atlassian Confluence. Always use this skill when the user mentions Confluence, wiki, or asks about internal documentation that might be stored in Confluence.
---

# Confluence Reader

Read Confluence pages, spaces, and blog posts using the `acli` CLI tool. Answer user questions based exclusively on content fetched from Confluence.

## Core Principle

Only answer from content retrieved via `acli` commands. Never supplement with outside knowledge. If the information is not found in Confluence, say so explicitly.

## Available Commands

### List Spaces

```bash
acli confluence space list --json
acli confluence space list --type global --json
acli confluence space list --type personal --json
```

### View Space Details

```bash
acli confluence space view --id <SPACE_ID> --json
```

### View a Page

```bash
acli confluence page view --id <PAGE_ID> --body-format storage --json
acli confluence page view --id <PAGE_ID> --body-format view --json
```

Use `--body-format view` for human-readable HTML. Use `--body-format storage` for raw Confluence storage format. Add flags like `--include-labels`, `--include-direct-children` for additional metadata.

### List Blog Posts

```bash
acli confluence blog list --space-id <SPACE_ID> --json
acli confluence blog list --space-id <SPACE_ID> --title "search term" --json
```

### View a Blog Post

```bash
acli confluence blog view --id <BLOG_ID> --body-format view --json
```

## Workflow

1. **Identify what to fetch**: Determine the page ID, space ID, or search terms from the user's question.
2. **Start with spaces if needed**: If the user mentions a space name but you don't have the ID, list spaces first to find the correct one.
3. **Fetch the content**: Use the appropriate command to retrieve the page or blog post content.
4. **Parse the response**: Extract the meaningful content from the JSON response. The page body is typically in HTML format within the `body` field.
5. **Answer the question**: Respond based solely on the fetched content.

## Response Guidelines

- Cite the source page title and ID when answering.
- If a page has child pages that might contain the answer, mention them and offer to fetch those too.
- If the content is not found, say: "I couldn't find this information in Confluence. The page may not exist, or I may need a different page ID or space to search in."
- Strip HTML tags when presenting content to the user for readability.
- For large pages, summarize the relevant sections rather than dumping everything.

## Tips

- Page IDs are numeric (e.g., `12345678`). If the user provides a URL like `https://site.atlassian.net/wiki/spaces/SPACE/pages/12345678/Page+Title`, extract the numeric page ID.
- Space IDs are also numeric. Use `acli confluence space list` to find them by name.
- If authentication fails, ask the user to run `acli confluence auth status` to check their login state.
