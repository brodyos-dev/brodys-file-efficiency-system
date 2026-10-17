---
name: brodys-file-efficiency-system
description: Sets up an AI-independent, file-based knowledge base (journals, backlog, decisions, logs), installs a real engineering skill workflow, and builds custom skills from the user's repeated tasks. Use when the user asks to set up their project files, knowledge base, or workflow efficiency system, says "run the file efficiency system", or asks to check, repair, or customize that setup.
---

# Brody's File Efficiency System

You are the project operator. Build an AI-independent knowledge base in a folder on the user's PC. Then set up an engineering workflow and custom skills on top of it. The files are the source of truth. Chat memory is not. Any AI must be able to read the folder and continue the work.

Default project context: a game built in Unreal Engine, with models made in Blender through a Blender MCP connection. If the user's project differs, adapt interview questions 1-4 and 9-16 to the real stack. Keep the rest.

## MODEL AND EFFORT FOR THIS RUN

Spend tokens where they matter. Tiers mean the newest model in each family: Top (for example Opus), Mid (for example Sonnet), Light (for example Haiku), or the nearest equivalent in the user's AI tool. At the start, tell the user this plan in one line, and name the one setting to change if the chat is on a different one.

| Steps | Tier | Effort | Why |
|---|---|---|---|
| 0, 0.5, 1, 2, 3, 8, 12 | Light | Low | Reading, questions, creating files |
| 4, 5, 7, 9, 10, 10B, 11 | Mid | Medium | Installs, hooks, building skills, verification |
| 6 (first grill, ADRs) | Top | Medium | Wrong design decisions are costly |

The user's pick always wins. Step 10B builds the permanent version of this table for the game workflow.

## RULES

- Do nothing but Step 0 and Step 0.5 until the interview in Step 1 is finished.
- Write everything durable to files. Never rely on chat history or built-in memory.
- Use plain Markdown and CSV only. No proprietary formats.
- Keep files short. Split any file that passes ~300 lines.
- Keep /00_START_HERE.md under 150 lines. Link out to detail files.
- Confirm before deleting or overwriting anything. Move retired files to /_archive instead of deleting.
- Never store passwords, API keys, or payment data in the knowledge base.
- Keep the knowledge base folder separate from the project folder. For Unreal, never put Content, Saved, Intermediate, or Binaries inside the knowledge base. Link to the project by path.
- Use Windows-safe paths and filenames: no special characters, lowercase-kebab-case, dates as YYYY-MM-DD.
- Check whether a tool, connector, or skill can do a task before telling the user to do it by hand.
- Install third-party skills only from the repo named in Step 5. Show each install command and wait for the user's OK before running it.
- Pending-plan rule: when the user and AI agree on a change that is not built yet, write it to /01_state/pending/YYYY-MM-DD-name.md in the same turn (what, why, files touched, steps left, owner). Every new chat and every context compaction starts by reading /01_state/pending/. When done, mark the file done and move it to /_archive/pending/.
- Expectations: /01_state/expectations.md holds standing rules for anyone working on the project, newest last. Read it every session. Append a rule only when the user states it as standing. Never rewrite old rules; mark them superseded.
- Speed rules: test only what changed. No helper agents for small jobs. Run one heavy job at a time (Unreal build, cook, shader compile, Blender bake). Read only the files the change needs. Run a script instead of re-reasoning a repeatable step.
- If a skill named brody-comms is installed, follow it for every reply. Otherwise follow OUTPUT STYLE at the end.

## SKILL DESIGN RULES (apply to every skill you build)

1. Script first, prompt second. Any repeatable step becomes a script the skill calls (for example a Blender Python export script, an Unreal Editor Python import script, an asset-name validator). Do not make the AI re-derive a repeatable step each run.
2. One job per skill. Write a specific trigger in the description. Similar skills fight over triggers.
3. Follow the writing-for-agents skill (from Step 5) when writing skills and pointer files.
4. Cap the first batch at 5 custom skills.
5. Register every skill in /08_prompts-and-skills/registry.md.
6. Every skill states its recommended model tier and effort in its first lines (see Step 10B). A skill that mostly runs a script is Light / Low.
7. Two-copy rule: every skill exists in two places, the AI tool's skills folder (the live copy) and /08_prompts-and-skills/skills/<name>/ (the backup copy, tracked by Git). After any skill edit, copy to both and confirm they match with `git diff --no-index --stat <live> <backup>` (or `diff -r` where available). Empty output means they match. Report any mismatch and fix it.

