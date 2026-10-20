# Grounded Agent Instructions

[English](README.md) | [한국어](README.ko.md)

A compact [AGENTS.md](AGENTS.md) for agents that check assumptions, calibrate their initiative, and communicate in the user's language. Persistent instructions, memories, and skills stay in English; necessary language-specific expressions retain their original form.

Copy or merge one Markdown file into an instruction file your agent loads. There is no runtime, API key, or package dependency.

## What it asks the agent to do

- **Check the problem framing.** Examine evidence, assumptions, and missing considerations that could change a decision.
- **Exercise judgment within permission.** Explain consequential problems with a requested method and propose an alternative aligned with the actual goal.
- **Adjust the action to the evidence.** Continue reversible investigation under uncertainty; reconsider stronger commitments when understanding weakens.
- **Separate storage language from conversation language.** Author persistent guidance in English and respond in the user's conversational language, respecting explicit language requests.
- **Maintain relevant continuity.** Revalidate remembered assumptions and preserve the goal, evidence, unresolved issues, and next checks within permitted storage.

## Use it

1. Open [AGENTS.md](AGENTS.md), or download the repository:

   ```sh
   git clone https://github.com/GwangHoonYoo/grounded-agent-instructions.git
   cd grounded-agent-instructions
   cat AGENTS.md
   ```

2. Merge its contents into the instruction file for the desired scope. Preserve existing project conventions and resolve conflicting rules.

   | Agent | All projects | One project |
   | --- | --- | --- |
   | Codex | `~/.codex/AGENTS.md` | `AGENTS.md` at the project root |
   | Claude Code | `~/.claude/CLAUDE.md` | `CLAUDE.md` at the project root |
   | Other agents | The documented global instruction file | The documented project instruction file |

   Codex uses `$CODEX_HOME` instead of `~/.codex` when configured. A nonempty `AGENTS.override.md` takes precedence at its scope; more specific project instructions can override global ones. Merge into the file actually loaded. For Claude Code, the payload is the **contents of `AGENTS.md`**, placed in the appropriate `CLAUDE.md`. Existing `AGENTS.md` support depends on the client's configuration and version.

3. Start a fresh session and ask:

   > Summarize your active guidance for assumptions, authorization, memory language, and response language.

   Then try the [evaluation scenarios](docs/evaluation.md). A correct summary checks instruction discovery; behavior must be assessed separately.

Installation locations are based on [Codex documentation](https://learn.chatgpt.com/docs/agent-configuration/agents-md) and [Claude Code documentation](https://code.claude.com/docs/en/memory). Other clients require their own loading mechanism.

## Example behavior

Illustrative examples, not recorded model results:

| Situation | Intended behavior |
| --- | --- |
| A plan relies on a reported 40% conversion rate | Check the source, denominator, and meaning of conversion before using it to justify spending. Continue available research. |
| New evidence contradicts an ongoing plan | Preserve the contradiction, revise the assumption, and reduce consequential action while investigating. |
| A user asks in Korean to remember a preference | Reply in Korean; author the memory in English, retaining Korean expressions only when needed to preserve meaning. |
| A user asks in Spanish for an English report | Converse in Spanish and produce the report in English. |
| A small, well-defined, reversible edit | Complete it proportionately without turning the guidance into an unnecessary interview. |

## Size and evidence

Only `AGENTS.md` needs to be in the agent's standing instruction context. The README and design notes are optional reading.

The token count and measurement method are recorded in [design notes](docs/design.md#token-budget). English storage is a design choice; savings depend on wording and tokenizer. This repository has no controlled evidence that the template improves model performance. Instructions guide behavior; enforcement and memory availability depend on the host agent.

## Research basis

The initiative rules are inspired by Kirandeep Kaur, Xingda Lyu, and Chirag Shah, [*Position: Knowing Isn't Understanding: Re-grounding Generative Proactivity with Epistemic and Behavioral Insight*](https://arxiv.org/html/2602.15259v2), arXiv:2602.15259v2, May 31, 2026.

The paper proposes coupling warranted understanding with the strength of intervention. This repository translates selected principles into a practical instruction template. English persistence and multilingual replies are this project's additional design choices. See the [principle mapping](docs/design.md#principle-mapping).

## Contribute

Report a reproducible failure or submit a focused change. Include the client/model, relevant instruction scope, anonymized prompt, observed behavior, expected behavior, and token impact. Keep persistent guidance in English and update both README languages together. Use the [evaluation protocol](docs/evaluation.md) to distinguish examples from measured outcomes.

## License

[MIT](LICENSE). The linked paper retains its own license.
