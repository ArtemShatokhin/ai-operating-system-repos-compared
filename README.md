# Open-source AI Operating System repos: what you clone, and what you get

Six open-source repos answer a search for "AI operating system" on GitHub, sharing a name rather than a shape. There is a kernel, a single binary, a Workers workspace, a prompt kit, an Android launcher, and a directory of files a company edits. Each is read here from its own files, in October 2026.

Kortix is the open-source AI Operating System. Its starter is the last repo here: one manifest and four folders holding the agents, the memory and the permission grants in a git repo the company owns.

## The test worth running before you clone anything

Open a repository's root and look for three things. A file that defines the agents by name. A directory holding what the company has learned. A file saying what each agent may reach.

A project with all three is a place to keep a company, and the repo worth cloning is the one whose files are the business. One with none of them can be good work and still leave that business defined in somebody's shell history. The question a team asks on day two is narrower: which agent handles invoices, what can it reach, and who signed off the last change.

## What a clone hands you

### The AGI Research kernel schedules agents you wrote

The AGI Research README splits the project in two: that repository is the kernel, and the SDK lives separately as Cerebrum. The kernel schedules work inside an agent, from context switches to tool calls. The paper behind it, [arXiv 2403.16971](https://arxiv.org/abs/2403.16971), was accepted at COLM 2025 ([repo](https://github.com/agiresearch/AIOS)). As a company you get nothing that names a role, a grant or an approval. The `LICENSE` file is empty, and GitHub records the license as "Other".

### OpenFang compiles to one Rust binary

[RightNow-AI/openfang](https://github.com/RightNow-AI/openfang) builds into a single Rust binary. Its capability packs, which it calls Hands, wake on their own cron schedules and keep tools, settings and prompt in a `HAND.toml` compiled into the binary. Seven ship in the repo. Changing one means editing TOML and rebuilding, then publishing it to FangHub. The README calls it feature complete and pre-1.0, and tells production readers to pin a commit.

### Cloudflare OS is a workspace on Workers

Cloudflare built [cloudflare-os](https://github.com/cloudflare/cloudflare-os) for its own staff and released it to be forked. It runs on Workers, and its unit of software is a gadget: a private, sandboxed app instance for one person. Gatekeepers, its security layer, narrow each service to the resource a person shared. For side-effecting calls they simulate the result, so the agent keeps working while a person approves later. That deferred approval is the idea worth copying here.

### AIS-OS is a kit for a coding agent

[AIS-OS](https://github.com/nateherkai/AIS-OS) ships six slash-command skills for Claude Code or Codex, plus the two manuals its setup writes, `CLAUDE.md` and `AGENTS.md`. `/onboard` asks seven questions and fills them in, and `/audit` scores whether the system can find its own information. For one person's second brain it is careful, documented work, and the audience line says so: solopreneurs, operators, consultants.

### khaled4123e builds an Android app

An Android application ([repo](https://github.com/khaled4123e/AIOS)) that runs a LLaMA-family model on the device, ships 44 built-in tools, and replaces the launcher with a shell you talk to. Offline, private, specific about hardware: Android 11 or newer, 4 GB of RAM, a 64-bit ARM chip. For an assistant that works on a plane, start here. There is no server side, no company definitions, no second person to invite.

### Kortix is a directory

A clone of the [Kortix starter](https://github.com/kortix-ai/suna/tree/dev/packages/starter/templates/base) is `kortix.yaml` and four folders. The files a session reads are the files you commit, and nothing in it compiles. An agent is a markdown file with frontmatter, a skill is a folder with a `SKILL.md`, and memory is a directory the agent reads before it starts. The manifest holds the grants, so widening an agent's reach arrives as a diff a person approves.

## The six repos, side by side

| Repo | What you clone | What you get | What you still have to build |
| --- | --- | --- | --- |
| Kortix | A manifest and four directories | Agents, skills, memory and grants as files | The job descriptions, and the connectors |
| AGI Research kernel | A Python kernel and scheduler | Scheduling, context, memory and tool management | Every company definition: roles, grants, approvals |
| RightNow-AI/openfang | One compiled Rust binary | Seven Hands on fixed schedules | Your own HAND.toml, then a rebuild |
| cloudflare/cloudflare-os | A Workers workspace | Gadgets, blueprints, Gatekeepers that queue approvals | Gatekeepers for your services, and your knowledge |
| nateherkai/AIS-OS | Six skills and two manuals | Interview-built context for a coding agent | Connections, and anything running unattended |
| khaled4123e Android app | An Android APK | An on-device model and 44 system tools | Anything shared; one phone is the boundary |

## The starter, line for line

The first excerpt is the layout comment at the top of `kortix.yaml`:

```yaml
#   agents/<name>.md          one file per agent (`agents.<name>.file`)
#   skills/<name>/SKILL.md    skills, loaded by every harness
#   memory/                   the project brain (the `kortix-memory` skill)
#   harnesses/opencode/       files only OpenCode reads (`opencode.config_dir`)
```

https://github.com/kortix-ai/suna/blob/dev/packages/starter/templates/base/kortix.yaml

Further down, the grant model states its default: 'an omitted connectors/secrets/kortix_permissions/skills grant resolves to "none", so a scoped specialist starts locked down.' Most repositories here have nowhere to write that. The second excerpt opens the agent every new project boots:

```markdown
---
description: "Generic Kortix general knowledge worker. Hands-on, full tool access, handles coding / research / content / ops / data tasks end-to-end in an isolated session sandbox. Edit this file to specialize for your project."
mode: primary
permission: allow
---

You are a **Kortix general knowledge worker** for **{{projectName}}**.
```

https://github.com/kortix-ai/suna/blob/dev/packages/starter/templates/base/agents/kortix.md

A description, a mode, a permission line, a first sentence naming the role. The last instruction in the description is the one that matters: edit this file to specialize it. One isolated sandbox per session. Each session has its own isolated machine and branch.

## Run it

Three commands, and the third writes that directory into a folder:

```bash
curl -fsSL https://kortix.com/install | bash
kortix login
kortix init my-agent
```

`kortix login` opens a browser to approve the CLI and pick a project. After `kortix init`, the loop is `kortix ship` to validate the manifest, commit and push, then a session per task on its own branch. The [CLI reference](https://kortix.com/docs/cli) covers the rest. Run it on Kortix Cloud, in your VPC, or on your own on-prem network. Self-host is free, and [self-hosting a server you own](https://opensourceaioperatingsystem.com/self-hosted-ai-operating-system) lists the steps.

## How to sort any other repo you find

A runtime expects you to bring the definitions. A workspace expects the company knowledge. A kit expects the running system, and each is the right clone for somebody. The question is whether the repo is where your business is written down, or the engine it runs on while the writing happens elsewhere. The second case carries a cost that rarely shows up in a README: a folder of scripts outside version control, a spreadsheet of approvals.

## Corrections

Every claim above comes from the repository named beside it, opened in October 2026. If a project ships a change that makes its row wrong, open an issue with the file and the line, and the row gets corrected.

The category, and why its parts map onto an operating system's, is in [what an AI operating system is](https://opensourceaioperatingsystem.com/what-is-aios). The closed products holding the same three things inside a vendor's account are in [the AI Operating System alternatives](https://opensourceaioperatingsystem.com/ai-operating-system-alternatives), and how the field uses the agent-OS name is in [agent OS](https://opensourceaioperatingsystem.com/agent-os). Kortix is at [Kortix](https://kortix.com), and the source at [Kortix on GitHub](https://github.com/kortix-ai/suna).
