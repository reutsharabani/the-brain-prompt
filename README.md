# the-brain-prompt

A bootstrap prompt for creating and maintaining a **brain repository** — persistent, portable context that any AI coding agent can read, navigate, and update across all of your projects.

**Prompt:** https://raw.githubusercontent.com/reutsharabani/the-brain-prompt/main/brain.prompt

## Quick start

1. Create your brain directory and open an agent session there:

   ```bash
   mkdir -p ~/brain && cd ~/brain
   ```

2. Paste this into the agent:

   > Read https://raw.githubusercontent.com/reutsharabani/the-brain-prompt/main/brain.prompt and follow it to bootstrap this directory as my brain repository. Do not ask me questions — discover everything autonomously as the prompt specifies.

3. For ongoing work, keep starting agent sessions in `~/brain`.

## Work from the brain, not the project

From the brain, the agent sees every project, host, and service at once, so it can consolidate, dedupe, and remove across them. Projects and services become implementation details the brain reasons over; a session inside one project sees only that slice.

```text
~/brain $ agent
> something here is slow and expensive, optimize it

agent: I have a full view of your projects and hosts.
       chat-api and live-rooms each run their own TURN relay
       (turn-a on edge-1, turn-b on edge-2). Same role, split
       traffic, both mostly idle, both on the bill.

       Nuke turn-b. Point both projects at turn-a.

       plan
         live-rooms   drop the local relay; use turn-a
         edge-2       remove turn-b
         edge-1       keep turn-a as the shared relay
       diff
         - 1 TURN relay
         ~ same coverage, one less service to run
```

*This is the leverage of treating services as implementation details.*

## The problem

Every new agent session starts cold. You re-explain your stack, tooling, conventions, and deployment targets. Project repos hold implementation detail, but not the cross-cutting context an agent needs to work *with* you instead of guessing.

A brain repo is the missing layer: one place for shared intent that sits above individual projects.

## What is a brain repo?

A brain repo is **not** an application, a service, or a monorepo. It is a structured knowledge base — mostly Markdown — that captures:

- Who you are and how you work (`identity/`)
- CLI, editors, shell, and MCP servers (`tooling/`)
- Languages, frameworks, and stacks in active use (`stacks/`)
- Infrastructure vision: cloud, deployment, monitoring (`infrastructure/`)
- A map of your projects, with pointers to their repos (`projects/`)
- Cross-project patterns and preferences (`patterns/`, `preferences/`)
- Current focus and past decisions (`context/`)

Agents discover what they need through a machine-readable `index.yaml` and a vendor-neutral `AGENTS.md` entrypoint — not by reading everything.

### Vision, not truth

The brain holds **intent and defaults**, not live state. Code and deployed systems are authoritative. When the brain and reality disagree, reality wins; the agent surfaces the drift instead of trusting stale Markdown.

### Context separation

Brain-level facts apply across two or more projects, or are independent of any single project. Project-specific detail stays in the project repo. The brain provides defaults; a project may override them locally.

### Autonomous bootstrapping

The agent builds the brain by observing your machine — dotfiles, installed tools, MCP config, cloud CLI profiles, and existing git repos. It infers what it cannot observe directly and marks uncertain entries. No questionnaire.

## Privacy

The generated brain contains inferred personal context — project paths, tooling choices, infrastructure hints. **Keep your brain repo private.** The prompt defaults to a private git remote and excludes secrets via `.gitignore`.

## What gets generated

```
~/brain/
├── AGENTS.md          # Agent entrypoint
├── README.md          # Human-facing index
├── index.yaml         # Machine-readable file manifest
├── identity/          # Profile and environment (auto-detected)
├── preferences/       # Code, docs, and communication style
├── tooling/           # CLI, editors, shell, MCP servers
├── stacks/            # One file per active stack
├── infrastructure/    # Cloud, deployment, monitoring
├── projects/          # Project inventory with repo pointers
├── patterns/          # Reusable architectural patterns
├── context/           # Current focus and past decisions
└── meta/              # Conventions, commit style, agent usage
```

See [`brain.prompt`](brain.prompt) for the full specification.
