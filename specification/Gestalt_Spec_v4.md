# Gestalt Syntax Specification
**Version 4.0 — Canonical Reference**

---

## Overview

Gestalt is an AI-native syntax for structured semantic encoding of natural language and code into a portable, relationship-explicit format. Unlike Abstract Syntax Trees and Language Server Protocol implementations — which produce graph representations tied to a running environment and require installed tooling to access — Gestalt produces a self-contained document that any AI model can ingest and reason over directly, without dependencies or environment state.

Gestalt was designed with two intentions:

- Represent the semantic intent and architectural relationships of a document or codebase in a structured, traversable graph format
- Make that representation portable and self-contained so any AI model can reason over it efficiently without prior context or tooling

Whether the design achieves either of these goals in practice is the subject of ongoing testing.

---

## Core Principles

**AI native comprehension** — Designed for zero-shot understanding across AI models without prior training or examples.

**Token efficiency optimization** — Prioritizes maximum meaning per token through deliberate structural choices.

**Nonlinear compression scaling** — Framework overhead is a fixed cost that amortizes over longer content. Short documents may see little or no compression benefit. Highly structured or repetitive content will see higher compression benefit as document length increases.

**Universal language support** — Semantic content may be expressed in the language that best represents the concept, independent of the source document language.

**Unified syntax framework** — Code and NLP content share identical syntax patterns and delimiter conventions within a single document.

**Semantic relationship preservation** — Connections between blocks are explicit and declared, never inferred.

**Guided reconstruction fidelity** — Gestalt is intentionally probabilistic to support language-agnostic encoding and expansion. The encoding rules, explicit relationship declarations, and metadata requirements exist to constrain the expansion space toward faithful reconstruction of the original intent. The goal is not identical output but consistent semantic interpretation across models.

---

## Delimiter System

Gestalt uses Unicode characters as delimiters, specifically chosen to avoid collision with code syntax. These characters must not be used for any other purpose within a document. ASCII pipe characters are not permitted as delimiters under any circumstance.

| Character | Role |
|---|---|
| `☩` | Separates block components |
| `☸` | Opens a content block or section |
| `☥` | Closes a content block or section |

---

## Syntactic Patterns

Gestalt defines two distinct syntactic patterns. Understanding which pattern applies to which block type is essential for correct encoding and parsing.

### Content Block Pattern

Content blocks carry semantic payload. They follow the full four-component format and are the primary unit of Gestalt encoding.

```
BLOCK_TYPE☩identifier☩metadata☸semantic_content☥
```

**BLOCK_TYPE** — Semantic classification of the block.

**identifier** — A concise label that uniquely identifies this block within the document. Uses underscores in place of spaces.

**metadata** — Required key:value pairs providing expansion context. Multiple pairs separated by commas. Metadata is required on every content block — a block without metadata cannot deterministically expand.

**semantic_content** — The compressed semantic core of the block.

**Block validation regex:**

```
^(\w+)☩([^☩]*?)☩([^☸]*?)☸([^☥]+)☥$
```

This regex validates that a content block is correctly formed. It applies to content blocks only — structural declarations META and RELATES follow their own defined flat patterns and are not validated by this regex. Use this regex as a construction check when encoding to confirm that each content block has all four required components in the correct order before the encoding is considered complete. A block that does not match this pattern is malformed and will not expand reliably.

### Structural Declaration Pattern

Structural declarations are flat statements that declare document context or semantic connections. They do not contain semantic payload and therefore have no opener or closer. Only two structural declarations exist in Gestalt: META and RELATES.

**META** declares document parsing context. It is always the first line of a Gestalt document.

```
META☩document_identifier☩configuration_parameters
```

**RELATES** declares a directed semantic connection from the preceding block to a target block.

```
RELATES☩target_identifier☩relationship_type
```

RELATES always follows immediately after the originating block. No semantic connection should be left to inference. When a block has multiple relationships, all RELATES declarations for that block stack immediately after it and before the next content block begins.

