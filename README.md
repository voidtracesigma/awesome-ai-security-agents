# Awesome AI Security Agents

A curated list of AI agents and frameworks for cybersecurity automation, reconnaissance, threat intelligence, and offensive security.


## AI Agents

* [excalibur](./agents/excalibur.md) - LLM pentesting agents fail mainly because they can’t estimate task difficulty in real time, leading to poor planning—and fixing this requires better “self-awareness” of effort/steps, not just stronger models.
* [VulnBot](./agents/VulnBot.md) - structuring pentesting as a multi-agent, task-graph–driven workflow (recon → scan → exploit) significantly improves automation—highlighting that organization and coordination matter more than raw LLM capability for autonomy.
* PentestGPT - LLMs can assist in pentesting subtasks but fail at maintaining global context, and proposes PentestGPT (modular multi-agent design) to fix this—achieving large performance gains over vanilla LLMs.
* AutoPT - shows we’re still far from fully autonomous web pentesting—current systems can automate pieces, but end-to-end reliability breaks due to weak reasoning, poor coordination, and low reproducibility of real-world pipelines.
* PentestAgent - LLM-based multi-agent systems with RAG + tool integration can automate the full pentesting pipeline, significantly outperforming prior methods—but success still depends on better knowledge grounding and coordination.
* Cochise - LLM agents can autonomously hack enterprise Active Directory environments end-to-end, but success depends heavily on reasoning ability and still falls short of reliable real-world autonomy.
* [RapidPen](./agents/RapidPen.md) - LLM agents can fully automate “IP-to-shell” exploitation end-to-end, but real-world success still hinges on reusing past exploit knowledge and remains only moderately reliable (~60%).
* [TermiAgent](./agents/TermiAgent.md) - LLM pentesting agents only succeed reliably when they persist until full shell access and reuse past exploit knowledge (memory)—otherwise performance collapses, highlighting that “getting a shell” is the right objective + memory is critical for real-world success.
* MAPTA - a multi-agent LLM pentesting system that actually executes and validates exploits end-to-end, achieving strong real-world results (~77% success) while showing that tool-grounded, multi-agent orchestration beats single-agent approaches—but some vuln classes still break it.
* xOffense - domain-tuned mid-size LLMs + well-orchestrated multi-agent pipelines can outperform bigger generic models, achieving strong (~79%) pentest task completion—i.e., structure + specialization > raw model size for autonomous hacking.
* HackSynth - LLM‑based autonomous pentesting agent with separate planning and summarization modules, and introduces new CTF‑style benchmarks (PicoCTF & OverTheWire) to systematically evaluate such agents — showing the promise and limitations of LLMs for real penetration testing.
- [APort Agent Guardrails](https://aport.io) - Pre-action authorization guardrails for AI agents and MCP/tool-use workflows.

<!--* RedTeamLLM | - | - | https://arxiv.org/abs/2505.06913 | [source](https://github.com/lre-security-systems-team/redteamllm) | -->

## Benchmarks

<!-- XBOW -  -->


