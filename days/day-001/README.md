# Day 001 — A primer on AI infrastructure

**Date:** November 6, 2026  
**Focus:** Understanding what happens after you send a prompt  
**Blog status:** Draft written; planned for Substack

## What I did

- Wrote a plain-English introduction to the infrastructure that runs a language model.
- Followed a request from the application through inference and back to a streamed response.
- Covered models versus applications, GPUs and VRAM, compute and bandwidth, PyTorch and vLLM, tokens, prefill and decode, KV caching, and routing with llm-d.

## Writing

- [A primer on AI infrastructure — draft](ai-infrastructure-primer.md)
- **Published post:** Not published yet. Add the Substack link here when it goes live.
- **Graphics:** Add diagrams and illustrations to [assets/](assets/).

## Main takeaways

- The model and the application around it are different parts of the system.
- Running a model involves both calculations and moving data through memory.
- Inference has two main stages: processing the input and generating the output.
- Caching can save repeated work, but it also uses memory.
- Routing to a server and choosing a model are different decisions.

## Questions to explore next

- When does inference become limited by compute versus memory bandwidth?
- How much GPU memory do model weights and KV caches need?
- How does vLLM handle multiple requests at once?
- How does llm-d weigh cached work against server load?
- How does choosing a model differ from choosing a server?

## Next steps

- [ ] Review the draft for technical accuracy and add source links.
- [ ] Add a graphic showing the path from prompt to response.
- [ ] Publish the post on Substack.
- [ ] Add the published link here and in the main learning log.

[← Learning log](../../README.md) · [Reading & watching list](../../resources/README.md)