```
FUNC☩calculate_tax☩params:amount:float,return:float☸
multiplies amount by TAX_RATE, rounds to 2 decimal places☥
RELATES☩TAX_RATE☩depends_on
RELATES☩validate_input☩calls
RELATES☩format_output☩calls
```

---

## Document Header

Every Gestalt document must begin with a META declaration on the first line. Three standard variants exist depending on document domain:

**Code document:**
```
META☩code_syntax☩lang:python,lbrace_escape:☸,rbrace_escape:☥
```

**NLP document:**
```
META☩nlp_syntax☩lang:english,content_type:technical,lbrace_escape:☸,rbrace_escape:☥
```

**Mixed content document:**
```
META☩mixed_content☩code_lang:python,text_lang:english,lbrace_escape:☸,rbrace_escape:☥
```

### Configuration Parameters

| Parameter | Purpose |
|---|---|
| `lang` | Primary content language |
| `code_lang` | Code content language for mixed documents |
| `text_lang` | NLP content language for mixed documents |
| `content_type` | Domain optimization hint: technical, conversational, academic, creative |
| `lbrace_escape` | Declares the opening delimiter character for this document — enables parser identification of structural boundaries |
| `rbrace_escape` | Declares the closing delimiter character for this document — enables parser identification of structural boundaries |

The `lbrace_escape` and `rbrace_escape` parameters explicitly declare which Unicode characters serve as structural delimiters in this document. This declaration enables deterministic parser construction and regex validation against the declared delimiter set rather than against assumed defaults.

---

## Reserved Block Types

Reserved block types have fixed structural meaning and must be used exactly as defined. They may not be repurposed or redefined. Reservation is global across all encoding contexts — a reserved block type name may not be used as a block type, identifier, or metadata value in any Gestalt document regardless of the encoding context.

**CORPUS** — Top level wrapper for multi-file corpus encoding. Required when encoding more than one file together. Not required for standalone document encoding. CORPUS establishes the shared namespace for all DOC blocks within it — identifiers are unique within the CORPUS scope. Each DOC within a CORPUS is preceded by its own META declaration. CORPUS defines the architectural reconstruction boundary for the entire corpus. CORPUS is reserved across all encoding contexts — it may not be used as a block type, identifier, or metadata value in any Gestalt document regardless of whether multi-file encoding is in use.
```
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
```

**META** — Document header. Structural declaration. In standalone encoding: required as the first line of the document. In corpus encoding: required immediately preceding each DOC block within the CORPUS. Declares parsing context and file-level configuration.

**DOC** — Document wrapper. Required for any complete document encoding. Optional only when encoding a fragment or excerpt. DOC defines the reconstruction boundary for a single file — an expanding model encountering a DOC block knows the entire enclosed graph represents one complete semantic unit to reconstruct. In corpus encoding, DOC blocks are children of the CORPUS block.
```
DOC☩document_name☩metadata☸
  blocks here
☥
```

**SEC** — Groups related blocks into a named hierarchical section. Requires `level` metadata key.
```
SEC☩section_name☩level:1☸
  blocks here
☥
```

**RELATES** — Structural declaration. Declares a directed semantic connection. No opener or closer. The scope of a RELATES declaration is determined by what it follows — a RELATES following a content block operates at block level, a RELATES following a DOC block operates at document level within a corpus. Stack multiple RELATES declarations immediately after the originating block before the next block begins.
```
RELATES☩target_identifier☩relationship_type
```

**DEFINITIONS** — Declares custom block types or abbreviations used in the document. Must appear at the top or bottom of the document.
```
DEFINITIONS☩document_key☩scope:document☸
  CUSTOM_TYPE☩description
☥
```

**EXAMPLE** — Raw content container. Content inside an EXAMPLE block is never compressed — it is preserved exactly as written. Use `ref:parent` to link to its parent block. EXAMPLE blocks are used for intentional illustrations of correct content. HOTSPOT blocks are used exclusively when the encoder cannot resolve ambiguity. They are never interchangeable.
```
CONCEPT☩function_name☩domain:python☸compressed semantic description☥
EXAMPLE☩function_name☩ref:parent☸
def function_name():
    pass
☥
```

