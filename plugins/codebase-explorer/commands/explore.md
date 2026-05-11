---
description: Launch the Socratic codebase exploration agent for interactive learning
argument-hint: [question or area to explore]
---

Launch the codebase-explorer agent to help the user understand this codebase through Socratic exploration.

The user wants to explore and understand a codebase interactively. They may have provided a specific question or area of focus: $ARGUMENTS

Spawn the codebase-explorer agent with the user's request. The agent will:
1. Scan dependencies and project structure
2. Provide a concise overview
3. Offer exploration paths
4. Guide learning through Socratic questioning

If the user provided arguments, pass them as the initial exploration context. If no arguments were provided, the agent will begin with Environment Sensing & Overview and ask the user what they'd like to explore.
