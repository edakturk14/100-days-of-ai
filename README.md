# 100 Days of AI

I'm learning AI in public for 100 days, starting with inference and the infrastructure behind it. This repo brings together short daily notes, useful resources, and longer explanations as I write them.

Learning along with me? Use the starting path below or pick a topic that interests you.

**Started:** November 6, 2026 · **Progress:** 5 / 100 days logged

## Start here

1. **Get the big picture:** read the opening chapters of [Inference Engineering](https://www.baseten.co/inference-engineering/book) by Philip Kiely. Prefer watching? Try [his conversation with Scott Hanselman](https://www.youtube.com/watch?v=ZrZfVbaxcF4).
2. **Follow a prompt through a model:** read [How caching works](https://huggingface.co/docs/transformers/en/cache_explanation), then sketch what gets reused as each new token is generated.
3. **Try some code:** work through [PyTorch's basics](https://docs.pytorch.org/tutorials/beginner/basics/intro.html). If you're ready to serve a model, try the [vLLM quickstart](https://docs.vllm.ai/en/latest/getting_started/quickstart/) and check its hardware requirements first.

For more technical reading, explore GPU bottlenecks and routing in the [resource list](resources/README.md). Resource statuses track my own progress.

## Learning log

| Day | Date | Topic | What I did | Notes & writing |
| --- | --- | --- | --- | --- |
| 001 | November 6, 2026 | AI infrastructure | Wrote a draft of “A primer on AI infrastructure.” | [Day 1](days/day-001/README.md) · [Original draft](days/day-001/ai-infrastructure-primer.md) |
| 002 | November 7, 2026 | AI inference | Continued learning about AI inference. | [Day 2](days/day-002/README.md) |
| 003 | November 8, 2026 | AI inference | Continued learning about inference and published a blog covering the first three days. | [Day 3](days/day-003/README.md) |
| 004 | November 9, 2026 | Inference Engineering | Read chapter 1 of [Inference Engineering](https://www.baseten.co/inference-engineering/book) by Philip Kiely. | [Day 4](days/day-004/README.md) |
| 005 | November 10, 2026 | Inference Engineering | Read chapter 2 of [Inference Engineering](https://www.baseten.co/inference-engineering/book) by Philip Kiely. | [Day 5](days/day-005/README.md) |

## Topics I want to explore

A few starting points, grouped by topic:

- **AI inference:** [Inference Engineering — Philip Kiely](https://www.baseten.co/inference-engineering/book) · Chapters 1–2 read.
- **GPUs & memory:** [All About Rooflines](https://jax-ml.github.io/scaling-book/roofline/) · A deeper look at compute and bandwidth limits.
- **PyTorch:** [Learn the Basics](https://docs.pytorch.org/tutorials/beginner/basics/intro.html) · A hands-on introduction.
- **vLLM:** [Quickstart](https://docs.vllm.ai/en/latest/getting_started/quickstart/) · Try serving a model.
- **KV caching:** [How caching works](https://huggingface.co/docs/transformers/en/cache_explanation) · Understand what gets reused during generation.
- **Server routing:** [llm-d architecture](https://llm-d.ai/docs/dev/architecture) · How requests reach model servers.
- **Model routing:** [RouteLLM](https://github.com/lm-sys/RouteLLM) · Explore choosing between models.
- **Agents:** [Building effective agents — Anthropic](https://www.anthropic.com/research/building-effective-agents) · Workflows, tools, and agent patterns.
- **Software factories:** [StrongDM's write-up](https://factory.strongdm.ai/) · One team's approach to agent-driven development.

The [reading & watching list](resources/README.md) tracks progress and includes a video interview with Philip Kiely.

## Join in

Use the [day template](templates/day.md) to start your own log. Keep notes in `days/day-NNN/README.md`, add images in that day's `assets/` folder, and update the learning log above.

Found a mistake or a useful resource? [Open an issue](https://github.com/edakturk14/100-days-of-ai/issues) with a correction or a link and one sentence about why it helps.

If this is useful, star the repo to find it again as the collection grows.
