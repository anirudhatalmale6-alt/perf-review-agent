# Performance Review Agent

A Claude Code custom agent that scans source code for performance bottlenecks, anti-patterns, and regressions. Provides actionable findings with severity ratings and concrete code fixes.

## What It Does

Analyzes code across 6 performance categories:
- ALGORITHMIC - O(n^2) patterns, unnecessary iterations, missing early exits
- MEMORY - Unbounded caches, object creation in loops, memory leaks
- I/O & DATABASE - N+1 queries, missing indexes, blocking I/O
- CONCURRENCY - Race conditions, lock contention, deadlocks
- RESOURCE MANAGEMENT - Unclosed connections, missing timeouts
- SERIALIZATION/NETWORK - Over-fetching, chatty protocols

## Setup

### For Copilot Team (GitHub Copilot with Claude)

1. Copy the `.github/agents/perf-review-agent.md` file into your project's `.github/agents/` directory
2. Open the project in VS Code with Claude Code extension installed
3. In Claude Code chat, select "Performance Review Agent" from the agent picker at the bottom
4. The agent uses `Claude Sonnet 4.6 (copilot)` model through your Copilot subscription

### For Bedrock Team (Claude through AWS Bedrock)

1. Copy the `.github/agents/perf-review-agent-bedrock.md` file into your project's `.github/agents/` directory
2. Rename it to `perf-review-agent.md` (remove the -bedrock suffix)
3. Configure Claude Code to use Bedrock as provider:
   - Open Claude Code settings
   - Set API provider to AWS Bedrock
   - Configure your AWS region and credentials
4. The agent uses `us.anthropic.claude-sonnet-4-6-20250514-v1:0` model through your Bedrock access

### Alternative: Claude Code CLI

```bash
# Navigate to your project (must have .github/agents/ folder)
cd your-project

# Start Claude Code CLI
claude

# Select the agent from the picker or reference it directly
```

## How to Use

Once the agent is selected in Claude Code:

```
# Scan a specific file
"Review src/controllers/OrderController.java for performance issues"

# Scan a directory
"Scan the src/services/ directory for performance bottlenecks"

# Review recent changes
"Check the latest git diff for performance regressions"

# Analyze specific patterns
"Look for N+1 query patterns in the data access layer"
```

## Integrating Into Your Project

To add this agent to any existing project:

```bash
# From your project root
mkdir -p .github/agents
cp perf-review-agent.md .github/agents/   # or perf-review-agent-bedrock.md
```

The agent automatically reads your project structure, detects the framework, and applies language-specific performance checks.
