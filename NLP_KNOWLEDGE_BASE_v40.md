# Gestalt Syntax — Knowledge Base
**Version 4.0**

---

## 1. What Gestalt Is

Gestalt is an AI-native syntax for structured semantic encoding of natural language and code.

The simplest way to understand what makes Gestalt different from every other encoding or representation format is this:

> **Abstract Syntax Trees and Language Server Protocol implementations keep the structure and sacrifice the meaning. Gestalt keeps the meaning and sacrifices some of the explicit structure.**

This is not a criticism of AST or LSP — those are precise, well-established tools that solve real problems. But they solve a different problem for a different consumer. An AST is a machine-readable graph of syntactic structure. It tells you exactly how a program is built. It does not tell you what it means, why it was built that way, or how its parts relate to each other semantically.

Gestalt was designed to answer those questions in a format that requires nothing to read — no installed environment, no running parser, no language-specific tooling. A Gestalt encoded document is **self-contained and portable**. Any AI model can ingest it directly and reason over its semantic content and declared relationships in a single pass.

---

### What Gestalt Encodes

Gestalt encodes two things that existing tools do not preserve together:

- **Semantic meaning** — the intent and significance of the content, not just its structure
- **Explicit relationships** — the connections between ideas, functions, and concepts, declared directly rather than left for a model to infer

Every connection in a Gestalt document is declared. Nothing is implicit. This is a deliberate design choice, and it is the property that appears to have the most significant impact on how AI models reason over Gestalt encoded content.

---

### Code Fidelity

For code content, Gestalt preserves the interface and sacrifices the internals. Function names, parameter types, return types, async flags, and complexity notation are all retained explicitly in the encoding. What gets compressed is the implementation body — not the contract.

This means a model expanding a Gestalt encoded function knows exactly what the function is called, what it accepts, what it returns, and what it is supposed to do. It reconstructs the body from that context. The result is **behavioral equivalence and interface surface preservation** — the expanded code will behave identically and expose the same contract, even if the internal implementation differs in variable names or loop structure.

This is intentional. Gestalt encodes architectural intent. Implementation details are reconstructed, not stored.

Because the encoding contains no language-specific syntax, there is no inherent constraint on the target language during expansion. A Gestalt encoded document is theoretically expandable into any language a model knows how to work with — the architectural intent and interface surfaces are preserved, and the model reconstructs the implementation in the target language from that foundation. Early testing of this capability has been encouraging. Rigorous cross-language expansion testing is ongoing.

---

### Two Kinds of Lossy

The word "lossy" is currently used as if it describes a single condition. It does not — and that imprecision makes it harder to understand what any encoding format is actually trading away.

There are two distinct failure modes worth separating:

- **Structurally lossy** — the encoding does not preserve syntactic structure, formatting, implementation internals, or language-specific patterns. What is lost can be reconstructed from the meaning that remains.
- **Semantically lossy** — the encoding loses meaning, intent, or relational context. What is lost cannot be recovered, because the information needed to reconstruct it is gone.

These are not equivalent tradeoffs. A structurally lossy format can still support faithful reconstruction. A semantically lossy format cannot — it has discarded the thing that makes reconstruction meaningful.

AST and LSP implementations are semantically lossy by design. They preserve syntactic structure with precision and discard semantic meaning entirely — that is not their purpose and they make no claim otherwise. Gestalt is structurally lossy by design. It discards syntactic internals and preserves semantic meaning and explicit relationships — that is its entire purpose.

This distinction matters beyond Gestalt. As AI context packages and AI-enabled workflows become more common, the field will need vocabulary that separates these two failure modes clearly. A context package that is structurally lossy is often acceptable. A context package that is semantically lossy is broken in ways that may not be immediately visible.

---

### What Gestalt Is Not

Gestalt is not a replacement for AST, LSP, or compiler intermediate representations. Those tools live in a running environment and serve compilers, linters, and language servers. Gestalt lives in a file and serves AI models.

Gestalt is not a lossless format. It is **intentionally probabilistic** — designed to constrain the space of valid interpretations toward faithful reconstruction of the original intent, without requiring identical output. Two models expanding the same Gestalt encoding will produce implementations that differ in variable names and syntactic choices while preserving behavioral equivalence and interface surfaces. This is a design property, not a failure.

Gestalt is not a compression tool in the traditional sense. Token efficiency is an observed property of the format, not its primary purpose. The primary purpose is **semantic fidelity in a portable, dependency-free form**.

---

### Zero-Shot Comprehension

