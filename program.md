# manifest

This is an experiment to have the LLM do its own research.

**Simplicity criterion**: All else being equal, simpler is better. A small improvement that adds ugly complexity is not worth it. Conversely, removing something and getting equal or better results is a great outcome — that's a simplification win. When evaluating whether to keep a change, weigh the complexity cost against the improvement magnitude. A 0.001 val_bpb improvement that adds 20 lines of hacky code? Probably not worth it. A 0.001 val_bpb improvement from deleting code? Definitely keep. An improvement of ~0 but much simpler code? Keep.

## Logging results

When an experiment is done, log it to `results.tsv` (tab-separated, NOT comma-separated — commas break in descriptions).

The TSV should have a header row and 5 columns:

```
wandb_name  val_bpb	artifact_size	status	description   
```

1. wandb run name
2. val_bpb achieved (e.g. 1.234567) — use 0.000000 for crashes
3. artifact size, in MB
4. status: `keep`, `discard`, or `crash`
5. short text description of what this experiment tried

## Research & Planning

1. You should regularly check PRs for high performance and methodologies that are promising for us. If you find promising leads, add them to the RESEARCH_PLAN.md to experiment with.
2. As experiments run, you should do research with Nia. Pay special attention to groundbreaking new papers, as well as posts on X - high-level AI researchers often post on there.
3. **IMPORTANT:** Make sure you update the RESEARCH_PLAN.md document if you have any new experiments you've decided to run. Also update the file afterward.

## The experiment loop

LOOP FOREVER:

The idea is that you are a completely autonomous researcher trying things out. If they work, keep. If they don't, discard. And you're advancing on an idea so that you can iterate. If you feel like you're getting stuck in some way, you can rewind but you should probably do this very very sparingly (if ever).

**Crashes**: If a run crashes (OOM, or a bug, or etc.), use your judgment: If it's something dumb and easy to fix (e.g. a typo, a missing import), fix it and re-run. If the idea itself is fundamentally broken, just skip it, log "crash" as the status in the tsv, and move on.

**NEVER STOP**: Once the experiment loop has begun (after the initial setup), do NOT pause to ask the human if you should continue. Do NOT ask "should I keep going?" or "is this a good stopping point?". The human might be asleep, or gone from a computer and expects you to continue working *indefinitely* until you are manually stopped. You are autonomous. If you run out of ideas, think harder — read papers referenced in the code, re-read the in-scope files for new angles, try combining previous near-misses, try more radical architectural changes. The loop runs until the human interrupts you, period.

As an example use case, a user might leave you running while they sleep. If each experiment takes you ~5 minutes then you can run approx 12/hour, for a total of about 100 over the duration of the average human sleep. The user then wakes up to experimental results, all completed by you while they slept!
