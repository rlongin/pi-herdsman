# EF HNIC Setup

**EF HNIC** stands for **Hierarchical Network Intelligence Coordinator**.

EF HNIC is the EF Ventures branded distribution of Pi Herdsman. The underlying
extension remains `pi-herdsman` so that Pi/herdr compatibility and upstream
updates remain intact.

## Architecture

```text
Nexus / EF Ventures
        |
        v
     EF HNIC
        |
        +-- Lead
        |    +-- Scout
        |    +-- Researcher
        |    +-- Reviewer
        |    +-- Custom EF agents
        |
        +-- Chief supervision
             +-- Lead A
             +-- Lead B
```

Pi owns each conversation and turn state. Pi Herdsman/EF HNIC coordinates
assignments, delegation, questions, results, and control. herdr owns physical
agent lifecycle and placement.

## Requirements

- Node >= 22.19.0
- herdr >= 0.9.1
- Pi >= 0.87.0 and < 0.88.0

## Install the supported runtime

The upstream npm package remains the compatibility source:

```sh
pi install npm:pi-herdsman
herdr integration install pi
herdr integration status
```

Start herdr in the target project:

```sh
herdr
```

Then start Pi inside the herdr pane:

```sh
pi
```

## Core operator commands

```text
/agents
/chief
/chief leave
```

Use `/agents` for the current lead's managed agents. Use `/chief` to supervise
independent leads in the current herdr runtime.

## EF HNIC operating model

Recommended default roles:

- **Scout** — fast repository mapping and discovery.
- **Researcher** — external/API verification and unfamiliar-system research.
- **Reviewer** — correctness, regression, and unnecessary-complexity review.
- **Builder** — bounded implementation work after scope is established.
- **Lead** — architecture, scope, acceptance, and final decisions.
- **Chief** — supervision across independent leads; does not take ownership of
  their agent trees.

Keep one executor per unresolved unit of work. Avoid overlapping writers in the
same worktree or file-ownership boundary.

## Nexus integration

Do not run this orchestration engine in the browser. EF HNIC belongs on the
machine/runtime layer with Pi and herdr.

Nexus should act as a control and status surface. A future Nexus page can show:

- runtime online/offline state;
- leads and agent counts;
- active / blocked / idle state;
- current assignment labels;
- recent result notifications;
- links to operator documentation.

The browser should not receive shell credentials, Pi session secrets, or direct
filesystem authority.

## Updating from upstream

Keep EF modifications surface-level whenever possible. Pull or merge upstream
Pi Herdsman changes into the EF fork, resolve only genuine conflicts, then rerun
the upstream validation flow.

Do not rename the npm package, command names, coordination tool names, or
protocol namespaces solely for branding.

## Attribution

See [NOTICE](../NOTICE) and [LICENSE](../LICENSE).