No AI model has been exposed to Gestalt during training. Zero-shot comprehension — the ability to read and reason over a Gestalt encoded document without prior exposure or a syntax guide — is an observed result across all tested models above approximately one billion parameters.

Encoding tasks will likely require the style guide due to the novel nature of the syntax. Reading and reasoning over Gestalt encoded documents appears to require no prior exposure at all.

Whether this property holds universally and what its boundaries are is an active area of investigation.

---

## 2. Why It Exists

### Background

Gestalt was created by Ryan Connelly, an independent researcher with a background in data analysis and project management. Ryan has autism, synesthesia, and eidetic memory — not binary photographic recall, but recall on a scale where some things are remembered with complete precision and others are not. The combination of these three conditions produces a cognitive experience that is difficult to describe and has historically been difficult to communicate to others.

Gestalt began as an attempt to do exactly that.

---

### Cognitive Model

Synesthesia produces involuntary cross-sensory associations. Eidetic memory produces overwhelming volumes of recalled information surfacing in response to contextual triggers. Autism produces a strong drive toward explicit, structured pattern recognition over implicit social inference.

The combination creates a specific cognitive challenge: when recall is triggered, an enormous amount of information surfaces simultaneously. Navigating it efficiently requires that the relationships between recalled items already be encoded — so that filtering to what is contextually relevant in the current moment is fast and low-cost. Nothing gets figured out on the fly. The connections are already declared.

This is not a metaphor. This is a functional description of how contextually relevant information surfaces in that cognitive model. The explicit relationship declarations in Gestalt are not a syntactic design choice. They are a direct externalization of that process.

---

### Origin

The initial goal was not to build an encoding format. It was to use AI as an interpreter — to externalize an internal cognitive process that had never been successfully communicated to others and see whether a structured representation of it could make it legible.

The process of designing that representation turned out to be as much an experience of self-discovery as it was an exercise in understanding memory structures in general. Formalizing the cognitive model required understanding it precisely enough to write it down. That precision is what became Gestalt.

---

### Application to AI Context

Most AI context packaging systems — RAG being the most common — work by retrieving chunks of raw information and handing them to a model. The model then has to reason over how those chunks apply to the current request. Relevance is figured out on the fly, at inference time, consuming reasoning capacity that could otherwise be spent on the actual problem.

This is precisely what Ryan's cognitive model does not do. The relationships between recalled items are already explicit. Filtering is fast because the connections that determine relevance are already declared. The cognitive load is front-loaded into the encoding, not deferred to the moment of use.

A further consequence of requiring explicit relationships is that their absence becomes immediately visible. When something surfaces without a declared relationship to the current context, that gap does not pass through unexamined — it either triggers the creation of a relationship or it surfaces a knowledge gap that requires resolution. The implicit never passes through silently. Anything without an explicit relationship becomes conspicuous by that absence alone.

AI models appear to exhibit an analogous behavior under Gestalt encoded input. When relationships are explicitly declared, undeclared connections become visible rather than invisible. The model either resolves them or flags them — it cannot silently paper over gaps the way it might with raw unstructured context, where implicit connections are the norm and missing relationships are easy to miss entirely.

Gestalt applies this same principle to AI context. By declaring relationships explicitly at encoding time, a model consuming a Gestalt document does not have to reason over relevance — it is already declared. The model is free to reason over meaning instead.

---

## 3. How It Differs From Existing Tools

Gestalt occupies a position that no existing tool currently fills. Understanding that position requires understanding what the surrounding tools actually do and who they are designed to serve.

---

### RAG and Retrieval Systems

Retrieval Augmented Generation works by retrieving chunks of raw content from a knowledge store and injecting them into a model's context at inference time. The model then has to reason over how those chunks relate to the current request — relevance is determined on the fly, at the moment of use, by the model itself.

The semantic relationships between retrieved chunks are implicit at best and absent at worst. Nothing in the retrieval process declares how one chunk connects to another, or why a given chunk is relevant to the current request beyond vector similarity. The model carries the full burden of establishing context from raw material.

Gestalt does not retrieve. It encodes. The relationships between concepts are declared at encoding time and travel with the document. A model consuming a Gestalt document does not have to establish context — it is already declared.

---

### Vector Stores

Vector stores require an AI model to encode content into embeddings and a compatible embedding agent to retrieve and navigate that structure at query time. The relational structure lives in the embedding space — it is latent, not explicit, and it is opaque without access to a compatible agent. The encoding agent and the retrieval agent are coupled by design.

