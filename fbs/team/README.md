# FBS Chief Team

This directory contains the Firefly Business Systems operating programs for the existing OpenClaw team:

- `chief` — human-facing leader and sole coordinator.
- `researcher` — evidence gathering and verification.
- `writer` — business artifact drafting and transformation.
- `reviewer` — independent QA, scope, evidence, and risk review.

## Required runtime wiring

Chief may delegate only to the three specialists:

```json5
{
  agents: {
    entries: {
      chief: {
        subagents: {
          allowAgents: ["researcher", "writer", "reviewer"],
          delegationMode: "prefer"
        }
      },
      researcher: { subagents: { allowAgents: [] } },
      writer: { subagents: { allowAgents: [] } },
      reviewer: { subagents: { allowAgents: [] } }
    }
  }
}
```

The current FBS runtime model policy is intended to remain separate from these workspace instructions: Codex/OpenAI primary and Claude CLI Sonnet fallback. Credentials, `openclaw.json`, SQLite state, and agent runtime databases must remain local and must not be committed.

For GPT-5.5 Chief sessions, disable Code Mode at the agent/model override when the runtime warns that the model does not advertise Code Mode support; do not disable Codex itself.
