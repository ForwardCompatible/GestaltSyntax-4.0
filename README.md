# GestaltSyntax 4.0

> An AI-native syntax for structured semantic encoding of natural language and code.

---

## What Gestalt Is

**Abstract Syntax Trees and Language Server Protocol implementations keep the structure and sacrifice the meaning. Gestalt keeps the meaning and sacrifices some of the explicit structure.**

Gestalt is a self-contained, portable encoding format designed specifically for AI consumption. It encodes the semantic intent of natural language and code along with the explicit relationships between ideas, functions, and concepts — producing a document that any AI model can ingest and reason over directly, without dependencies, without a running environment, and without prior exposure to the syntax.

For a complete explanation of what Gestalt is, how it differs from existing tools, and the research questions it was designed to explore, see [`NLP_knowledgebase.md`](NLP_knowledgebase.md). To ask an AI model questions about Gestalt directly, provide [`GST_knowledgebase.md`](GST_knowledgebase.md) — no configuration required.

---

## How It Works

Gestalt uses three Unicode delimiters to structure content into typed, identified, metadata-tagged blocks with explicitly declared relationships between them:

```
FUNC☩calculate_tax☩params:amount:float,return:float☸
multiplies amount by TAX_RATE, rounds to 2 decimal places☥
RELATES☩TAX_RATE☩depends_on
RELATES☩validate_input☩calls
```

Every block carries its semantic content, its classification, its metadata context, and its declared relationships to other blocks. Nothing is left to inference.

The complete encoding and expansion reference is in [`STYLE_GUIDE.md`](STYLE_GUIDE.md).

---

## Why It Exists Relative to Other Tools

Gestalt is not a replacement for AST, LSP, RAG, or vector stores. Those are well-established tools solving different problems for different consumers. Gestalt occupies a position none of them fill: a portable, self-contained semantic document designed specifically for an AI model as the primary consumer.

- **AST and LSP** are runtime tools. They require an installed environment and serve compilers and language servers. They are structurally precise and semantically empty.
- **RAG and vector stores** retrieve context at inference time and hand the model raw material to reason over. Relevance is established on the fly.
- **Gestalt** encodes semantic meaning and explicit relationships at encoding time. The model consuming it does not have to establish relevance or interpret structure — that work is already done.

---

## Token Efficiency

Token efficiency is an observed property of Gestalt encoding, not its primary purpose.

Every Gestalt document carries a fixed framework overhead of approximately 170 tokens. Below that threshold, a Gestalt encoded document may be larger than its source. Above it, efficiency scales nonlinearly with document length and the structural and repetitive density of the source content.

The knowledge base documents in this repository provide a verifiable comparison. [`NLP_knowledgebase.md`](NLP_knowledgebase.md) is 612 lines. [`GST_knowledgebase.md`](GST_knowledgebase.md) is 494 lines. Both contain identical content across eight sections. The difference is attributable entirely to the encoding.

The more meaningful distinction is what might be called **context density** — a working term developed during the research behind Gestalt, for which no existing industry standard was found. It may be superseded by a more precise term as the field develops. Context density refers to the degree to which a unit of encoded information carries not only its semantic content but also the explicit relational and interpretive context necessary to use that information without additional reasoning overhead. A RELATES declaration doesn't just connect two blocks — it answers the question of why that connection exists and makes that answer available to the model at the moment the information arrives.

---

## Zero-Shot Comprehension

No AI model has been exposed to Gestalt during training. Zero-shot comprehension — the ability to read and reason over a Gestalt encoded document without prior exposure or a syntax guide — is an observed result across all tested models above approximately one billion parameters.

Encoding tasks will likely require the style guide. Reading and reasoning over Gestalt encoded documents appears to require no prior exposure at all. Whether this property holds universally and what its boundaries are is an active area of investigation.

---

## Testing and Findings

All testing is conducted against the v4.0 specification. Results from prior versions are not cited — the v3.2 specification was incomplete in ways that make those results unreliable as a baseline.

Current testing in progress:

- **QuALITY benchmark** — comparing model response quality on raw NLP input versus the same content encoded in Gestalt, identical questions against both
- **Code complexity and expansion fidelity** — Lizard baseline metrics on a source file, Gestalt encoding, cold session expansion by a different model, functional verification and metric comparison
- **Cross-language expansion** — encoding a Python program into Gestalt and expanding it into other languages in cold sessions
- **Knowledge base token efficiency demonstration** — the paired NLP and GST knowledge base documents in this repository

Active hypotheses under investigation include hallucination reduction, attention persistence across the forward pass, explicit relationships surfacing knowledge gaps, and the broader impact of Gestalt encoding on model reasoning quality. These are research questions, not findings. Full detail is in [`NLP_knowledgebase.md`](NLP_knowledgebase.md).

Findings — positive, negative, or inconclusive — will be documented in `results/` as they become available. Community contributions and independent reproductions are welcome.

---

## Getting Started

**To ask questions about Gestalt:**
1. Provide [`GST_knowledgebase.md`](GST_knowledgebase.md) to your preferred AI model
2. Ask questions directly — no configuration or syntax guide required

**To encode a document into Gestalt:**
1. Provide [`STYLE_GUIDE.md`](STYLE_GUIDE.md) to your AI model
2. Optionally configure your environment using [`SYSTEM_PROMPT.md`](SYSTEM_PROMPT.md)
3. Ask your AI to encode your document using Gestalt v4.0 syntax

**To expand a Gestalt encoded document:**
1. Provide the Gestalt encoded document to your AI model
2. Ask your AI to expand it to the target language

*Providing the style guide alongside the document is not required but may reduce initial perplexity, particularly on smaller models. The impact of style guide presence on expansion quality is an area of ongoing research.*

---

## Repository Contents

| File | Purpose |
|---|---|
| `NLP_KNOWLEDGE_BASE_v40.md` | Complete human-readable knowledge base. Start here for full context. |
| `GST_KNOWLEDGE_BASE_v40.md` | Gestalt encoded knowledge base. AI-deployable. Drop into any model and ask questions. |
| `specification/Gestalt_Spec_v40.md` | Canonical v4.0 specification. Human-readable reference. |
| `specification/STYLE_GUIDE.md` | Operational encoding and expansion reference for AI models. |
| `specification/SYSTEM_PROMPT.md` | Recommended system prompt for configuring an AI environment for Gestalt tasks. |
| `tests/` | Test methodologies, source files, and encoded samples for community reproduction. |
| `results/` | Test results as they become available. |

---

CC BY-NC 4.0 — Ryan Connelly. Commercial use requires a separate license agreement.