## STEP 0: READ FIRST (read-only)

Fetch https://github.com/mattpocock/skills and read the README. Note the current skill list, the install command for each AI tool, and what the setup skill asks. If the README differs from this file, the README wins. Install nothing yet.

## STEP 0.5: REPEAT-TASK AUDIT

Ask the user to export past AI chats (any tool) and drop them in a folder you can read. Scan them for tasks the user asked for 3 or more times. Rank by frequency and time cost. Save the list to /10_inbox/repeat-task-audit.md. Use it in Step 10 to propose skills from real behavior. If the user has no chats, skip this step and say so.

## STEP 1: INTERVIEW

Ask 20 multiple-choice questions in 5 batches of 4. Wait for answers after each batch. Each question has lettered options plus "Other (I'll type it)". Do not skip any question.

Batch 1: Project
1. Game genre? a) Action/adventure b) Shooter c) RPG d) Horror e) Puzzle/platformer f) Sim/strategy g) Other
2. Project stage? a) Idea only b) Prototype c) Vertical slice d) Mid-production e) Near release
3. Target platform? a) PC only b) PC + console c) Mobile d) VR e) Undecided
4. Target release date? a) No date b) Within 6 months c) 6-12 months d) 1-2 years e) 2+ years

Batch 2: Team and tools
5. Team size? a) Solo b) 2-3 people c) 4-10 d) 10+
6. Hours per week on this project? a) Under 5 b) 5-15 c) 15-30 d) 30+
7. Who uses the knowledge base? a) Only me b) Me and a partner c) A small team d) Contractors will read it too
8. Which AI tool do you use most? (Sets the skill install method.) a) Claude Code b) Claude desktop app c) Codex d) Cursor or VS Code Copilot e) Gemini CLI f) Other

Batch 3: Tech setup
9. Unreal Engine version? a) 5.4 b) 5.5 c) 5.6 or newer d) 4.x e) I'm not sure
10. Code approach? a) Blueprints only b) Mostly Blueprints, some C++ c) Mostly C++ d) Undecided
11. Version control for the project? a) None yet b) Git c) Git + LFS d) Perforce e) Other
12. Blender MCP use today? a) Generate models from prompts b) Edit/clean existing models c) Materials and textures d) Rigging/animation e) Mix of these f) Not set up yet

Batch 4: Assets and pipeline
13. Where do assets come from? a) All made by me b) Blender + marketplace c) Mostly marketplace d) AI-generated + cleanup e) Mix of everything
14. Asset naming convention? a) None yet b) Unreal standard (SM_, T_, M_, BP_) c) My own d) Help me pick one
15. Biggest time sink right now? a) Modeling b) Texturing/materials c) Importing into Unreal d) Level design e) Gameplay code/Blueprints f) Bugs g) Planning and tracking
16. Do you track asset licenses and AI-generation disclosure (needed for Steam and other stores)? a) Yes, already b) No c) No, but I want to start d) Not sure what that means

Batch 5: Knowledge base and workflow
17. Folder depth? a) Minimal (under 10 folders) b) Moderate c) Detailed d) You decide
18. Backup and sync? (Choose one.) a) Private GitHub repo for the knowledge base (needed for end-session) b) GitHub repo + OneDrive/Google Drive sync c) OneDrive/Google Drive sync only d) External drive copies e) None
19. Self-improvement depth? a) Light: update lessons after each session b) Standard: lessons log + weekly review + /retro each session c) Strict: standard + monthly rule audit d) Off
20. Where do tickets live? a) Local Markdown files in the knowledge base b) GitHub Issues c) Both: GitHub Issues primary, mirrored locally d) Other

## STEP 2: CREATE THE FOLDER

Ask where on the PC to create it. Scale the structure to Q17. Minimum:

```
/00_START_HERE.md        Handoff file: rules, file map, resume prompt, "which skill when" table
/01_state/               current-status.md, roadmap.md, milestones.md (definition of done per milestone),
                         settings.md, expectations.md, locked-facts.json,
                         pending/ (agreed but unbuilt changes, one dated file each)
/02_backlog/             backlog.csv, bugs.csv, done.csv, tickets/, specs/ (if Q20 = a or c)
/03_decisions/           decision-log.md, adr/
/04_logs/
  daily/YYYY-MM-DD.md    One entry per session, links to topic journals touched
  handoffs/              Handoff docs for switching AIs or chats
  journals/              Two files per topic, side by side:
                           <topic>.md      working file, current truth only (sections below)
                           <topic>-log.md  append-only history; split by month past ~300 lines
    topics: app-build  unreal-code  blender  assets-and-import
    level-and-design  art-and-audio  bugs-and-testing  tools-and-workflow
    (add or drop topics based on Q10, Q12, Q15)
  changelog.md
/05_game/                GLOSSARY.md, design-doc, systems, art-direction, asset-pipeline,
                         naming-conventions, unreal-setup, blender-mcp-setup
/06_assets/              asset-register.csv (name, source, license, AI-generated y/n, used y/n)
/07_research/            references, competitors, tutorials (cite sources)
/08_prompts-and-skills/  registry.md, skills/ (backup copy of every skill), scripts/, templates/
/09_improvement/         lessons-learned.md, mistakes-log.md, rules-candidates.md, weekly-review/
/10_inbox/               unsorted notes, repeat-task-audit.md
/_archive/               retired files, superseded-facts/<topic>.md, pending/, skill-versions/
```

Create /08_prompts-and-skills/templates/ with templates for: ticket, ADR, journal working file, log entry, bug report, pending plan. Create /07_ops-style files only if the user asks.

Every topic working file (<topic>.md) has exactly these sections:
- Charter: what this topic covers, in 2-3 lines. Rarely changes.
- Current state: where the work stands now. Rewrite it, do not append.
- Standing facts: settled facts that stay true until replaced (engine version, export scale, naming rules).
- Waiting on me: open questions and decisions only the user can make.
Rule: the working file holds current truth only. When a fact changes, move the old wording to /_archive/superseded-facts/<topic>.md with the date, then write the new one. Everything that happened goes in <topic>-log.md, append-only, newest last. Never edit old log lines.

Locked facts: /01_state/locked-facts.json lists facts that must read the same everywhere (engine version, project name, naming prefixes, store target, milestone dates). Format: [{"id": "engine-version", "value": "5.5", "must_appear_in": ["05_game/unreal-setup.md"], "stale_patterns": ["5\\.4"]}]. Fill it from interview answers and the first grill.

Scripts to create in /08_prompts-and-skills/scripts/ (plain Python, Windows-safe):
- check_paths.py: scans every .md file for links and file paths and reports ones that do not exist.
- check_facts.py: reads locked-facts.json and reports any stale pattern found and any must_appear_in file missing the value.
Run both in end-session and in Step 11. Report findings. Do not auto-fix facts without the user's OK.

Create /04_logs/journals/tools-and-workflow.md with an MCP inventory section: each connected MCP server, what it does, known quirks.

Seed /01_state/expectations.md with 3-5 rules from the interview (for example the naming convention, the backup rule, the speed rules). Show them to the user.

registry.md columns: skill name, trigger, inputs, outputs, scripts used, model tier, effort, created, last used, est. time saved per run.

## STEP 3: BACKLOG IMPORT

Ask for all notes, TODOs, repo issues, and chat exports. Convert to backlog.csv with columns: id, title, type, priority, status, est, created, updated, notes. If Q20 = a or c, also write one file per ticket in /02_backlog/tickets/. Mark unknowns "unverified". Show the result before saving the final version.

## STEP 4: GIT, GITHUB, AND SAFETY HOOKS

Knowledge base, based on Q18:
1. Check that Git is installed. If not, give the install link.
2. Run git init in the knowledge base folder.
3. Create a .gitignore: secrets and .env files, OS junk (Thumbs.db, desktop.ini), Unreal and Blender generated or binary files (Content, Saved, Intermediate, Binaries, DerivedDataCache, *.blend1, *.uasset, *.umap).
4. Help create a private GitHub repo and set it as origin. Check for the GitHub CLI or a GitHub connector before telling the user to do any step by hand.
5. Make the first commit and push.
If Q18 = no GitHub, skip steps 4-5 and make local commits only.

Safety hooks (so safety does not depend on the AI remembering rules):
- Add a git pre-commit hook that scans staged changes for secrets (API keys, tokens, passwords) and blocks the commit on a match.
- Block force push: set up a pre-push hook or the AI tool's hook system (for example Claude Code hooks) to reject `--force` and `--force-with-lease`.
- Test each hook with a harmless fake secret. Show the user the result.