**ANNOTATION** — Preserves original comments, notes, and editorial remarks exactly as found in the source. Applies to both code and NLP content. Content inside an ANNOTATION block is never compressed. Use RELATES to link it to the block it annotates. ANNOTATION captures the original author or developer's intent as stated — this information must not be lost during encoding as it frequently contains context that cannot be inferred from the semantic content alone.
```
FUNC☩calculate_tax☩params:amount:float,return:float☸
multiplies amount by TAX_RATE, rounds to 2 decimal places☥
ANNOTATION☩calculate_tax_note☩ref:calculate_tax☸
# do not change rounding behavior — matches legacy billing system expectation
☥
RELATES☩calculate_tax☩documents
```

---

## Recommended NLP Block Types

The following is a non-exhaustive starting vocabulary for NLP content. Custom block types are permitted provided a DEFINITIONS block is supplied.

| Block Type | Purpose |
|---|---|
| STATEMENT | Facts, assertions, declarations, opinions |
| QUESTION | Information seeking, clarification, exploration |
| DESCRIPTION | Sensory, visual, or environmental information |
| INTENT | Objectives, goals, desired outcomes |
| EMOTION | Emotional states, sentiment, mood |
| INSTRUCTION | Commands, procedures, directions |
| NARRATIVE | Temporal sequences, cause and effect chains |
| CONCEPT | Abstract ideas, definitions, theoretical constructs |
| PROTOCOL | Systematic procedures, workflows |
| RULE | Constraints, requirements, limitations |

---

## Code Domain Block Types

The following block types are defined specifically for code compression and to support reconstruction fidelity. They extend the base content block format with code-specific metadata conventions.

**FUNC** — Defines a function.
```
FUNC☩function_name☩params:param_types,return:type,async:bool,complexity:O_notation☸
semantic description of function purpose☥
```

**CLASS** — Defines a class.
```
CLASS☩class_name☩inherits:parent,access:visibility,namespace:scope☸
semantic description of class purpose☥
```

**Control structures** follow inline shorthand patterns:
```
IF☩condition☸action☥ELSE☸alternative☥
LOOP☩type☩condition☸body☥
TRY☸attempt☥CATCH☩exception☸handler☥
SWITCH☩variable☸cases☥
```

**HOTSPOT** — Reserved flag block for code encoding. When an encoder cannot produce an unambiguous encoding of a block, it preserves the original content exactly as found inside a HOTSPOT block and continues encoding without stopping. HOTSPOT blocks signal locations where intent and implementation most likely diverge. Circular dependencies between blocks should also be encoded as HOTSPOT blocks — use the identifier to describe the nature of the circular relationship. On expansion, the model reconstructs from the preserved content and explicitly surfaces whether the tension is resolved or requires human review.
```
HOTSPOT☩circular_dependency_calculate_tax_validate_input☩domain:code,certainty:ambiguous☸
original source content preserved exactly as found
☥
```

---

## Encoding Examples

### NLP Encoding

**Source:**
The system failed to process the payment because the user's session had expired before the transaction could complete.

**Correct encoding:**
```
NARRATIVE☩payment_failure☩domain:payments,certainty:observed☸
system failed process payment, user session expired before transaction complete☥
RELATES☩session_expiry☩causes
```

**Incorrect encoding:**
```
STATEMENT☩payment_failure☸
the system failed to process the payment because the user session expired
☥
```

**Why it is wrong:** Metadata is missing — the block cannot deterministically expand without domain and certainty context. The semantic content is not compressed — articles and prepositions have not been omitted. The causal relationship between session expiry and payment failure is left implicit rather than declared via RELATES.

---

## Hierarchical Organization

Gestalt documents may be organized into nested sections using the SEC reserved block type. Sections group related blocks and provide inherited context to everything they contain.

```
SEC☩section_name☩level:1☸
  BLOCK_TYPE☩identifier☩metadata☸semantic_content☥

  SEC☩subsection_name☩level:2☸
    BLOCK_TYPE☩identifier☩metadata☸semantic_content☥
  ☥
☥
```

