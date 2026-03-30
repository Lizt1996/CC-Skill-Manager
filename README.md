# CC-Skill-Manager

Two Claude Code skills for managing and syncing your global skill environment across machines.

## Skills

### `skill-registry`
Records all globally installed skills on the current machine — name, description, and install source. Update `registry.md` whenever a skill is added or removed.

### `skill-manager`
Restores the full skill environment on a new machine by comparing the local install against `registry.md` and installing what's missing.

## Quick Start

### Install on a new machine

```bash
# 1. Copy these two skills
git clone https://github.com/Lizt1996/CC-Skill-Manager.git /tmp/cc-skill-manager
cp -r /tmp/cc-skill-manager/skill-manager ~/.claude/skills/
cp -r /tmp/cc-skill-manager/skill-registry ~/.claude/skills/

# 2. Install official skills
git clone https://github.com/anthropics/skills.git /tmp/anthropic-skills
cp -r /tmp/anthropic-skills/skills/* ~/.claude/skills/

# 3. Install superpowers framework
git clone https://github.com/obra/superpowers.git /tmp/superpowers
cp -r /tmp/superpowers/skills/* ~/.claude/skills/
```

> If GitHub is unreachable, add `-c http.proxy=http://127.0.0.1:<port> -c http.sslVerify=false` to each `git` command.

Reopen Claude Code after installation.

## File Structure

```
skill-manager/
└── SKILL.md          # Sync workflow instructions
skill-registry/
├── SKILL.md          # Registry update instructions
└── registry.md       # Skill catalog (source of truth)
```

## Workflow

- When you **install a new skill** → trigger `skill-registry` to update `registry.md`, then push here
- When you **set up a new machine** → clone this repo, copy skills, run `skill-manager` to install the rest
