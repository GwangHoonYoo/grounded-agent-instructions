# Design notes

## Principle mapping

The template adapts selected ideas from [Kaur, Lyu, and Shah (2026), arXiv v2](https://arxiv.org/html/2602.15259v2). It is an independent practical interpretation.

| Basis | Instruction behavior |
| --- | --- |
| Epistemic incompleteness, sections 1 and 3 | Examine missing dimensions and the adequacy of the problem framing, beyond confidence over existing variables. |
| Behavioral grounding, section 4 | Respect authorization, consequences, and reversibility. |
| Epistemic-behavioral coupling, section 5 | Match intervention strength to warranted understanding; preserve uncertainty and contradictory evidence. |
| Minimal requirements, section 5.1 | Continue reversible inquiry and reduce commitment when understanding weakens. |
| Commitment and evaluation, section 6 | Consider whether action was justified using information available at the time, rather than outcome alone. |
| Epistemic partnership, section 7 and appendix B | Ask consequential questions, consider cumulative commitments, and reassess during interaction. |
| This project's language policy | Author persistent guidance in English while matching user-facing language and preserving necessary original-language expressions. |
| This project's continuity policy | Retrieve relevant state, preserve provenance and scope, and revalidate assumptions. |

Critical judgment concerns methods and assumptions. The user's goal, explicit constraints, and permissions remain controlling. Routine execution should remain proportionate to the task. Recognizing a possible gap justifies investigation; it does not establish that the gap is real or authorize stronger action.

## Token budget

The standing payload is exactly the UTF-8 contents of `AGENTS.md`. Documentation and this mapping need not be loaded every session.

The current payload token count is recorded below after measurement with `tiktoken` and the `o200k_base` encoding. This is a reproducible reference count, not a claim about every model's billing tokenizer or a guaranteed saving from English.

<!-- token-metrics:start -->
- `AGENTS.md`: **383 tokens** (`o200k_base`), **2,252 UTF-8 bytes**.
- Payload SHA-256: `d88a391f74450e734de713888508ff0146c2bdc207da66d1278f84f1f1176040`.
<!-- token-metrics:end -->

Reproduce the count with Python and `tiktoken` installed:

```sh
python3 -c 'from pathlib import Path; import tiktoken; print(len(tiktoken.get_encoding("o200k_base").encode(Path("AGENTS.md").read_text(encoding="utf-8"))))'
```

The count excludes client wrappers, other instructions, tool descriptions, retrieved memory, and generated reasoning. Language choice and instruction length should be evaluated alongside behavior and user effort.

## Scope of evidence

This repository provides an instruction artifact and a manual evaluation protocol. It does not implement an epistemic-state estimator, a memory service, a permission system, or enforcement hooks. The paper is a position paper; its framework and this template require empirical evaluation for any claim of performance gains. Neither a successful install nor an agent's summary establishes improved critical judgment.

## Maintenance

Keep `AGENTS.md` self-contained and portable. Put optional explanations in documentation. Preserve language-policy exceptions for exact text and local nuance. Update the measured count whenever the payload changes, keep both READMEs aligned, and include reproducible evidence for behavioral claims.
