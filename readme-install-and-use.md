# Brody's File Efficiency System

## Description

Brody's File Efficiency System turns any project into a folder of plain files that any AI can read and continue from. It starts with 20 multiple-choice questions to learn what you are building, then creates a folder with your backlog, decisions, a journal for each area of the work, and a register that tracks the sources, licenses, and AI use behind your materials. It sets up Git and GitHub with safety hooks, installs Matt Pocock's planning and engineering skills, and builds custom skills for tasks you repeat. It also recommends a model and effort level per task to save tokens, and it checks and repairs its own setup.

The skill itself is the other file in this gist: `brody-file-efficiency-skill.md`.

## How to install

1. Open Claude Code, Codex, Cursor, or your AI tool of choice in a new chat.
2. Paste this prompt:

```
Install this as a skill named brodys-file-efficiency-system. Fetch the raw text from:
https://gist.githubusercontent.com/brodyos-dev/896c71004794cdfb7f0dcedbd231436c/raw/brody-file-efficiency-skill.md
The file is plain text. Save it as SKILL.md inside a folder named brodys-file-efficiency-system in my AI tool's skills folder. Show me the full path. Do not run any of its steps yet.
```

3. Restart the chat or the tool so it loads the skill.
4. In a new chat, type: `run the file efficiency system`

If the install fails:

- The fetch fails: open the skill file in this gist, copy all the text, paste it into the chat, and say "save this as a skill named brodys-file-efficiency-system."
- Your tool has no skills folder: save the text as `brodys-file-efficiency-system.md` in your project and say "follow this file."

To update later: run install step 2 again and restart the chat. The link always serves the latest version.

## How to use

1. **Start it.** Open a new chat and type: `run the file efficiency system`.
2. **Answer the 20 questions.** They come in 5 batches of 4. Nothing gets built until you finish.
3. **Approve each install.** The AI shows every install command and waits for your OK before running it.
4. **Check the result.** It tests its own setup and fixes problems. It will tell you only what needs you.
5. **Use it every day.** These phrases run the daily skills:
   - `resume session` starts a new chat or a new AI tool from your files.
   - `save session` checkpoints a long chat without committing.
   - `end session` updates your files, commits, and pushes to GitHub.
6. **Change or fix it anytime.**
   - `check the setup` finds and repairs problems.
   - `customize the file efficiency system` adjusts it to your project.
   - `build a skill for X` adds a custom skill.