Gestalt also requires an AI model to encode. That overhead is real and is not claimed otherwise. The difference is what happens after encoding. The relational structure in a Gestalt document lives in explicit declarations within the document itself — not in a latent embedding space. Any AI model can read those declarations directly at retrieval time. The encoding agent is not required. The relational structure is not opaque. The coupling between encoding and retrieval is eliminated.

---

### Traditional Compression

Gestalt deliberately avoids the framing of compression, and that choice is worth explaining directly.

Traditional compression — whether lossless formats like ZIP or lossy formats like JPEG — implies a recoverable original. Lossless compression recovers the artifact exactly. Lossy compression recovers an approximation that degrades gracefully. In both cases, the goal is fidelity to the original artifact.

Gestalt makes no such claim. It is not attempting to recover the original artifact — it is attempting to preserve the semantic intent of the original and support faithful reconstruction from that intent. Two expansions of the same Gestalt encoding will produce functionally equivalent output that may differ in implementation details. That is not compression behavior. It is a different class of encoding entirely, and compressing it into the compression framing misrepresents what it does and sets the wrong expectations for what success looks like.

---

### Runtime Tools

Abstract Syntax Trees, Language Server Protocol implementations, and compiler intermediate representations are runtime tools. They require an installed environment, a running parser, and language-specific tooling to produce and to read. They are not portable in any meaningful sense — you cannot hand someone an AST and have them reason over it without standing up the environment that produced it.

Gestalt requires nothing beyond the document itself. No environment to install. No parser to run. No language-specific tooling to configure. The portability gap between Gestalt and runtime tools is not a matter of degree — it is absolute. A Gestalt document is readable by any AI model in any context without precondition.

---

### The Consumer Distinction

Every tool listed above was designed for a specific consumer. ASTs serve compilers and static analyzers. LSP implementations serve language servers and IDEs. Vector stores serve retrieval pipelines. RAG systems serve inference engines assembling context at query time.

None of them were designed to serve an AI model as the primary consumer of a self-contained semantic document.

Gestalt appears to fill this role — not because it was designed around a consumer profile, but because it was designed around a cognitive model that happens to map closely onto how AI models consume and reason over context. The design came first. The fit was discovered.

---

## 4. Token Efficiency

Token efficiency is an observed property of Gestalt encoding, not its primary purpose. It emerges from the structural design of the format and behaves in a specific, predictable way that is worth understanding before drawing conclusions from any single test result.

---

### Framework Overhead

Every Gestalt document carries a fixed structural cost regardless of its content. The delimiter system, META declaration, reserved block types, and RELATES declarations that form the skeleton of any Gestalt document consume approximately 170 tokens before a single unit of semantic content is encoded.

This overhead is not a defect — it is the cost of the explicit relational structure that makes Gestalt useful. But it means that token efficiency cannot be evaluated against short documents. The framework must be paid for before any efficiency is realized.

---

### The Efficiency Threshold

Token efficiency in Gestalt is not linear and it is not guaranteed at any document length. It is threshold-dependent.

Below the threshold — when the source document is short enough that the framework overhead dominates — Gestalt encoded output will be larger than the source. This is expected behavior, not a failure of the format. Gestalt was not designed for short content.

Above the threshold, the fixed overhead is amortized across a growing volume of semantic content. As document length increases, the per-token cost of the framework becomes proportionally smaller and the efficiency of semantic encoding becomes proportionally larger. The crossover point is not a fixed line — it depends on the structural and repetitive density of the source content.

---

### Nonlinear Scaling

Beyond the efficiency threshold, token efficiency scales nonlinearly. Two factors drive this:

- **Document length** — longer documents amortize framework overhead further and provide more surface area for semantic encoding to reduce token count
- **Source structure and repetition** — highly structured content with repeated patterns, boilerplate, and redundant restatements compresses more aggressively than content that is already semantically dense. Technical documentation, legacy codebases, and procedural content are strong candidates. Literary and creative content, already word-choice optimized, offers minimal token efficiency benefit.

The relationship between these two factors means that efficiency projections from one document type do not transfer reliably to another. Testing on representative content is the only reliable measure.

---

### Previous Data

Prior to v4.0, token efficiency observations were collected under the v3.2 specification. That specification was incomplete — encoding and expansion rules for code content were underspecified, leaving those results on an unreliable foundation.

Those data points are not cited here. They are noted only to explain their absence. v4.0 represents a complete and internally consistent specification, and all efficiency claims going forward will be grounded in testing conducted against it.

