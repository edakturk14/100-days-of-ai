# 100 Days of AI

I'm spending 100 days learning more about AI and documenting what I learn along the way.

I'm starting with the infrastructure behind it all: what happens after you send a prompt, how models run, and how systems serve them. From there, I want to explore topics like inference, model routing, and software factories.

This is a place for my notes, questions, experiments, graphics, and writing. Some days might turn into a blog post; others might just be a few notes from a video or something I tried building. The point is to keep learning and make the concepts easier to understand.

**Started:** November 6, 2026 · **Progress:** 4 / 100 days logged

## Learning log

| Day | Date | Topic | What I did | Notes & writing |
| --- | --- | --- | --- | --- |
| 001 | November 6, 2026 | AI infrastructure | Wrote a draft of “A primer on AI infrastructure.” | [Day 1](days/day-001/README.md) · [Original draft](days/day-001/ai-infrastructure-primer.md) |
| 002 | November 7, 2026 | AI inference | Continued learning about AI inference. | [Day 2](days/day-002/README.md) |
| 003 | November 8, 2026 | AI inference | Continued learning about inference and published a blog covering the first three days. | [Day 3](days/day-003/README.md) |
| 004 | November 9, 2026 | Inference Engineering | Read chapter 1 of *Inference Engineering* by Philip Kiely. | [Day 4](days/day-004/README.md) |

## Topics I want to explore

An evolving list, rather than a fixed curriculum:

- [ ] AI inference: what happens when a model runs
- [ ] GPUs, memory, and the tradeoffs behind serving models
- [ ] PyTorch and vLLM
- [ ] Prefill, decode, and KV caching
- [ ] Routing requests across servers with llm-d
- [ ] Model routing: choosing which model to use
- [ ] Agents, harnesses, and software factories
- [ ] Small hands-on experiments to connect the concepts

Videos, blog posts, papers, and documentation I want to spend time with go in the [resource list](resources/README.md).

## How this repo is organized

```text
days/
  day-001/
    README.md                    # Date, activities, takeaways, and questions
    ai-infrastructure-primer.md   # Blog draft
    assets/                      # Graphics and other supporting files
resources/
  README.md                      # Reading and watching list
templates/
  day.md                         # Starting point for each new day
```

## Adding a day

1. Create a folder such as `days/day-002/` and copy [the day template](templates/day.md) into it as `README.md`.
2. Add the date, what I did, what I learned, and any questions or links.
3. Keep drafts and experiments in that day's folder, with graphics in an `assets/` subfolder when needed.
4. Add a row to the learning log and update the progress count above.
5. When a post goes live, add its public link to the day's notes and the learning log.

These are learning notes, so I'll revisit and correct them as my understanding grows.