Permissions allowlist: propose a list of commands the AI may run without asking (git status, git diff, file reads, builds, tests). Require confirmation for deletes, pushes, installs, and anything outside the two folders. Show the list. Apply it only after the user's OK, using the AI tool's own permission settings.

Game project: if Q11 = a, set up Git for the game project first, with an Unreal-specific .gitignore and Git LFS for large binaries. The engineering skills in Step 5 assume a Git repo. If Q11 = d (Perforce), say which skills still apply and which do not.

Backup gap: the knowledge base repo does not cover game assets. State this, and confirm the game project has its own off-machine backup (Git LFS remote, Perforce server, or a scheduled copy).

## STEP 5: INSTALL THE ENGINEERING SKILLS

Source: https://github.com/mattpocock/skills
1. Pick the install method from the README that matches Q8. Use one method only (plugin OR npx). Both together install every skill twice. If the method needs Node.js or npm, check it is installed.
2. Show the exact command. Wait for OK. Run it. If the installer asks which skills to take, include the setup skill.
3. Run the setup skill (setup-matt-pocock-skills) once, in the game project repo. Give the agent both folders. Answer its questions from the interview:
   - Issue tracker: from Q20. Local files go in /02_backlog/tickets/.
   - Triage labels: propose defaults for a game project. Show before applying.
   - Docs location: GLOSSARY.md in /05_game/, ADRs in /03_decisions/adr/.
   If the setup skill cannot point outside the game repo, say so. Propose a fallback that keeps one source of truth (docs in the game repo plus a pointer file in the knowledge base). Wait for the user's choice.
4. Write a "which skill when" table into /00_START_HERE.md, built from the README's current skill list. Start from these mappings and drop any that do not fit:
   - grill-with-docs: before every new feature or system change. Updates GLOSSARY.md and ADRs.
   - grill-me: planning with no code (story, scope).
   - to-spec then to-tickets: turn a planned feature into a spec and tickets.
   - tdd: pure gameplay logic in C++ (Unreal automation tests). Skip for Blueprints, levels, art.
   - diagnosing-bugs: crashes, hard bugs, performance drops.
   - prototype: throwaway mechanic prototypes.
   - research: cited notes saved to /07_research/.
   - handoff: long chats, or before switching AI tools.
   - wait-what: when an explanation does not land.
   - retro: end of session (Q19 = b or c).
   - improve-codebase-architecture, code-review, implement: C++ work only (Q10 = b or c).
   - wayfinder: whole-game or milestone-sized planning.
   - writing-for-agents: when writing skills and pointer files.
   State where these skills fit poorly in an Unreal and Blender workflow (Blueprints, levels, art, MCP modeling) and what to use instead.

## STEP 6: FIRST GRILL

Run grill-with-docs on the project. Goals:
- Build the first /05_game/GLOSSARY.md (core mechanics, asset types, level and world terms).
- Write ADRs for the decisions behind Q9, Q10, Q11.
- Record open questions in /01_state/current-status.md.
- Draft /01_state/milestones.md: one page per milestone (prototype, vertical slice, alpha, beta, release) with pass/fail criteria.

## STEP 7: END-SESSION SKILL

Build a skill named "end-session" in /08_prompts-and-skills/end-session/SKILL.md. Follow the skill design rules above. Tell the user how to install it for their AI tool. When the user says "end session" (or similar), it runs:
1. Read what changed this session.
2. For each topic touched: rewrite Current state, move any replaced fact to /_archive/superseded-facts/<topic>.md, update Waiting on me, and append dated lines to <topic>-log.md. Write the daily entry and link the journals. Check /01_state/pending/ and mark finished plans done.
3. Update current-status.md, backlog.csv, tickets, bugs.csv, done.csv, decision-log.md, GLOSSARY.md, asset-register.csv, lessons-learned.md, and registry.md (last-used dates) as needed.
4. Run check_paths.py and check_facts.py. Report findings. Scan staged changes for secrets. If found, stop, name the file, ask.
5. Run git status. Show a short summary of what will be committed.
6. Commit: "YYYY-MM-DD: short summary of the session".
7. Push to origin. Never force push.
8. Report: commit hash, files changed, push result, next action in one line.
On failure, state the cause and the fix. Common cases: no remote, authentication needed, merge conflict, push rejected. Do not delete or overwrite anything to fix an error. Ask first.
This skill never calls another user-invoked skill. The user runs /retro before end-session.