---

## 5. Theories Under Investigation

The following are active hypotheses about Gestalt's impact on AI model behavior. Each has been observed consistently enough to warrant formal investigation. None have been validated against controlled methodology. They are presented here as research questions, not findings.

---

### Hallucination Reduction

In sessions where a Gestalt encoded document is provided as the primary context, a specific failure mode has been consistently absent: the pattern where a model hallucinates answers that were present in the source text, producing responses that drift from or contradict the provided material and derail the session.

This observation is consistent across sessions but has not yet been tested against a controlled methodology. The QuALITY benchmark is being used to examine this directly — comparing model response quality on raw NLP input against the same content encoded in Gestalt, using identical questions against both. Whether the reduction in this failure mode is attributable to the explicit relational structure, the token efficiency of the format, or some combination of factors is what that testing is designed to reveal.

---

### Attention Persistence Across the Forward Pass

Gestalt uses three Unicode delimiter characters, each with a tokenizer fertility rate of approximately 2.0. This means each delimiter token is represented consistently enough across training corpora that stable attention patterns are likely associated with it.

The hypothesis is that the explicit relationship declarations in Gestalt create attention that persists through transformer layers that would normally attenuate — specifically the early layers that are typically prunable without measurable impact on model output. If this is occurring, the explicit structure of Gestalt is not merely helping a model find meaning — it may be changing how attention distributes across the full forward pass.

This hypothesis requires interpretability tooling to investigate and has not yet been tested. It is noted here because it provides a potential mechanistic explanation for other observed behaviors and points toward a specific and falsifiable research direction.

---

### Explicit Relationships Surface Knowledge Gaps

In the cognitive model that produced Gestalt, explicit relationships between recalled items serve a validation function. When something surfaces without a declared relationship to the current context, the absence is immediately visible — it either triggers the creation of a relationship or it surfaces a knowledge gap that requires resolution. Nothing passes through silently. The implicit never goes unexamined.

The hypothesis is that AI models exhibit an analogous behavior under Gestalt encoded input. When relationships are explicitly declared, undeclared connections become conspicuous rather than invisible. The model either resolves them or flags them — it cannot silently paper over gaps the way it might with raw unstructured context, where implicit connections are the norm and missing relationships are easy to miss entirely.

This behavior has been observed consistently in sessions using Gestalt encoded documents. Controlled testing to confirm it as a reliable property of the format rather than a session-level artifact is ongoing.

---

### Impact on Model Reasoning

Gestalt encoding is hypothesized to impact model reasoning quality. The nature and degree of that impact is the subject of active testing.

---

## 6. Current Testing

All testing documented here is conducted against the v4.0 specification exclusively. Results from prior versions are not cited. Findings — positive, negative, or inconclusive — will be documented in the repository as they become available. Community contributions and independent reproductions are welcome.

---

### QuALITY Benchmark

The QuALITY benchmark is being used to compare model response quality on raw NLP input against the same content encoded in Gestalt. The same corpus is used for both runs. The same questions are asked against both. The only variable between runs is the format of the input.

This test is designed to examine the hallucination reduction hypothesis directly — specifically whether the explicit relational structure of Gestalt reduces the failure mode where a model produces responses that drift from or contradict the provided source material. It also provides an initial data point on the broader hypothesis that Gestalt impacts model reasoning quality.

---

### Code Complexity and Expansion Fidelity

An intentionally complex single-file program is used as the source. Lizard is run against the original to establish baseline complexity metrics. The file is then encoded into Gestalt. A completely different model — with no access to the original source — is used to expand the Gestalt encoded document back to the source language in a cold session.

The expanded output is verified for functional correctness. Lizard metrics are run against it and compared to the baseline. This test is designed to examine whether behavioral equivalence and interface surface preservation hold in practice, and whether the expansion fidelity rules of the v4.0 specification produce reliable results across models.

---

### Cross-Language Expansion

A self-contained single-file Python program is encoded into Gestalt. The Gestalt encoded document is then provided to a model in a cold session with no access to the original source, and expansion into a different target language is requested.

This test examines whether the absence of language-specific syntax in Gestalt encoding supports faithful reconstruction in a language other than the source. A successful result produces a functionally equivalent program in the target language. Early testing of this capability has been encouraging. Systematic testing across multiple target languages is ongoing.

---

### Knowledge Base Token Efficiency Demonstration

This document is one half of a paired test. The other half is the Gestalt encoded version of this knowledge base, available in the repository alongside this document.