- The `level` metadata key is required on every SEC block
- Blocks inside a section inherit the context of their parent section
- Sections are optional — a flat document structure is valid
- Indentation is optional and carries no syntactic meaning

---

## Metadata

Metadata is required on every content block. It provides the contextual information that compression removes and is the primary mechanism by which deterministic expansion is achieved.

```
key:value
key:value,key:value,key:value
```

Keys and values use underscores in place of spaces. Custom keys are permitted without a DEFINITIONS entry as descriptive key names are considered self-documenting.

### Reserved Metadata Keys

| Key | Used On | Purpose |
|---|---|---|
| `level` | SEC | Indicates hierarchical nesting depth |
| `ref:parent` | EXAMPLE | Links the example to its parent block |
| `scope` | DEFINITIONS | Declares the scope of the definitions block |
| `async` | FUNC | Indicates asynchronous function |
| `complexity` | FUNC | Big O notation for algorithmic complexity |
| `access` | CLASS, FUNC | Visibility scope |

### Common Metadata Categories

- **Certainty** — `certainty:level`
- **Domain** — `domain:field`
- **Agent** — `agent:actor`
- **Temporal** — `temporal:timeframe`
- **Spatial** — `spatial:location`
- **Emotional** — `intensity:level`, `valence:positive_negative_neutral`
- **Causal** — `causality:type`
- **Code** — `async:bool`, `complexity:O_notation`, `safety:level`, `params:types`, `return:type`

---

## Relationship Types

Relationships between blocks are declared explicitly using RELATES. Place the declaration immediately after the originating block. No semantic connection should be left to inference.

```
RELATES☩target_identifier☩relationship_type
```

### Logical
`supports`, `contradicts`, `builds_on`, `evidences`, `derives_from`, `exemplifies`

### Causal
`causes`, `results_in`, `enables`, `prevents`, `triggered_by`, `influences`

### Temporal
`precedes`, `follows`, `concurrent`, `interrupts`, `resumes`, `cyclical`

### Semantic
`defines`, `clarifies`, `contextualizes`, `generalizes`, `specifies`, `analogizes`

### Code Specific
`calls`, `implements`, `contains`, `throws`, `returns`, `inherits`, `depends_on`

### Cross Domain
`explains`, `documents`, `tests`, `validates`, `implements_concept`

---

## Corpus Encoding

Corpus encoding applies when multiple files or documents are encoded together as a related body of work. The rules in this section extend the base encoding rules — they do not replace them.

### When to use CORPUS

Use CORPUS when encoding two or more files that have architectural relationships to each other. Do not use CORPUS for standalone document encoding — the base encoding rules apply without modification. CORPUS is a globally reserved block type and may not be used for any other purpose in any Gestalt document regardless of encoding context.

### Encoding order

Encode in architectural dependency order. Identify which files depend on which other files before encoding begins. Encode dependencies before the files that depend on them. This mirrors the expansion rule of traversing the RELATES graph before reconstructing.

### Identifier uniqueness

In standalone encoding, identifiers must be unique within their DOC block.

In corpus encoding, identifiers must be unique within the CORPUS. The DOC identifier serves as the namespace for all blocks within it. When a RELATES declaration in one DOC references a block in another DOC, use the format `DOC_identifier:block_identifier` to specify the target unambiguously.

```
RELATES☩file_b:calculate_tax☩calls
```

When a RELATES declaration references a block within the same DOC, no prefix is needed.

### Document level relationships

RELATES declarations following a DOC block declare architectural relationships between documents within the corpus. These operate at document level, not block level.

```
DOC☩file_a☩type:service_layer☸
  blocks here
☥
RELATES☩file_b☩depends_on
RELATES☩file_c☩implements
```

### Corpus validation

A correctly encoded corpus satisfies all base validation requirements for each individual DOC, plus:

- All cross-document dependencies are declared via RELATES at the DOC level
- All cross-document block references use the `DOC_identifier:block_identifier` format
- Encoding order reflects architectural dependency order

---

## Encoding Guidelines