## STEP 8: HANDOFF, SAVE, AND RESUME

Write a resume prompt in /00_START_HERE.md:
"Read /00_START_HERE.md, then /01_state/current-status.md, then /05_game/GLOSSARY.md, then /02_backlog/backlog.csv. Summarize where we are and propose the next action."
Test it: summarize the project from the files alone and show the user.
Build two more skills in /08_prompts-and-skills/ (follow the skill design rules; both Light / Low):
- save-session: a mid-chat checkpoint for when the chat is long or the user must stop. It writes any agreed-but-unbuilt work to /01_state/pending/, updates the working file of each topic touched, appends to the logs, and writes a handoff file to /04_logs/handoffs/YYYY-MM-DD-hhmm.md (what was done, what is in progress, exact next action, files open, commands to re-run). It does not commit or push.
- resume-session: for a new chat, a new AI tool, or after compaction. It reads, in order: 00_START_HERE.md, expectations.md, /01_state/pending/, the newest file in /04_logs/handoffs/, current-status.md, the working files of the topics named in the handoff, then the top 10 backlog items. It replies with where things stand, what is pending, and the one next action.
Difference from end-session: save-session is a checkpoint with no Git. end-session closes the day and commits.
Create a one-line pointer file for each AI tool the user uses (CLAUDE.md, AGENTS.md) in both the knowledge base and the game project. Each says only: "Read <path to knowledge base>/00_START_HERE.md."

## STEP 9: SELF-IMPROVEMENT LOOPS

Use the depth from Q19.
- After each session: log what broke, what worked, and what cost time in lessons-learned.md and mistakes-log.md. In standard and strict modes, run /retro and save suggestions to rules-candidates.md.
- Weekly: review the journals. Prune stale backlog items. Update the roadmap. Move repeated lessons to rules-candidates.md.
- Weekly: run check_paths.py and check_facts.py, and confirm every skill's live copy matches its backup copy (design rule 7). Archive pending plans older than 30 days after asking the user.
- Weekly skill review: read registry.md. List skills unused for 30 days (retire or fix). List tasks done by hand 3+ times (new skill candidates). Save to /09_improvement/weekly-review/.
- Monthly (strict mode): propose promoting proven rules into /00_START_HERE.md. Ask approval for each. Retire rules that no longer apply.
- Offer a scheduled task that runs the weekly review and saves the report. Create it only after the user agrees.
- Never change the user's rules or instructions without approval.

## STEP 10: CUSTOM SKILL OFFER

Use repeat-task-audit.md, the journals, the backlog, and the interview. Propose up to 5 custom skills. For each: name, what it does, trigger, scripts it needs, time saved. Candidates, when the audit supports them:
- Blender-to-Unreal batch pipeline: export presets (scale, axis, pivots, FBX), Unreal import script, asset-register entry, in one run
- Asset intake: naming, license check, asset-register entry
- Asset naming and folder audit: checks the Content folder against the naming convention
- Build and cook: packaged build through UAT (BuildCookRun), logs result, records failures in bugs-and-testing.md
- Playtest intake: raw playtest notes to triaged bug tickets
- Performance check: Unreal stat commands and Unreal Insights, results logged to a journal
- Blueprint or C++ system documentation from a short description
- Blender MCP session routine: scene setup, export settings, cleanup
- Start-of-session routine
- Store-page and AI-disclosure prep, as a recurring milestone check
Ask which to build. Build only the approved ones. Save drafts and scripts in /08_prompts-and-skills/. Add each to registry.md.

## STEP 10B: MODEL AND EFFORT SETUP (run before Step 11)

Goal: heavy models and high effort for hard thinking; light models and low effort for routine work and script runs.

1. Ask 3 multiple-choice questions, each with "Other (I'll type it)":
   a. Which models can you switch between in your AI tool? a) Three tiers (top, mid, light) b) Two tiers c) One model only d) Not sure (check the tool's model picker and tell me)
   b. How tight are your usage limits? a) I often hit them b) Sometimes c) Rarely d) I pay per token and cost matters
   c. Can your AI tool set a model or effort for a single task or helper agent? a) Only for the whole chat b) Yes, for helper agents too c) No d) Not sure (check and tell me)
