# Moving the program to a new Mac

Written for a one-shot move to a machine with a **different macOS username**, which is the case that needs care — the three scheduled-task prompts hardcode `/Users/jochp/...` and will silently read nothing if those paths don't resolve. A task that can't read `00-PROGRAM.md` doesn't fail loudly; it reconstructs the program from memory, which is precisely what the "source of truth — read, don't reconstruct" instruction exists to prevent. The restore script rewrites them.

## The shape of the problem

Three different kinds of state are in play, and only the first kind actually copies.

**Plain files.** The seven program documents, the three task prompts, and the tracker's `index.html`. These move as bytes.

**Registration state.** The cron schedules, the enabled flags, and the artifact's entry in the Cowork manifest live in Claude's application state, *not* in `~/Claude/`. The proof is sitting on your current disk: `~/Claude/Scheduled/` holds five task directories, but only three are registered. `genai-daily-study` (the old 7am task you deleted) and `genai-evening-build` still have their `SKILL.md` on disk and are dead — deleting a task removes the registration and leaves the prompt behind. So copying the folder gets you the prompts and none of the scheduling. Re-registering is a conversation with Claude on the new machine, and it takes about a minute.

**Browser-local state.** The tracker's click history is in `localStorage` under the key `genai16w-v1`, inside the artifact's webview. It is per-install and syncs nowhere. It does not survive the move.

That last one is the only real loss, and today it costs you almost nothing — you're on Day 1 of Week 1, so there is at most one session's worth of clicks to redo. This is the cheapest week of the entire sixteen to do this in. If you'd rather not lose it in some future move, ask me to add an Export/Import button to the tracker and the state becomes a JSON file you can carry.

## Do this

1. **On the old Mac**, run the bundler. It reads live files rather than anything I transcribed, skips the two dead prompts, and drops a single archive on your Desktop.

   ```
   bash ~/Documents/"Claude Cowork"/"GenAI Study"/migrate-bundle.sh
   ```

   Expect `Bundle: ~/Desktop/genai-program-<date>.tgz` — a small archive, well under a megabyte, since it's all text. It refuses to run if the study folder is missing, and warns rather than fails on anything else.

2. **Push the code repo.** `genai-16week` is a git repo and should move as one — don't put it in the tarball. From the repo root: `git add -A && git commit -m "pre-migration" && git push`. If it has no remote yet, create a private repo and add one now. `LEARNING-LOG.md` is in here, and `05-ACCOUNTABILITY.md` is right that it's the highest-value artifact in the program — it should not exist on exactly one laptop.

3. **Move the archive** (AirDrop, or any means you like) and unpack it on the new Mac.

   ```
   tar -xzf genai-program-<date>.tgz && cd genai-program && ./restore.sh
   ```

   It backs up anything it would overwrite as `*.bak-<timestamp>`, rewrites the study-folder path in all three prompts to the new home, and reports how many references it rewrote in each — the morning brief should report 5. If it warns that a prompt still references the old home, open that file and fix the straggler by hand.

4. **Clone the repo** on the new machine.

5. **Open Claude, grant it the study folder**, then paste the re-registration request that `restore.sh` prints. It asks Claude to register the three tasks from the restored prompts (morning brief 6am weekdays, midday build 1pm weekdays, weekly review 9am Saturdays) and to re-create the tracker from the restored `index.html`.

6. **Reinstall the toolchain** — none of it should be copied. Claude Code, Codex, Kiro, the AgentCore CLI (`npm install -g @aws/agentcore`, then `agentcore --version`), Python 3.12+ with `uv`, **Node 22+** (not 20 — the CLI's TypeScript path needs 22, and Weeks 8 and 15 use it), and the AWS CDK.

7. **Configure AWS credentials.** Nothing else on the AWS side needs redoing: Bedrock model access in `us-east-1` and `us-west-2`, the $50 Budget, and your sandbox IAM all belong to the account, not the laptop. Add the `bedrock:CountTokens` action while you're in there — the 08-25 currency entry explains why.

## Verify before you trust it

Ask Claude to list your scheduled tasks: you want exactly three, all enabled, with next-run times that look right for your timezone. Then ask it to read `06-CURRENCY-DELTA.md` and tell you where you are in the program — if it answers with the correct week and the 08-25 `CountTokens` finding, the paths resolve and the tasks will read real files at 6am. Open the tracker from the sidebar and confirm it renders and accepts a click.

The honest end-to-end test is simply the next morning brief. If it arrives correct and on time, the migration held.

## One thing worth changing while you're at it

Scheduled tasks only fire while the Claude app is open; today's brief queued at 6:03am and ran at 8:12am because of it. If the new laptop also gets quit overnight, either leave the app running or move the morning trigger to a time you're reliably at the machine. Moving the block honestly beats letting it decay — that decay is the failure mode `05-ACCOUNTABILITY.md` warns about.