The pairing serves three purposes simultaneously. It is a direct token efficiency demonstration — the line count and token count of both versions are verifiable by anyone. It is a functional proof of the knowledge artifact concept — the Gestalt encoded version can be provided to any AI model to answer questions about Gestalt without prior exposure or configuration. And it is a self-demonstrating example of zero-shot comprehension — the encoding is readable and navigable by any model without a syntax guide.

Both documents are available in the repository. The methodology for the token efficiency comparison is documented there as well.

---

## 7. Repository and Resources

The Gestalt Syntax repository is the canonical home for the v4.0 specification, all supporting documents, test methodology, and results as they become available.

**https://github.com/ForwardCompatible/GestaltSyntax-4.0**

---

### What's Inside

| File | Purpose |
|---|---|
| `Gestalt_Spec_v40.md` | Canonical v4.0 specification. Human-readable reference. Start here. |
| `STYLE_GUIDE.md` | Operational encoding and expansion reference for AI models. |
| `SYSTEM_PROMPT.md` | Recommended system prompt for configuring an AI environment for Gestalt tasks. |
| `NLP_knowledgebase.md` | This document. Human-readable knowledge base. |
| `GST_knowledgebase.md` | Gestalt encoded version of this knowledge base. AI-deployable knowledge artifact. |
| `tests/` | Test methodologies, source files, and encoded samples for community reproduction. |
| `results/` | Test results as they become available. |

---

### Getting Started

**To ask questions about Gestalt:**
1. Provide `GST_knowledgebase.md` to your preferred AI model
2. Ask questions directly — no configuration or syntax guide required

**To encode a document into Gestalt:**
1. Provide `STYLE_GUIDE.md` to your AI model
2. Optionally configure your environment using `SYSTEM_PROMPT.md`
3. Ask your AI to encode your document using Gestalt v4.0 syntax

**To expand a Gestalt encoded document:**
1. Provide the Gestalt encoded document to your AI model
2. Ask your AI to expand it to the target language

*Providing `STYLE_GUIDE.md` alongside the document is not required but may reduce initial perplexity, particularly on smaller models. The impact of style guide presence on expansion quality is an area of ongoing research.*

---

## 8. Gestalt Syntax Reference

The following is the complete v4.0 encoding and expansion reference encoded in Gestalt. It is provided here as a functional syntax example and as the AI-consumable operational reference for encoding and expansion tasks.