2. Build /08_prompts-and-skills/model-effort-defaults.md. Put the tier-to-model mapping at the top (check the vendor's current model list live, not from memory). Then one row per task type: task type, tier, effort, why. Starting rows, adjusted to the answers above:
   - Architecture, ADRs, big design (grill-with-docs, wayfinder, to-spec): Top / Medium. High only for a one-off redesign.
   - C++ gameplay code and hard bugs (tdd, diagnosing-bugs, implement, code-review): Top / Medium. High for crashes.
   - Blueprint and system docs, GLOSSARY updates, ticket writing (to-tickets): Mid / Low.
   - Blender MCP modeling sessions: Mid / Medium.
   - Blender-to-Unreal export and import runs, asset intake, naming audit, build and cook: Light / Low. The script does the work.
   - Research: Mid / Medium.
   - Playtest notes to tickets, bug triage: Mid / Low.
   - Journals, end-session, save-session, resume-session, status and backlog edits, git: Light / Low.
   - Weekly review, retro: Mid / Low.
   - Store page and AI-disclosure prep: Mid / Medium. Accuracy matters.
   Drop tiers the user does not have. With one model only, keep the effort column and skip the tier column.
3. Rules for every session:
   - Start each task on its default. Go up one level only for a one-off hard job, then drop back.
   - The user's pick wins. Keep it for that chat.
   - The most expensive tier needs the user's OK first.
   - Script runs, journal writes, git, and status updates use Light / Low.
   - Helper agents: no helper agents for small jobs. For big multi-file jobs use the Light tier unless the work needs more, and repeat the model and effort rules in the helper's prompt.
   - Read only the files the change needs. Prefer a script over re-reasoning a repeatable step.
   - If the tool lets you set the model or effort for a helper agent or the next step, set it. If only the user can switch the chat's model, say so in one line and name the one setting to change. Never say you switched when you cannot.
4. Add a "Recommended model/effort: <tier> / <effort>" line to the top of every skill built so far, including end-session. Fill the model tier and effort columns in registry.md.
5. Build a skill named "pick-model-effort" in /08_prompts-and-skills/pick-model-effort/SKILL.md (Light / Low). Trigger: the user asks "which model for this," or a new task starts. It does this:
   1. Classify the task against model-effort-defaults.md.
   2. Reply in two lines: the recommended tier and effort, and the one setting to change if the chat is on a different one. If the current setting is unknown, ask once.
   3. If the task splits into parts, say which parts to hand to helper agents on the Light tier.
   4. If no row fits, pick the nearest row, say so, and offer to add a new row.
6. Review the table in the weekly review. List tasks that ran on a heavier tier than they needed, and tasks that failed or needed redoing on a lighter tier. Propose row changes. Apply them only with the user's OK, and log each change in decision-log.md with what would reverse it.

## SESSION PROTOCOL (every session)

1. Read the start file, expectations.md, everything in /01_state/pending/, status, GLOSSARY.md, and top 10 backlog items. Do the same after any context compaction. For a new chat or a new AI tool, run resume-session.
2. Say where the project stands and the next action. Name the recommended model and effort for today's task (pick-model-effort); if the chat is on a different setting, name the one setting to change.
3. Before any feature or system change, run /grill-with-docs.
4. Work. Use the "which skill when" table.
5. Standard or strict mode: run /retro.
6. Run end-session. If the chat is long or the user must stop without closing the day, run save-session.
7. End with the next action in one line.

## OUTPUT STYLE (only if brody-comms is not installed)

Active voice, short sentences, plain words. Lead with the answer. State errors flatly: cause, then fix. No filler.

## STEP 11: VERIFY AND SELF-REPAIR

Run after Step 10. Run again any time the user says "check the setup."
1. Confirm /01_state/settings.md exists and holds all 20 interview answers. Create it if missing.
2. Test each step's output:
   - Folder exists with the expected files.
   - Git repo is clean and the remote is reachable.
   - Each hook blocks a harmless fake secret and a fake force push.
   - Installed skills appear in the AI tool's skill list, with no duplicates.
   - The setup skill's config (tracker, labels, docs paths) is recorded.
   - end-session does a dry run (no commit, no push) and reports what it would do.
   - The resume prompt test passes, and resume-session returns the same picture.
   - save-session does a dry run and writes a handoff file.
   - check_paths.py and check_facts.py run and report clean (or list real findings).
   - Every skill matches between the AI tool's skills folder and /08_prompts-and-skills/skills/ (design rule 7).
   - Every topic has a working file with all four sections and a matching -log file.
   - Every skill has a recommended model and effort line, and registry.md matches.
3. Log every failure or skipped step in /09_improvement/setup-issues.md: step, exact error, cause, fix, status.
4. Fix it yourself using tools, connectors, scripts, and web search. Ask for approval only for installs, deletes, overwrites, and pushes.
5. If a step in this skill is wrong or outdated, edit this skill file directly. It belongs to the user now. Before each edit, copy the current version to /_archive/skill-versions/brodys-file-efficiency-system-YYYY-MM-DD.md, and log what changed and why in setup-issues.md. The skill file lives in the AI tool's skills folder, outside the knowledge base and outside Git, so this archive copy is the only way to revert. If you cannot find or write the skill file (for example the user pasted this as a prompt), save the edited version to /08_prompts-and-skills/brodys-file-efficiency-system.md, tell the user to use that file from now on, and archive the old version the same way. Also keep a backup copy of this skill at /08_prompts-and-skills/skills/brodys-file-efficiency-system/SKILL.md (design rule 7).
6. Report: what passed, what you fixed, what still needs the user. Never ask the user to send anything to anyone else. Solve it here.

## STEP 12: CUSTOMIZE WITH THE USER

Tell the user in plain words: this setup is a starting point, and every part can change. Then ask up to 5 multiple-choice questions, one batch, each with "Other (I'll type it)":
1. Which folders or journals do you not need?
2. Which repeated work has no journal or skill yet?
3. Which steps felt like too much?
4. Which tools do you use that this setup ignores (for example Substance, Jira, Discord, Perforce)?
5. Which workflow should become a skill first?
Apply the answers to this skill file, the folder, and settings.md. Archive the old skill version first, as in Step 11. Show the user what changed.

Write this section into /00_START_HERE.md under "How to change this system":
- Add a journal: create <topic>.md (with the four sections) and <topic>-log.md in /04_logs/journals/, then add the topic to end-session.
- Add a standing rule: tell the AI, and it appends to /01_state/expectations.md.
- Save agreed work for later: say "save session". Pick up later with "resume session".
- Add a skill: say "build a skill for X." The AI follows the skill design rules and registers it.
- Remove something: move it to /_archive. Do not delete.
- Change a setting: edit /01_state/settings.md, or tell the AI what to change.
- Change reply style: edit OUTPUT STYLE in this skill, or install brody-comms.
- Revert a skill change: copy the version you want from /_archive/skill-versions/ back over the skill file.
- Re-run customization: say "customize the file efficiency system."
- Fix a broken step: say "check the setup." The AI finds the cause and fixes it.

## TROUBLESHOOTING (fix these yourself, then log in setup-issues.md)

| Symptom | Cause | Fix |
|---|---|---|
| Install command fails | Node.js or npm missing, or the README command changed | Check `node -v`. Install Node if missing. Re-read the README and use the current command. |
| Skills appear twice | Plugin and npx both installed | Remove one method. Keep the one that matches Q8. |
| Setup skill cannot use a docs path outside the game repo | Skill expects docs inside the repo | Use the fallback in Step 5: docs in the game repo, pointer file in the knowledge base. |
| git push asks for credentials or fails | No auth set up | Run `gh auth login` if the GitHub CLI is installed. Otherwise set up a credential manager and tell the user the exact steps. |
| Hooks do not fire on Windows | Git Bash missing, or hook file not executable | Confirm Git for Windows is installed. Re-create the hook and re-test with the fake secret. |
| AI asks permission for every command | No allowlist | Apply the allowlist from Step 4 in the AI tool's permission settings. |
| Skill never triggers | Description too vague, or it overlaps another skill | Rewrite the trigger in the description. Check registry.md for overlap. |
| Files grow too large | No split rule applied | Split files past ~300 lines. Keep 00_START_HERE.md under 150 lines. |
| Live and backup skill copies differ | Edited one copy only | Pick the newer one, copy it over the other, re-run the diff, log it in setup-issues.md. |
| check_facts.py reports a stale value | A fact changed in one place only | Show the user each hit. With OK, update the file and move the old wording to superseded-facts. |
| LFS or push fails on large files | Binaries tracked without LFS | Track the file types with Git LFS, then recommit. |

## START

Open with 3 sentences: what this does, that every part can be customized, and that the user never needs to send anything to anyone else because the AI checks and fixes its own setup. Then run Step 0, then Step 0.5, then Batch 1. Create no files and install nothing until all 20 questions are answered.
