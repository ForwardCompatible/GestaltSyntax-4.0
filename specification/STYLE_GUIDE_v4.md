# Gestalt Encoding Style Guide
**Canonical Reference — v4.0**

---

## Delimiters

| Character | Role |
|---|---|
| `☩` | Separates block components |
| `☸` | Opens a content block or section |
| `☥` | Closes a content block or section |

ASCII pipe characters are not permitted. Unicode delimiters only.

---

## Syntactic Patterns

Gestalt has two syntactic patterns. Every block follows one of these two patterns exactly.

### Content Block
Carries semantic payload. Metadata is required on every content block.

```
BLOCK_TYPE☩identifier☩metadata☸semantic_content☥
```

**BLOCK_TYPE** — Semantic classification of the block.

**identifier** — A concise label that uniquely identifies this block. Uses underscores in place of spaces. In standalone encoding identifiers must be unique within the DOC block. In corpus encoding identifiers must be unique within the CORPUS.

**metadata** — Required key:value pairs providing expansion context. Multiple pairs separated by commas. A block without metadata cannot deterministically expand.

**semantic_content** — The compressed semantic core of the block.

**Block validation regex:**
```
^(\w+)☩([^☩]*?)☩([^☸]*?)☸([^☥]+)☥$
```
Applies to content blocks only. Use as a construction check during encoding to confirm each content block has all four required components in the correct order. Structural declarations META and RELATES are not validated by this regex. A block that does not match this pattern is malformed and will not expand reliably.

### Structural Declaration
Flat statement with no opener or closer. Only META and RELATES use this pattern.

```
META☩document_identifier☩configuration_parameters
RELATES☩target_identifier☩relationship_type
```

---

## Document Header

In standalone encoding every Gestalt document must begin with a META declaration on the first line. In corpus encoding META precedes each DOC block within the CORPUS.

**Code:**
```
META☩code_syntax☩lang:python,lbrace_escape:☸,rbrace_escape:☥
```

**NLP:**
```
META☩nlp_syntax☩lang:english,content_type:technical,lbrace_escape:☸,rbrace_escape:☥
```

**Mixed:**
```
META☩mixed_content☩code_lang:python,text_lang:english,lbrace_escape:☸,rbrace_escape:☥
```

**Configuration parameters:**

| Parameter | Purpose |
|---|---|
| `lang` | Primary content language |
| `code_lang` | Code content language for mixed documents |
| `text_lang` | NLP content language for mixed documents |
| `content_type` | Domain optimization hint: technical, conversational, academic, creative |
| `lbrace_escape` | Declares the open delimiter character — enables parser identification of structural boundaries |
| `rbrace_escape` | Declares the close delimiter character — enables parser identification of structural boundaries |

The `lbrace_escape` and `rbrace_escape` parameters explicitly declare which Unicode characters serve as structural delimiters in this document. This declaration enables deterministic parser construction and regex validation against the declared delimiter set.

---

## Reserved Block Types

These block types have fixed meaning and must be used exactly as defined. Reservation is global across all encoding contexts — a reserved block type name may not be used as a block type, identifier, or metadata value in any Gestalt document regardless of encoding context.

**CORPUS** — Top level wrapper for multi-file corpus encoding. Required when encoding two or more files together. Not required for standalone encoding. Establishes the shared namespace for all DOC blocks within it — identifiers are unique within CORPUS scope. Each DOC within a CORPUS is preceded by its own META declaration. CORPUS is globally reserved — it may not be used as a block type, identifier, or metadata value in any Gestalt document regardless of whether multi-file encoding is in use.
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

**DOC** — Document wrapper. Required for complete document encoding. Optional for fragment encoding. Defines the reconstruction boundary for a single file. In corpus encoding, DOC blocks are children of the CORPUS block.
```
DOC☩document_name☩metadata☸
  blocks here
☥
```

**SEC** — Hierarchical section grouping. Requires `level` metadata key.
```
SEC☩section_name☩level:1☸
  blocks here
☥
```
Blocks inside a section inherit the context of their parent section. Sections are optional — a flat document structure is valid. Indentation is optional and carries no syntactic meaning.

**RELATES** — Structural declaration. Declares a directed connection from the preceding block. Scope is determined by what it follows — a RELATES following a content block operates at block level, a RELATES following a DOC block operates at document level within a corpus. Stack multiple RELATES declarations immediately after the originating block before the next block begins.
```
FUNC☩calculate_tax☩params:amount:float,return:float☸
multiplies amount by TAX_RATE, rounds to 2 decimal places☥
RELATES☩TAX_RATE☩depends_on
RELATES☩validate_input☩calls
```

**DEFINITIONS** — Declares custom block types or abbreviations. Must appear at top or bottom of document.
```
DEFINITIONS☩document_key☩scope:document☸
  CUSTOM_TYPE☩description
☥
```

**EXAMPLE** — Preserves raw content exactly as written. Never compress content inside an EXAMPLE block. Use `ref:parent` to link to its parent block. Used for intentional illustrations only — never interchangeable with HOTSPOT.
```
CONCEPT☩function_name☩domain:python☸compressed semantic description☥
EXAMPLE☩function_name☩ref:parent☸
def function_name():
    pass
☥
```

**ANNOTATION** — Preserves original comments, notes, and editorial remarks exactly as found in the source. Applies to both code and NLP content. Never compress content inside an ANNOTATION block. Use RELATES to link it to the block it annotates.
```
FUNC☩calculate_tax☩params:amount:float,return:float☸
multiplies amount by TAX_RATE, rounds to 2 decimal places☥
ANNOTATION☩calculate_tax_note☩ref:calculate_tax☸
# do not change rounding behavior — matches legacy billing system expectation
☥
RELATES☩calculate_tax☩documents
```