```
META☩gestalt_style_guide☩lang:english,content_type:technical,lbrace_escape:☸,rbrace_escape:☥

DOC☩style_guide_v40☩type:operational_reference,domain:gestalt_encoding☸

SEC☩delimiters☩level:1☸
RULE☩delimiter_system☩domain:syntax,certainty:required☸
☩ separates block components, ☸ opens content block or section, ☥ closes content block or section, ASCII pipe not permitted, Unicode delimiters only☥
☥

SEC☩syntactic_patterns☩level:1☸

SEC☩content_block_pattern☩level:2☸
RULE☩content_block_format☩domain:syntax,certainty:required☸
BLOCK_TYPE☩identifier☩metadata☸semantic_content☥☥
RULE☩block_type☩domain:syntax,certainty:required☸
semantic classification of block☥
RULE☩identifier☩domain:syntax,certainty:required☸
concise unique label within scope, underscores replace spaces, unique within DOC standalone or CORPUS in corpus encoding☥
RULE☩metadata☩domain:syntax,certainty:required☸
required key:value pairs, multiple pairs comma separated, block without metadata cannot deterministically expand☥
RULE☩semantic_content☩domain:syntax,certainty:required☸
compressed semantic core of block☥
RULE☩block_validation_regex☩domain:syntax,certainty:required☸
^(\w+)☩([^☩]*?)☩([^☸]*?)☸([^☥]+)☥$ — applies content blocks only, use as construction check, structural declarations META and RELATES not validated, block not matching is malformed and will not expand reliably☥
☥

SEC☩structural_declaration_pattern☩level:2☸
RULE☩structural_declaration_format☩domain:syntax,certainty:required☸
flat statement, no opener or closer, only META and RELATES use this pattern☥
EXAMPLE☩structural_declaration_examples☩ref:structural_declaration_format☸
META☩document_identifier☩configuration_parameters
RELATES☩target_identifier☩relationship_type
☥
☥

SEC☩document_header☩level:1☸
RULE☩meta_standalone☩domain:syntax,certainty:required☸
standalone encoding: META required first line of document, corpus encoding: META precedes each DOC within CORPUS☥
EXAMPLE☩meta_code☩ref:meta_standalone☸
META☩code_syntax☩lang:python,lbrace_escape:☸,rbrace_escape:☥
☥
EXAMPLE☩meta_nlp☩ref:meta_standalone☸
META☩nlp_syntax☩lang:english,content_type:technical,lbrace_escape:☸,rbrace_escape:☥
☥
EXAMPLE☩meta_mixed☩ref:meta_standalone☸
META☩mixed_content☩code_lang:python,text_lang:english,lbrace_escape:☸,rbrace_escape:☥
☥
RULE☩configuration_parameters☩domain:syntax,certainty:required☸
lang: primary content language, code_lang: code language mixed docs, text_lang: NLP language mixed docs, content_type: domain hint technical/conversational/academic/creative, lbrace_escape: declares open delimiter, rbrace_escape: declares close delimiter☥
☥

SEC☩reserved_block_types☩level:1☸
RULE☩reservation_scope☩domain:syntax,certainty:required☸
reserved block type names may not be used as block type, identifier, or metadata value in any Gestalt document regardless of encoding context☥

RULE☩corpus_block☩domain:syntax,certainty:required☸
top level wrapper multi-file corpus encoding, required two or more files together, not required standalone, establishes shared namespace for all DOC blocks, identifiers unique within CORPUS scope, each DOC preceded by own META, globally reserved☥
EXAMPLE☩corpus_example☩ref:corpus_block☸
CORPUS☩project_name☩type:multi_file,domain:python_service☸
  META☩file_a☩lang:python,content_type:code,lbrace_escape:☸,rbrace_escape:☥
  DOC☩file_a☩type:service_layer☸
    blocks here
  ☥
  RELATES☩file_b☩depends_on
  META☩file_b☩lang:python,content_type:code,lbrace_escape:☸,rbrace_escape:☥
  DOC☩file_b☩type:constants☸
    blocks here
  ☥
☥
☥

RULE☩meta_block☩domain:syntax,certainty:required☸
document header, structural declaration, standalone: first line of document, corpus: immediately preceding each DOC block, declares parsing context and file-level configuration☥

RULE☩doc_block☩domain:syntax,certainty:required☸
document wrapper, required complete document encoding, optional fragment encoding, defines reconstruction boundary single file, corpus: DOC blocks children of CORPUS☥
EXAMPLE☩doc_example☩ref:doc_block☸
DOC☩document_name☩metadata☸
  blocks here
☥
☥

RULE☩sec_block☩domain:syntax,certainty:required☸
hierarchical section grouping, requires level metadata key, blocks inside inherit parent section context, sections optional flat structure valid, indentation optional no syntactic meaning☥
EXAMPLE☩sec_example☩ref:sec_block☸
SEC☩section_name☩level:1☸
  blocks here
☥
☥

RULE☩relates_block☩domain:syntax,certainty:required☸
structural declaration, declares directed connection from preceding block, scope determined by what it follows — content block: block level, DOC block: document level within corpus, stack multiple RELATES immediately after originating block before next block begins☥
EXAMPLE☩relates_example☩ref:relates_block☸
FUNC☩calculate_tax☩params:amount:float,return:float☸
multiplies amount by TAX_RATE, rounds to 2 decimal places☥
RELATES☩TAX_RATE☩depends_on
RELATES☩validate_input☩calls
☥

RULE☩definitions_block☩domain:syntax,certainty:required☸
declares custom block types or abbreviations, must appear top or bottom of document☥
EXAMPLE☩definitions_example☩ref:definitions_block☸
DEFINITIONS☩document_key☩scope:document☸
  CUSTOM_TYPE☩description
☥
☥

RULE☩example_block☩domain:syntax,certainty:required☸
preserves raw content exactly as written, never compress inside EXAMPLE block, use ref:parent to link to parent block, intentional illustrations only, never interchangeable with HOTSPOT☥
EXAMPLE☩example_block_example☩ref:example_block☸
CONCEPT☩function_name☩domain:python☸compressed semantic description☥
EXAMPLE☩function_name☩ref:parent☸
def function_name():
    pass
☥
☥

RULE☩annotation_block☩domain:syntax,certainty:required☸
preserves original comments, notes, editorial remarks exactly as found, applies code and NLP, never compress inside ANNOTATION block, use RELATES to link to annotated block☥
EXAMPLE☩annotation_example☩ref:annotation_block☸
FUNC☩calculate_tax☩params:amount:float,return:float☸
multiplies amount by TAX_RATE, rounds to 2 decimal places☥
ANNOTATION☩calculate_tax_note☩ref:calculate_tax☸
# do not change rounding behavior — matches legacy billing system expectation
☥
RELATES☩calculate_tax☩documents
☥

RULE☩hotspot_block☩domain:syntax,certainty:required☸
code encoding only, use when block cannot be encoded unambiguously, preserves original content exactly as found, identifier describes nature of ambiguity, use for circular dependencies, encoder continues without stopping, on expansion reconstruct from preserved content and surface whether tension resolved or requires human review☥
EXAMPLE☩hotspot_example☩ref:hotspot_block☸
HOTSPOT☩circular_dependency_calculate_tax_validate_input☩domain:code,certainty:ambiguous☸
original source content preserved exactly as found
☥
☥
☥

SEC☩nlp_block_types☩level:1☸
RULE☩nlp_vocabulary☩domain:encoding,certainty:reference☸
non-exhaustive starting vocabulary, custom types permitted with DEFINITIONS block☥
STATEMENT☩nlp_statement☩domain:reference,certainty:canonical☸facts, assertions, declarations, opinions☥
QUESTION☩nlp_question☩domain:reference,certainty:canonical☸information seeking, clarification, exploration☥
DESCRIPTION☩nlp_description☩domain:reference,certainty:canonical☸sensory, visual, environmental information☥
INTENT☩nlp_intent☩domain:reference,certainty:canonical☸objectives, goals, desired outcomes☥
EMOTION☩nlp_emotion☩domain:reference,certainty:canonical☸emotional states, sentiment, mood☥
INSTRUCTION☩nlp_instruction☩domain:reference,certainty:canonical☸commands, procedures, directions☥
NARRATIVE☩nlp_narrative☩domain:reference,certainty:canonical☸temporal sequences, cause and effect chains☥
CONCEPT☩nlp_concept☩domain:reference,certainty:canonical☸abstract ideas, definitions, theoretical constructs☥
PROTOCOL☩nlp_protocol☩domain:reference,certainty:canonical☸systematic procedures, workflows☥
RULE☩nlp_rule☩domain:reference,certainty:canonical☸constraints, requirements, limitations☥
☥

SEC☩code_block_types☩level:1☸
RULE☩func_block☩domain:encoding,certainty:required☸
defines a function☥
EXAMPLE☩func_example☩ref:func_block☸
FUNC☩function_name☩params:param_types,return:type,async:bool,complexity:O_notation☸
semantic description of function purpose☥
☥
RULE☩class_block☩domain:encoding,certainty:required☸
defines a class☥
EXAMPLE☩class_example☩ref:class_block☸
CLASS☩class_name☩inherits:parent,access:visibility,namespace:scope☸
semantic description of class purpose☥
☥
RULE☩control_structures☩domain:encoding,certainty:required☸
inline shorthand patterns for control flow☥
EXAMPLE☩control_example☩ref:control_structures☸
IF☩condition☸action☥ELSE☸alternative☥
LOOP☩type☩condition☸body☥
TRY☸attempt☥CATCH☩exception☸handler☥
SWITCH☩variable☸cases☥
☥
☥

SEC☩relationship_types☩level:1☸
RULE☩relates_syntax☩domain:syntax,certainty:required☸
RELATES☩target_identifier☩relationship_type☥
RULE☩logical_relationships☩domain:encoding,certainty:reference☸
supports, contradicts, builds_on, evidences, derives_from, exemplifies☥
RULE☩causal_relationships☩domain:encoding,certainty:reference☸
causes, results_in, enables, prevents, triggered_by, influences☥
RULE☩temporal_relationships☩domain:encoding,certainty:reference☸
precedes, follows, concurrent, interrupts, resumes, cyclical☥
RULE☩semantic_relationships☩domain:encoding,certainty:reference☸
defines, clarifies, contextualizes, generalizes, specifies, analogizes☥
RULE☩code_relationships☩domain:encoding,certainty:reference☸
calls, implements, contains, throws, returns, inherits, depends_on☥
RULE☩cross_domain_relationships☩domain:encoding,certainty:reference☸
explains, documents, tests, validates, implements_concept☥
☥

SEC☩metadata_rules☩level:1☸
RULE☩metadata_format☩domain:syntax,certainty:required☸
required every content block, key:value pairs comma separated, underscores replace spaces☥
RULE☩reserved_metadata_keys☩domain:syntax,certainty:required☸
level: SEC nesting depth, ref:parent: EXAMPLE links to parent, scope: DEFINITIONS scope, async: FUNC async flag, complexity: FUNC big O notation, access: CLASS/FUNC visibility☥
RULE☩common_metadata_categories☩domain:encoding,certainty:reference☸
certainty:level, domain:field, agent:actor, temporal:timeframe, spatial:location, intensity:level, valence:positive_negative_neutral, causality:type, safety:level, params:types, return:type☥
☥

SEC☩encoding_rules☩level:1☸

SEC☩corpus_encoding_rules☩level:2☸
RULE☩corpus_when☩domain:encoding,certainty:required☸
use CORPUS encoding two or more files with architectural relationships, do not use standalone encoding☥
RULE☩corpus_order☩domain:encoding,certainty:required☸
encode architectural dependency order, encode dependencies before files that depend on them☥
RULE☩corpus_identifiers☩domain:encoding,certainty:required☸
identifiers unique within CORPUS scope, cross-document block references use DOC_identifier:block_identifier format☥
RULE☩corpus_doc_relates☩domain:encoding,certainty:required☸
declare document-level relationships via RELATES following each DOC block☥
EXAMPLE☩corpus_doc_relates_example☩ref:corpus_doc_relates☸
DOC☩file_a☩type:service_layer☸
  blocks here
☥
RELATES☩file_b☩depends_on
RELATES☩file_c☩implements
☥
☥

SEC☩content_language_rules☩level:2☸
RULE☩nlp_content_language☩domain:encoding,certainty:required☸
NLP semantic content written in English☥
RULE☩code_content_language☩domain:encoding,certainty:required☸
code semantic content uses English or language-agnostic identifiers☥
RULE☩mixed_content_language☩domain:encoding,certainty:required☸
mixed documents: each domain follows own content language convention☥
☥

SEC☩block_granularity_rules☩level:2☸
RULE☩granularity☩domain:encoding,certainty:required☸
one block per discrete concept, if RELATES edge drawable between two pieces of content they belong in separate blocks☥
RULE☩preserve☩domain:encoding,certainty:required☸
nouns, verbs, adjectives, negations, quantifiers, domain terminology, semantic logic, architectural relationships☥
RULE☩omit☩domain:encoding,certainty:required☸
articles, most prepositions, conjunctions without logical weight, boilerplate, redundant restatements already in metadata☥
RULE☩guiding_test☩domain:encoding,certainty:required☸
if removing changes block meaning keep it, if meaning survives without it omit it☥
☥

SEC☩expansion_fidelity_requirements☩level:2☸
RULE☩explicit_dependencies☩domain:encoding,certainty:required☸
all dependency relationships explicitly declared via RELATES, no implicit dependencies☥
RULE☩metadata_sufficiency☩domain:encoding,certainty:required☸
metadata must disambiguate semantic content independently☥
RULE☩hotspot_requirement☩domain:encoding,certainty:required☸
block cannot be encoded unambiguously: use HOTSPOT, do not proceed with ambiguous encoding☥
RULE☩annotation_requirement☩domain:encoding,certainty:required☸
all comments, notes, editorial remarks in source content preserved verbatim using ANNOTATION blocks, never compress or omit☥
☥
☥

SEC☩expansion_rules☩level:1☸
RULE☩expansion_rule_0☩domain:expansion,certainty:required,order:0☸
if CORPUS present read it first, establish architectural context entire corpus, understand document-level relationships before expanding any DOC, expand in dependency order☥
RULE☩expansion_rule_1☩domain:expansion,certainty:required,order:1☸
traverse RELATES graph before beginning expansion, establish dependency order from declared relationship graph, expand dependencies before blocks that depend on them, do not rely on document order alone☥
RULE☩expansion_rule_2☩domain:expansion,certainty:required,order:2☸
metadata takes precedence resolving ambiguity, when metadata and semantic content conflict metadata wins☥
RULE☩expansion_rule_3☩domain:expansion,certainty:required,order:3☸
produce pragmatic idiomatic output target language, functional equivalence goal, do not infer add or expand anything not explicitly encoded, two expansions same encoding differ implementation details while preserving behavioral equivalence, intentional design not failure☥
RULE☩expansion_rule_4☩domain:expansion,certainty:required,order:4☸
handle HOTSPOT blocks explicitly, reconstruct using preserved content exactly as found, after full reconstruction review HOTSPOT in context, explicitly state whether tension resolved or requires human review, surface analysis end of reconstructed output☥
☥

☥
```

---