Gestalt encoding is the process of reducing natural language or code to its semantic core. The goal is to preserve meaning completely while removing everything that does not contribute to it.

### Block Granularity

Each block represents one discrete concept or semantic unit. For NLP content, a paragraph containing multiple distinct ideas should become multiple blocks — one per concept. For code content, each function, class, and control structure maps to its own block. The guiding test for granularity: if you could draw a RELATES edge between two pieces of content, they belong in separate blocks.

### What to Preserve

- **Nouns and proper nouns** — the subjects and objects of meaning
- **Verbs** — the actions and states that connect meaning
- **Adjectives** — qualifiers that change or specify meaning
- **Negations** — "not", "never", "no" — removing these inverts meaning
- **Quantifiers** — "all", "some", "none", "every" — these define scope
- **Domain specific terminology** — technical terms that cannot be substituted without loss of precision
- **Semantic logic and architectural relationships** — the reasoning structure of code

### What to Omit

- **Articles** — "the", "a", "an"
- **Most prepositions** — unless their removal alters the relationship between elements
- **Conjunctions** — unless they carry logical weight such as "but", "however", or "except"
- **Boilerplate and repetitive patterns** — structural overhead that adds no semantic value
- **Redundant restatements** — information already captured in metadata

### The Guiding Test

If removing something changes what the block means, keep it. If the meaning survives without it, omit it.

### Encoding Requirements for Expansion Fidelity

The following requirements ensure that a Gestalt encoded document can be faithfully expanded:

- **All dependency relationships must be explicitly declared** — no dependency between blocks should be left implicit or assumed from document position alone. If one block depends on another, a RELATES declaration is required.
- **Metadata must be sufficient to disambiguate semantic content independently** — metadata is the semantic checksum. It must carry enough context that the semantic content of a block can be deterministically interpreted without reference to surrounding blocks.
- **Ambiguous blocks must be flagged using HOTSPOT** — if the encoder cannot produce an unambiguous encoding of a block, it must wrap the original content exactly as found in a HOTSPOT block rather than proceeding with an ambiguous encoding. The encoder continues without stopping. HOTSPOT blocks are surfaced for human review on expansion.
- **All comments, notes, and editorial remarks must be preserved using ANNOTATION** — original annotations found in source content must never be compressed or omitted. They must be captured verbatim in an ANNOTATION block and linked to their parent block via RELATES.

---

## Content Language

Gestalt distinguishes content language by domain:

**NLP content** — Semantic content is written in English. Testing of character-based languages for potential token density improvements is an identified research direction and has not yet been validated.

**Code content** — Semantic content uses English or language-agnostic identifiers. Code structure is already compressed through function names, types, and signatures.

**Mixed content** — Each domain follows its own content language convention within the same document.

---

## Content Type Considerations

Different content types compress differently. This is a design consideration, not a guarantee:

**Technical documentation** — High redundancy patterns make this a strong candidate for compression.

**Conversational text** — Filler words and informal patterns offer moderate compression opportunity. Emotional tone and social context should be preserved.

**Academic literature** — Already structurally optimized. Primary benefit may be improved relationship clarity rather than token reduction.

**Creative and literary content** — Deliberately word-choice optimized. Compression potential is minimal. Primary benefit is structural analysis support.

**Short content of any type** — Framework overhead dominates at low token counts. Compression benefits emerge at longer document lengths.

---

## Positioning Relative to Existing Tools

Gestalt is not a replacement for Abstract Syntax Trees, Language Server Protocol implementations, or compiler intermediate representations. Those tools produce graph representations of code that live in a running environment and require installed tooling, active language support, or a functioning parser to access.

Gestalt produces a portable semantic representation in a self-contained file. It requires no running environment, no installed dependencies, and no language-specific tooling to read. Any AI model can ingest a Gestalt encoded document in a single pass and reason over its semantic content and declared relationships directly.

The overlap with program analysis tools is real — RELATES declarations are conceptually similar to edges in a program dependence graph, and Gestalt's explicit call graph and dependency relationships cover similar ground to what static analysis tools produce automatically. The difference is portability and accessibility. Gestalt trades the precision and losslessness of machine-native graph representations for a format that travels with the document and requires nothing to interpret beyond the document itself.