**HOTSPOT** — Reserved for code encoding only. Use when a block cannot be encoded unambiguously. Preserves original content exactly as found. Use the identifier to describe the nature of the ambiguity. Circular dependencies between blocks should also be encoded as HOTSPOT blocks — use the identifier to describe the nature of the circular relationship. Encoder continues without stopping. On expansion, reconstruct from preserved content and explicitly surface whether the tension is resolved or requires human review.
```
HOTSPOT☩circular_dependency_calculate_tax_validate_input☩domain:code,certainty:ambiguous☸
original source content preserved exactly as found
☥
```

---

## NLP Block Types

Non-exhaustive starting vocabulary. Custom types permitted with a DEFINITIONS block.

| Block Type | Use For |
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

## Code Block Types

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

**Control structures:**
```
IF☩condition☸action☥ELSE☸alternative☥
LOOP☩type☩condition☸body☥
TRY☸attempt☥CATCH☩exception☸handler☥
SWITCH☩variable☸cases☥
```

---

## Relationship Types

```
RELATES☩target_identifier☩relationship_type
```

**Logical:** `supports`, `contradicts`, `builds_on`, `evidences`, `derives_from`, `exemplifies`

**Causal:** `causes`, `results_in`, `enables`, `prevents`, `triggered_by`, `influences`

**Temporal:** `precedes`, `follows`, `concurrent`, `interrupts`, `resumes`, `cyclical`

**Semantic:** `defines`, `clarifies`, `contextualizes`, `generalizes`, `specifies`, `analogizes`

**Code Specific:** `calls`, `implements`, `contains`, `throws`, `returns`, `inherits`, `depends_on`

**Cross Domain:** `explains`, `documents`, `tests`, `validates`, `implements_concept`

---

## Metadata

Required on every content block. Key:value pairs separated by commas. Underscores in place of spaces.

```
key:value
key:value,key:value,key:value
```

**Reserved keys:**

| Key | Used On | Purpose |
|---|---|---|
| `level` | SEC | Hierarchical nesting depth |
| `ref:parent` | EXAMPLE | Links example to parent block |
| `scope` | DEFINITIONS | Scope of definitions block |
| `async` | FUNC | Asynchronous function flag |
| `complexity` | FUNC | Big O notation |
| `access` | CLASS, FUNC | Visibility scope |

**Common categories:** `certainty:level`, `domain:field`, `agent:actor`, `temporal:timeframe`, `spatial:location`, `intensity:level`, `valence:positive_negative_neutral`, `causality:type`, `safety:level`, `params:types`, `return:type`

---

## Encoding Rules

**Corpus encoding:**
- Use CORPUS when encoding two or more files with architectural relationships — do not use for standalone encoding
- Encode in architectural dependency order — encode dependencies before the files that depend on them
- Identifiers must be unique within the CORPUS scope
- Cross-document block references use `DOC_identifier:block_identifier` format
- Declare document-level relationships via RELATES following each DOC block

```
DOC☩file_a☩type:service_layer☸
  blocks here
☥
RELATES☩file_b☩depends_on
RELATES☩file_c☩implements
```

**Content language:**
- NLP semantic content is written in English
- Code semantic content uses English or language-agnostic identifiers
- In mixed documents each domain follows its own content language convention

**Block granularity:** One block per discrete concept. If you could draw a RELATES edge between two pieces of content, they belong in separate blocks.

**Preserve:** nouns, verbs, adjectives, negations, quantifiers, domain terminology, semantic logic, architectural relationships

**Omit:** articles, most prepositions, conjunctions without logical weight, boilerplate, redundant restatements already in metadata

**Guiding test:** If removing something changes the block's meaning, keep it. If the meaning survives without it, omit it.

**Expansion fidelity requirements:**
- All dependency relationships must be explicitly declared via RELATES — no implicit dependencies
- Metadata must be sufficient to disambiguate semantic content independently
- If a block cannot be encoded unambiguously, use HOTSPOT — do not proceed with an ambiguous encoding
- All comments, notes, and editorial remarks found in source content must be preserved verbatim using ANNOTATION blocks — never compress or omit them

---

## Expansion Rules

Gestalt is intentionally probabilistic to support language-agnostic encoding and expansion. Two expansions of the same encoding will differ in implementation details while preserving behavioral equivalence. This is expected behavior, not a failure. The rules below exist to constrain the expansion space toward faithful reconstruction of the original intent.

**0. If CORPUS is present, read it first**
Before expanding any content, read the CORPUS block to establish the architectural context of the entire corpus. Understand the document-level relationships between DOC blocks before expanding any individual DOC. Expand in dependency order — expand the DOC blocks that others depend on first.

**1. Traverse the RELATES graph before beginning expansion**
Establish dependency order from the declared relationship graph. Expand dependencies before the blocks that depend on them. Do not rely on document order alone.

**2. Metadata takes precedence when resolving ambiguity**
When metadata and semantic content appear to conflict, metadata wins.

**3. Produce pragmatic, idiomatic output in the target language**
Functional equivalence is the goal. Do not infer, add, or expand upon anything not explicitly encoded. If the encoding does not specify it, do not produce it. Two expansions of the same encoding will differ in implementation details while preserving behavioral equivalence. This is intentional design, not a failure.

**4. Handle HOTSPOT blocks explicitly**
Reconstruct using the preserved content exactly as found. After full reconstruction is complete, review the HOTSPOT in context and explicitly state whether the tension is resolved or requires human review. Surface this analysis at the end of the reconstructed output.

---
