# User Guide: Get Shit Done (GSD)

A practical guide to using GSD for building software with Claude Code.

## Table of Contents

- [Installation](#installation)
- [Basic Workflow](#basic-workflow)
- [Complete Example: Building a Blog](#complete-example-building-a-blog)
- [Command Reference](#command-reference)
- [Configuration](#configuration)
- [Tips & Best Practices](#tips--best-practices)
- [Troubleshooting](#troubleshooting)

---

## Installation

### Quick Start

```bash
npx get-shit-done-cc
```

The installer will prompt you to choose:
1. **Runtime**: Claude Code, OpenCode, Gemini, or all
2. **Location**: Global (all projects) or local (current project only)

### Recommended Setup

For the best experience, run Claude Code with permissions skipped:

```bash
claude --dangerously-skip-permissions
```

This prevents constant approval prompts for commands like `date`, `git commit`, etc.

### Verify Installation

Inside Claude Code, verify GSD is installed:

```
/gsd:help
```

You should see a list of all GSD commands.

### Updating

GSD evolves quickly. Update periodically:

```bash
npx get-shit-done-cc@latest
```

---

## Basic Workflow

GSD follows a simple cycle for each phase of your project:

```
1. /gsd:new-project      → Define what you're building
2. /gsd:discuss-phase 1  → Share your vision for this phase
3. /gsd:plan-phase 1     → Research and create execution plans
4. /gsd:execute-phase 1  → Build it automatically
5. /gsd:verify-work 1    → Test that it works

Repeat steps 2-5 for each phase until complete
```

### What GSD Creates

When you run GSD, it creates a `.planning/` directory in your project:

```
.planning/
  PROJECT.md           # Your project vision
  REQUIREMENTS.md      # What's in scope (v1, v2, out of scope)
  ROADMAP.md          # Phases and progress
  STATE.md            # Project memory across sessions
  config.json         # Your preferences
  phases/
    01-foundation/
      01-CONTEXT.md      # Your implementation decisions
      01-RESEARCH.md     # Domain research
      01-01-PLAN.md      # Executable plan
      01-01-SUMMARY.md   # What was built
```

---

## Complete Example: Building a Blog

Let's walk through building a simple blog application with Next.js.

### Step 1: Initialize Project

```
/gsd:new-project
```

**What happens:**

GSD asks: *"What do you want to build?"*

You respond:
> A personal blog with markdown posts, syntax highlighting for code, and a clean reading experience. I want to write posts in markdown files and have them automatically render with good typography.

GSD will ask follow-up questions to understand your vision:
- What tech stack? (You: "Next.js 15 with App Router, TypeScript, and Tailwind")
- Who's the audience? (You: "Developers reading technical content")
- Dark mode? (You: "Yes, respects system preference")
- Comments? (You: "Not in v1, maybe v2")
- SEO important? (You: "Yes, proper meta tags and OpenGraph")

After understanding your project, GSD:
1. ✅ Creates `PROJECT.md` with your vision
2. ✅ Optionally researches the domain (markdown rendering, syntax highlighting)
3. ✅ Extracts requirements (what's v1, v2, out of scope)
4. ✅ Creates a roadmap with phases

**Example roadmap:**
```
Phase 1: Foundation & Setup
Phase 2: Markdown Rendering
Phase 3: Post Listing & Navigation
Phase 4: Dark Mode & Polish
```

### Step 2: Discuss Phase 1

```
/gsd:discuss-phase 1
```

**What happens:**

GSD analyzes Phase 1 and asks about your preferences:

- Layout preference? (You: "Centered content, max-width 720px")
- Styling approach? (You: "Utility-first with Tailwind, minimal custom CSS")
- File organization? (You: "Posts in `/content/posts/`, components in `/components/`")
- Navigation style? (You: "Simple header with home link and about page")

GSD saves your decisions to `01-CONTEXT.md`. This guides the planner to build what you actually want.

### Step 3: Plan Phase 1

```
/gsd:plan-phase 1
```

**What happens:**

GSD:
1. ✅ Researches how to implement Phase 1 (reads your CONTEXT.md for guidance)
2. ✅ Creates 2-3 atomic plans, each with 2-3 tasks
3. ✅ Verifies plans achieve phase goals

**Example plans created:**
- `01-01-PLAN.md`: "Next.js Setup & Configuration"
  - Task 1: Create Next.js 15 project with TypeScript
  - Task 2: Configure Tailwind with typography plugin
  - Task 3: Set up basic layout with 720px max-width

- `01-02-PLAN.md`: "Content Structure & Routing"
  - Task 1: Create `/content/posts/` directory structure
  - Task 2: Add example markdown posts
  - Task 3: Set up dynamic routing for posts

Plans are small (2-3 tasks each) to prevent context degradation.

### Step 4: Execute Phase 1

```
/gsd:execute-phase 1
```

**What happens:**

GSD executes all plans for Phase 1:
1. ✅ Groups plans into waves (parallel where possible)
2. ✅ Spawns fresh executor agents for each plan
3. ✅ Each task gets its own atomic git commit
4. ✅ Creates summary after each plan completes

**Example git log:**
```
docs(01-02): complete content structure plan
feat(01-02): set up dynamic routing for posts
feat(01-02): add example markdown posts
feat(01-02): create content directory structure
docs(01-01): complete setup plan
feat(01-01): set up basic layout with centered content
feat(01-01): configure Tailwind with typography
feat(01-01): create Next.js 15 project
```

**You can walk away.** When you return, Phase 1 is complete with clean git history.

### Step 5: Verify Phase 1

```
/gsd:verify-work 1
```

**What happens:**

GSD walks you through testing what was built:

```
Testing Phase 1 deliverables:

1. Next.js dev server starts without errors
   Visit http://localhost:3000 - does it load? (yes/no/describe issue)
```

You respond: `yes`

```
2. Content is centered with 720px max-width
   Resize browser window - does content stay centered? (yes/no/describe issue)
```

You respond: `yes`

```
3. Example posts are accessible
   Visit http://localhost:3000/posts/hello-world - does it render? (yes/no/describe issue)
```

You respond: `no - getting 404 error`

**If issues found:**

GSD automatically:
1. ✅ Spawns debugger agent to diagnose the 404 issue
2. ✅ Finds root cause (routing configuration error)
3. ✅ Creates fix plan ready for execution

You then run:
```
/gsd:execute-phase 1
```

GSD executes only the fix plans, then verification passes.

### Step 6: Continue to Next Phase

```
/gsd:discuss-phase 2
/gsd:plan-phase 2
/gsd:execute-phase 2
/gsd:verify-work 2
```

Repeat the cycle for each phase:
- Phase 2: Markdown rendering with syntax highlighting
- Phase 3: Post listing and navigation
- Phase 4: Dark mode and polish

### Step 7: Complete the Milestone

When all phases are done:

```
/gsd:complete-milestone
```

**What happens:**

GSD:
1. ✅ Archives the milestone to `.planning/milestones/archive/`
2. ✅ Tags the release in git (`v1.0.0`)
3. ✅ Clears STATE.md for next milestone

### Step 8: Plan Next Version (Optional)

```
/gsd:new-milestone
```

Start planning v2 features (comments, RSS feed, etc.) using the same workflow.

---

## Command Reference

### Core Workflow

| Command | When to Use |
|---------|-------------|
| `/gsd:new-project` | Start a brand new project |
| `/gsd:discuss-phase [N]` | Before planning, share your vision for how this phase should work |
| `/gsd:plan-phase [N]` | Create execution plans for a phase |
| `/gsd:execute-phase <N>` | Build the phase (spawns agents, creates commits) |
| `/gsd:verify-work [N]` | Manually test that the phase works correctly |
| `/gsd:complete-milestone` | Archive current milestone and tag release |
| `/gsd:new-milestone [name]` | Start planning the next version |

### Navigation

| Command | When to Use |
|---------|-------------|
| `/gsd:progress` | See where you are in the roadmap |
| `/gsd:help` | List all commands |
| `/gsd:update` | Update GSD to latest version |

### Brownfield Projects

| Command | When to Use |
|---------|-------------|
| `/gsd:map-codebase` | Before `/gsd:new-project` if you have existing code |

### Phase Management

| Command | When to Use |
|---------|-------------|
| `/gsd:add-phase` | Add a new phase to the end of the roadmap |
| `/gsd:insert-phase [N]` | Insert urgent work between existing phases |
| `/gsd:remove-phase [N]` | Remove a future phase you no longer need |
| `/gsd:list-phase-assumptions [N]` | Preview what Claude plans to build before planning |

### Utilities

| Command | When to Use |
|---------|-------------|
| `/gsd:quick` | One-off tasks that don't need full planning (bug fixes, small features) |
| `/gsd:add-todo [desc]` | Capture an idea for later |
| `/gsd:check-todos` | List your pending todos |
| `/gsd:debug [desc]` | Systematic debugging with persistent state |
| `/gsd:settings` | Configure GSD behavior |
| `/gsd:set-profile <profile>` | Switch between quality/balanced/budget model profiles |

### Session Management

| Command | When to Use |
|---------|-------------|
| `/gsd:pause-work` | Stopping mid-phase? Create a handoff document |
| `/gsd:resume-work` | Continue from where you left off |

---

## Configuration

### Access Settings

```
/gsd:settings
```

GSD will walk you through configuring:
- **Mode**: `interactive` (confirm each step) or `yolo` (auto-approve everything)
- **Depth**: `quick`, `standard`, or `comprehensive` planning
- **Model profile**: Which Claude models to use for different agents
- **Workflow agents**: Toggle research, plan checking, verification

### Model Profiles

Control cost vs quality:

| Profile | Planning | Execution | Verification | Best For |
|---------|----------|-----------|--------------|----------|
| `quality` | Opus | Opus | Sonnet | Critical projects |
| `balanced` | Opus | Sonnet | Sonnet | Default (recommended) |
| `budget` | Sonnet | Sonnet | Haiku | Prototypes, learning |

Switch profiles:
```
/gsd:set-profile budget
```

### Git Branching

By default, GSD commits to your current branch. You can enable automatic branching:

```
/gsd:settings
```

Select **Git branching strategy**:
- `none` - Commits to current branch (default)
- `phase` - Creates branch per phase, merges when phase completes
- `milestone` - Creates one branch for entire milestone

At milestone completion, GSD offers squash merge (recommended) or merge with history.

---

## Tips & Best Practices

### 1. Use `/gsd:discuss-phase` Generously

The more context you provide during discussion, the better the results:

❌ **Skipping discussion:**
```
/gsd:plan-phase 1
```
Result: Reasonable defaults, but may not match your vision

✅ **Using discussion:**
```
/gsd:discuss-phase 1
```
Result: Plans built exactly how you want them

### 2. Start with Existing Code

If you have an existing codebase, run `/gsd:map-codebase` first:

```
/gsd:map-codebase
/gsd:new-project
```

This analyzes your:
- Tech stack and dependencies
- Architecture patterns
- Code conventions
- Common pitfalls

Then when you run `/gsd:new-project`, questions focus on what you're *adding*, not what already exists.

### 3. Use Quick Mode for Small Tasks

Don't run full planning for every little thing:

```
/gsd:quick
> "Fix typo in homepage title"
```

Quick mode gives you GSD guarantees (atomic commits, state tracking) without the overhead.

### 4. Check Progress Regularly

```
/gsd:progress
```

Shows:
- Current phase and status
- Completed vs remaining work
- What to run next

### 5. Leverage Todos

Capture ideas as you work:

```
/gsd:add-todo "Add RSS feed for blog posts"
/gsd:add-todo "Optimize images with next/image"
/gsd:add-todo "Add reading time estimate to posts"
```

Later:
```
/gsd:check-todos
```

GSD shows your captured ideas and helps prioritize them.

### 6. Debug Systematically

When something breaks:

```
/gsd:debug "Users getting 500 error on login"
```

GSD:
- Creates persistent debug state
- Spawns debugger agents
- Traces root cause systematically
- Creates fix plans

Much better than ad-hoc debugging in main conversation.

### 7. Use Atomic Git History

Each task gets its own commit. Use this:

```bash
# Find when a feature was added
git log --grep="01-02"

# See what a specific task changed
git show <commit-hash>

# Revert a specific task
git revert <commit-hash>

# Bisect to find breaking task
git bisect start
git bisect bad HEAD
git bisect good v1.0.0
# Git will pinpoint exact failing task
```

### 8. Pause and Resume Freely

Stopping mid-phase?

```
/gsd:pause-work
```

Creates a handoff document with:
- Current position
- What's done
- What's next
- Any blockers

Later (even in a new Claude session):

```
/gsd:resume-work
```

GSD loads the handoff and continues exactly where you left off.

---

## Troubleshooting

### "Command not found" after install

**Fix:** Restart Claude Code to reload slash commands.

Verify files exist:
- Global: `~/.claude/commands/gsd/`
- Local: `./.claude/commands/gsd/`

### Plans executing slowly

**Try:**
1. Switch to budget profile: `/gsd:set-profile budget`
2. Disable optional agents: `/gsd:settings` → disable research or plan checking
3. Use quick mode for simple tasks: `/gsd:quick`

### Phase execution failed

**Check:**
1. Read the error in the executor output
2. Check `STATE.md` for blockers
3. Use `/gsd:debug` to diagnose systematically
4. Fix the issue, then re-run `/gsd:execute-phase`

### GSD seems "off track"

**Fix:**
1. Check `PROJECT.md` - does it match your vision?
2. Edit it if needed
3. Use `/gsd:discuss-phase` to provide more context
4. Update `STATE.md` with important decisions

### Git merge conflicts

**Cause:** Parallel plan execution modified same files

**Fix:**
1. Resolve conflicts manually
2. Continue with `git add` + `git commit`
3. Run `/gsd:execute-phase` to continue remaining plans

### Want to change direction mid-phase

**Options:**

1. **Pause and replan:**
   ```
   /gsd:pause-work
   # Edit ROADMAP.md or requirements
   /gsd:plan-phase 1 --skip-research
   /gsd:resume-work
   ```

2. **Insert urgent phase:**
   ```
   /gsd:insert-phase 2
   ```
   This renumbers phases, letting you inject high-priority work.

3. **Use quick mode:**
   ```
   /gsd:quick
   > "Change authentication to use OAuth instead of JWT"
   ```

---

## Example Project Types

### Web App with Database
```
Phase 1: Next.js setup + database schema
Phase 2: API routes + authentication
Phase 3: Core features (CRUD)
Phase 4: UI polish + deployment
```

### CLI Tool
```
Phase 1: Argument parsing + config loading
Phase 2: Core commands implementation
Phase 3: Output formatting + error handling
Phase 4: Testing + documentation
```

### Chrome Extension
```
Phase 1: Manifest + popup UI
Phase 2: Content script + messaging
Phase 3: Storage + settings
Phase 4: Polish + Chrome Web Store prep
```

### API Service
```
Phase 1: Express setup + middleware
Phase 2: Database models + migrations
Phase 3: Endpoints + validation
Phase 4: Auth + rate limiting + deployment
```

---

## Getting Help

- **In Claude Code:** `/gsd:help`
- **GitHub Issues:** https://github.com/glittercowboy/get-shit-done/issues
- **Discord Community:** `/gsd:join-discord`

---

## Key Takeaways

1. **GSD automates the build process** - You describe what you want, GSD researches, plans, and builds it
2. **Fresh context per plan** - No degradation, consistent quality throughout
3. **Atomic git commits** - Clean history, easy debugging, surgical reverts
4. **Human verification matters** - `/gsd:verify-work` catches issues automated tests miss
5. **Iterate freely** - Pause, resume, insert phases, debug systematically

**The workflow:**
```
Describe → Discuss → Plan → Execute → Verify → Repeat
```

Ship working software consistently. No enterprise theater. Just build cool stuff.
