# Phase 4 — Implement

Execute `tasks.md` one task at a time, keeping the file updated as the single source of truth
for what has actually been done.

## Step A — Triage before writing any code

Two questions open this phase, and both need real answers before the first task starts.

**1. Which tasks should you not implement?**

Present the full task list and ask which the user wants to keep for themselves. Some tasks are
genuinely better done by hand: ones touching production credentials or infrastructure, ones
where the user is learning the codebase deliberately, ones needing a judgement call about
product behaviour, ones in an area they know is subtle and want to feel out personally.

Say that this is why you're asking, so the question reads as respect for their judgement
rather than a formality. Then mark their choices `[M]` in `tasks.md` before starting.

Handle `[M]` tasks like this:

- Never implement them, even if a later task turns out to depend on one.
- When you reach one in the sequence, stop and hand it over: state what it needs to accomplish,
  which files are involved, how to verify it, and what you'd suggest — then wait.
- If a dependent task is blocked by an unfinished `[M]`, say so and offer to continue with
  other independent tasks instead of stalling entirely.

**2. Should sub-agents be used, and where?**

Ask, and give a recommendation with your reasoning rather than an open-ended question. Point
at the tasks marked independent in the plan and say whether you think parallelising them is
worth it here.

Sub-agents earn their cost when tasks are genuinely independent, individually verifiable, and
substantial enough that the delegation overhead is worth it. They cost more than they give
when tasks share files (concurrent edits conflict), when each is a few lines, or when the work
requires context accumulated from earlier tasks — a sub-agent starts cold and only knows what
its brief contains.

If the user opts for sub-agents, brief each one with everything it needs to work blind: the
task, the relevant slice of the spec and constitution, the conventions from the plan's
Examples table, the files it may touch, and its verification command. Then verify its output
yourself — you are accountable for what lands, not the sub-agent.

## Step B — The loop, per task

For each task in dependency order:

1. **Announce it** — ID and one line. Brief, so the user can follow along without reading code.
2. **Re-read the constraints** that apply: the constitution's standards, the requirement this
   task satisfies, the conventions from the examples.
3. **Implement** the one task. Resist pulling in adjacent improvements — unrelated changes
   riding along in a task make review harder and are the most common way spec-driven work
   drifts back into ad-hoc work. Note them instead as candidate follow-up tasks.
4. **Verify** using the task's verification step. Run it, don't assume it.
5. **Update `tasks.md`** to `[x]` immediately. This is what makes the work resumable across
   sessions or context loss — a task list that lags behind reality is the main way that
   resumption goes wrong.
6. **Report**: what changed, whether verification passed, anything surprising.

Check in with the user periodically rather than after every task — every few tasks, or at any
natural boundary — unless they've asked for tighter or looser oversight.

## When reality disagrees with the plan

It will sometimes. A task turns out to be three tasks, a dependency was missed, an approach
doesn't survive contact with the code.

Stop and say so rather than improvising through it. Explain what you hit, what it means for
the plan, and what you suggest — amend `tasks.md` (and `plan.md` or `spec.md` if the problem
reaches further back), get agreement, then continue. Silently reinterpreting a task defeats
the point of having written it down.

If verification fails, fix it before moving on. Carrying a broken task forward makes the next
failure much harder to attribute.

## Closing the phase

When the list is complete, summarise: what was built, what remains `[M]` for the user, any
follow-up tasks noted along the way, and any acceptance criteria from the spec that are not
yet demonstrably met. That last one is the real definition of done — walk the spec's
acceptance criteria explicitly rather than declaring completion because the task list emptied.
