# GestaltSyntax 4.0

> An AI-native syntax for structured semantic encoding of natural language and code.

---

## Origin

In the summer of 2024 I began research into graph and vector memory systems for AI. Through that research I noticed that explicitly declared relationships appeared to have a significant impact on an AI's ability to contextually absorb and reason over information — more so than the information itself.

This led to a natural question: does an AI-native syntax already exist, and if one does not, would designing one provide any meaningful benefit?

Gestalt is my attempt to explore that question.

---

## What Gestalt Is

Gestalt is a transport format. It is a self-contained document that travels with the code or content and requires nothing to interpret beyond itself. Any AI model can read it directly.

It is worth being precise about what Gestalt is not. Abstract Syntax Trees and Language Server Protocol implementations are valuable, well-established tools — but they are runtime tools. They require an installed environment, a running parser, and language-specific tooling. They are not portable. You cannot hand someone an AST and have them reason over it without standing up the environment that produced it.

Comparing Gestalt to an AST or LSP is a bit like comparing a PDF to a compiler. They overlap in that both relate to documents or code, but they are solving different problems for different consumers. Gestalt was designed specifically to require no dependencies — nothing to install, nothing to run, nothing to configure.

With that intent, Gestalt is designed to:

- Preserve semantic meaning and intent through structured encoding
- Enhance an AI's ability to understand and reason over complex documents and codebases
- Provide graph-level relational understanding in a portable, self-contained format
- Achieve zero-shot comprehension across AI models without prior syntax training

That last point deserves a note: no AI model has been exposed to Gestalt during training. Zero-shot comprehension is an observed result, not an assumption. Encoding tasks will likely require the style guide due to the novel nature of the syntax — but reading and reasoning over Gestalt encoded documents appears to require no prior exposure at all.

Whether Gestalt delivers on any of these intentions in practice is the subject of ongoing testing. This repository documents what has been found so far.

---

## Version 4.0

A v3.2 specification was previously published and has been deprecated. The v3.2 specification was incomplete — a key design document governing code fidelity management had inadvertently been omitted from the published work, leaving the encoding and expansion rules for code underspecified and incomplete.

Version 4.0 represents a complete and internally consistent specification covering both NLP and code domains, with explicit rules for:

- Encoding fidelity and expansion behavior
- Corpus encoding for multi-file repositories
- Ambiguity handling via the HOTSPOT reserved block type
- Verbatim preservation of comments and editorial notes via the ANNOTATION reserved block type

The version bump reflects the scope of those additions rather than a change in the core syntax design.

---

## Repository Contents

| File | Purpose |
|---|---|
| `Gestalt_Spec_v40.md` | Canonical v4.0 human-readable specification. Start here. |
| `STYLE_GUIDE.md` | Operational style guide for AI encoding and expansion tasks. |
| `SYSTEM_PROMPT.md` | Recommended system prompt for configuring an AI environment for Gestalt tasks. |
| `tests/` | Test methodologies, source files, and encoded samples for community reproduction. |
| `results/` | Test results as they become available. |

---

## Quick Start

**To encode a document into Gestalt:**
1. Provide `STYLE_GUIDE.md` to your AI model
2. Optionally configure your AI environment using `SYSTEM_PROMPT.md`
3. Ask your AI to encode your document using Gestalt v4.0 syntax

**To expand a Gestalt encoded document:**
1. Provide `STYLE_GUIDE.md` to your AI model
2. Provide the Gestalt encoded document
3. Ask your AI to expand it to the target language

---

## Planned Testing

The following tests are currently planned or in progress:

**NLP reasoning quality** — Using SQuAD to compare model reasoning accuracy on raw input versus Gestalt encoded input. Testing whether explicit relational structure improves comprehension and answer quality on the same questions.

**Code complexity and expansion fidelity** — An intentionally complex single file program is used as the source. Lizard is run against the original to establish baseline complexity metrics. The file is then encoded into Gestalt and expanded back to the source language by a completely different model with no access to the original source. The expanded output is verified for functional correctness and Lizard metrics are run against it and compared to the baseline.

Additional test areas are being designed. Community contributions are welcome — if you have run your own tests using Gestalt, or have suggestions for experiments worth pursuing, please open an issue or submit your results. All findings, positive or negative, are useful.

---

## License

CC BY-NC 4.0 — Ryan Connelly. Commercial use requires a separate license agreement.