---

## Mixed Content Documents

Gestalt handles mixed code and NLP content within a single document using the same delimiter system throughout. Each domain follows its own content language convention. Cross-domain relationships between code blocks and NLP blocks are expressed using the cross-domain RELATES types.

This unified approach enables complete system documentation where code blocks reference NLP concepts and NLP blocks reference code implementations within a single traversable semantic graph.

---

## Expansion Guidelines

Gestalt expansion is the process of producing target language output from a Gestalt encoded document. The goal is pragmatic, idiomatic equivalence — not literal transcription.

**1. Traverse the RELATES graph before beginning expansion**
Establish dependency order from the declared relationship graph. Expand dependencies before the blocks that depend on them. Do not rely on document order alone.

**2. Metadata takes precedence when resolving ambiguity**
Metadata is the semantic checksum. When metadata and semantic content appear to conflict, metadata wins. It carries the contextual information that compression removed.

**3. Produce pragmatic, idiomatic output in the target language**
Functional equivalence is the goal. Do not infer, add, or expand upon anything not explicitly encoded. If the encoding does not specify it, do not produce it. Two expansions of the same encoding will differ in implementation details while preserving behavioral equivalence. This is intentional design, not a failure.

**4. Handle HOTSPOT blocks explicitly**
When encountering a HOTSPOT block, reconstruct using the preserved content exactly as found. After full reconstruction is complete, review the HOTSPOT in context and explicitly state whether the tension is resolved or requires human review. Surface this analysis at the end of the reconstructed output.

---

## Validation Requirements

A correctly encoded Gestalt document should satisfy the following requirements:

**Semantic fidelity** — The compressed form must preserve the complete meaning of the original. Nothing that changes interpretation should be omitted.

**Guided reconstruction fidelity** — A Gestalt block must be encoded with sufficient precision that a model expanding it will arrive at a consistent semantic interpretation. If the same block could reasonably be interpreted two different ways, the encoding is incomplete. The system is intentionally probabilistic to support language agnosticity — the guardrails of explicit relationships, required metadata, and HOTSPOT flagging exist to constrain the expansion space toward faithful reconstruction of the original intent. Consistent interpretation of intent is the goal, not identical implementation.

**Relationship integrity** — All logical connections between blocks must be explicitly declared using RELATES.

**Syntactic correctness** — Content blocks must conform to the block validation regex. Structural declarations must follow their defined flat format.

**Corpus completeness** — When CORPUS is present, all DOC blocks within it must satisfy the above requirements individually. Additionally all cross-document dependencies must be declared at the DOC level via RELATES, all cross-document block references must use the `DOC_identifier:block_identifier` format, and encoding order must reflect architectural dependency order.

**Functional equivalence on expansion** — Expansion from a Gestalt encoding produces functionally equivalent output, not syntactically identical output. Two models expanding the same encoding will produce implementations that differ in variable names, loop structures, and syntactic choices while preserving behavioral equivalence. This is intentional. Gestalt encodes architectural intent and connection surfaces, not implementation details. Deviation at the implementation level while preserving intent is a design property, not a failure. Current testing suggests this may prevent implementation-specific bugs from being carried forward on expansion, but further testing is required before making that claim definitively.

---

## Future Research Directions

The following areas are identified for further investigation:

- Optimal language selection for NLP semantic content — comparison of character-based languages under real tokenization conditions
- Domain specific vocabulary optimization for technical fields
- Compression behavior across different document lengths and content types
- Delimiter alternatives with improved tokenizer vocabulary coverage
- FIM editing suitability — Gestalt may be better suited as a storage and transport format than as an actively edited format
- RAG and vector store comparison — Gestalt blocks as pre-chunked semantic units with explicit relationships
- KV cache pre-computation hypothesis — explicit relationship encoding may reduce inference cost beyond token count reduction
- Applications to legacy codebase analysis and cross-language translation

---
