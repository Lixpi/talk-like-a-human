# talk-like-a-human

Agent skill: make LLM responses simpler and more readable.

For now this is tailored for engineering. An alternative version targeting a broader audience will be released later.

## Installation

There's no install script yet, so for now you copy the skill folder into your harness by hand. The whole skill is a single file, `skills/talk-like-a-human/SKILL.md`, and the folder name has to stay `talk-like-a-human` because it matches the `name` in the skill's frontmatter.

Clone the repository first:

```sh
git clone https://github.com/Lixpi/talk-like-a-human.git
```

Then copy the folder into the skills directory of the harness you use.

### Claude Code

Copy the folder into your personal skills directory to make it available in every project:

```sh
mkdir -p ~/.claude/skills
cp -r talk-like-a-human/skills/talk-like-a-human ~/.claude/skills/
```

To install it for a single project instead, copy it into that project's `.claude/skills/` directory. Claude Code picks up new skills when a session starts.

### Codex

Codex looks for personal skills in `~/.agents/skills`, so copying the folder there makes it available in every repository:

```sh
mkdir -p ~/.agents/skills
cp -r talk-like-a-human/skills/talk-like-a-human ~/.agents/skills/
```

To install it for a single repository instead, copy it into `.agents/skills/` at the repository root. Codex detects new skills automatically, but if the skill doesn't show up, restart Codex.

### Other harnesses

Other harnesses that support agent skills use the same folder layout but look for skills in their own directory, so check your harness's documentation for the location and copy the folder there.

## Making the skill mandatory (optional)

A harness usually loads a skill only when the agent decides the task calls for it, so the agent may skip it for replies that don't look like writing tasks, such as a quick answer or a progress update. If you want the skill applied to everything the agent writes for people, add the block below to your agent instructions file, such as `AGENTS.md` or `CLAUDE.md`.

```markdown
## Required Human-Facing Communication Skill

At the start of every agent turn, before writing any human-facing text, read and follow the `talk-like-a-human` skill. This is a hard rule for every interaction, including answers, clarification questions, progress updates, review comments, documentation, tickets, reports, and final responses. It applies even when the task is unrelated to documentation.

If the skill cannot be resolved or read, stop immediately. Do not continue the task and do not produce any substantive response. The only permitted response is a brief report that `talk-like-a-human` could not be resolved, followed by waiting for the user's instructions.
```

The last paragraph makes the agent stop instead of quietly carrying on without the skill, so a missing install shows up on the first turn rather than as a gradual drift back to the default writing style.
