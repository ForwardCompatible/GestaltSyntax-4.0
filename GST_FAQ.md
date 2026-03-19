META☩nlp_syntax☩lang:english,content_type:knowledge_base,lbrace_escape:☸,rbrace_escape:☥

DOC☩gestalt_knowledge_base☩version:4.0,purpose:ai_faq,domain:gestalt_syntax☸

SEC☩what_gestalt_is☩level:1☸

CONCEPT☩gestalt_definition☩domain:gestalt,version:4.0☸
AI-native syntax for structured semantic encoding of natural language and code into portable relationship-explicit format. Written by AI, read by AI, expanded by AI. Not intended for human authorship.☥

CONCEPT☩gestalt_origin☩domain:gestalt,temporal:2024☸
created from research into graph and vector memory systems. observation: explicitly declared relationships significantly impact AI contextual absorption and reasoning. question explored: does AI-native syntax exist, if not would one provide meaningful benefit☥

CONCEPT☩gestalt_positioning☩domain:gestalt,certainty:stated☸
transport format — self-contained document requiring no dependencies, no running environment, no installed tooling. any AI reads it directly. not replacement for AST or LSP — those are runtime tools tied to running environments, not portable. comparing Gestalt to AST/LSP is like comparing PDF to compiler — both relate to code but solve different problems for different consumers☥
RELATES☩gestalt_definition☩clarifies

CONCEPT☩gestalt_not☩domain:gestalt,certainty:stated☸
not lossless compression. not AST replacement. not LSP replacement. not compiler IR. not deterministic in formal sense. intentionally probabilistic to enable language agnosticity☥
RELATES☩gestalt_definition☩clarifies

☥

SEC☩core_principles☩level:1☸

CONCEPT☩principle_ai_comprehension☩domain:design☸
zero-shot understanding across AI models without prior training or examples. no model has been trained on Gestalt. zero-shot comprehension is observed result not assumption☥

CONCEPT☩principle_token_efficiency☩domain:design☸
maximum meaning per token through deliberate structural choices. framework overhead fixed cost amortizes over longer content. highly structured repetitive content sees higher compression benefit as length increases☥

CONCEPT☩principle_universal_language☩domain:design☸
semantic content expressed in language best representing concept, independent of source document language. NLP content uses English pending validation of character-based language token density☥

CONCEPT☩principle_unified_framework☩domain:design☸
code and NLP content share identical syntax patterns and delimiter conventions within single document☥

CONCEPT☩principle_relationship_preservation☩domain:design☸
connections between blocks explicit and declared, never inferred. no semantic connection should be left to inference☥

CONCEPT☩principle_guided_reconstruction☩domain:design☸
intentionally probabilistic to support language-agnostic encoding and expansion. encoding rules, explicit relationship declarations, metadata requirements exist to constrain expansion space toward faithful reconstruction of original intent. goal is consistent semantic interpretation across models, not identical output☥

☥

SEC☩delimiter_system☩level:1☸

CONCEPT☩delimiters☩domain:syntax,certainty:stated☸
Unicode characters chosen to avoid collision with code syntax. ☩ separates block components. ☸ opens content block or section. ☥ closes content block or section. ASCII pipe characters never permitted. reservation global — these characters must not be used for any other purpose within a document☥

☥

SEC☩syntactic_patterns☩level:1☸

CONCEPT☩content_block_pattern☩domain:syntax,certainty:stated☸
carries semantic payload. four required components: BLOCK_TYPE☩identifier☩metadata☸semantic_content☥
validation regex: ^(\w+)☩([^☩]*?)☩([^☸]*?)☸([^☥]+)☥$
applies to content blocks only. use as construction check during encoding. block not matching pattern is malformed and will not expand reliably☥

CONCEPT☩structural_declaration_pattern☩domain:syntax,certainty:stated☸
flat statements with no opener or closer. only META and RELATES use this pattern. META declares document parsing context, always first line. RELATES declares directed semantic connection from preceding block☥

CONCEPT☩relates_stacking☩domain:syntax,certainty:stated☸
all RELATES declarations for a block stack immediately after originating block before next content block begins. scope determined by what RELATES follows — after content block operates at block level, after DOC block operates at document level within corpus☥

☥

SEC☩document_structure☩level:1☸

CONCEPT☩meta_header☩domain:syntax,certainty:stated☸
required first line for standalone documents. precedes each DOC in corpus encoding. three variants: code uses lang:python, NLP uses lang:english content_type:technical, mixed uses code_lang and text_lang. lbrace_escape and rbrace_escape declare structural delimiters enabling deterministic parser construction☥

CONCEPT☩doc_block☩domain:syntax,certainty:stated☸
required for complete document encoding, optional for fragments. defines reconstruction boundary — expanding model knows entire enclosed graph represents one complete semantic unit. in corpus encoding DOC blocks are children of CORPUS block☥

CONCEPT☩corpus_block☩domain:syntax,certainty:stated☸
top level wrapper for multi-file corpus encoding. required when encoding two or more files together, not required for standalone encoding. establishes shared namespace — identifiers unique within CORPUS scope. globally reserved across all encoding contexts regardless of whether multi-file encoding in use☥

☥

SEC☩reserved_block_types☩level:1☸

CONCEPT☩reserved_types_overview☩domain:syntax,certainty:stated☸
reservation global across all encoding contexts. reserved names may not be used as block type, identifier, or metadata value in any Gestalt document regardless of encoding context. reserved types: CORPUS, META, DOC, SEC, RELATES, DEFINITIONS, EXAMPLE, ANNOTATION, HOTSPOT☥

CONCEPT☩sec_block☩domain:syntax,certainty:stated☸
groups related blocks into named hierarchical section. requires level metadata key. blocks inside section inherit context of parent section. sections optional — flat document structure valid. indentation optional, carries no syntactic meaning☥

CONCEPT☩definitions_block☩domain:syntax,certainty:stated☸
declares custom block types or abbreviations. must appear at top or bottom of document☥

CONCEPT☩example_block☩domain:syntax,certainty:stated☸
raw content container. content never compressed — preserved exactly as written. use ref:parent to link to parent block. for intentional illustrations only. never interchangeable with HOTSPOT☥

CONCEPT☩annotation_block☩domain:syntax,certainty:stated☸
preserves original comments, notes, editorial remarks exactly as found in source. applies to both code and NLP. content never compressed. use RELATES to link to annotated block. original author or developer intent must not be lost during encoding — frequently contains context that cannot be inferred from semantic content alone☥

CONCEPT☩hotspot_block☩domain:syntax,certainty:stated☸
reserved for code encoding. use when block cannot be encoded unambiguously. preserves original content exactly as found. use identifier to describe nature of ambiguity. circular dependencies also encoded as HOTSPOT — use identifier to describe circular relationship. encoder continues without stopping. on expansion reconstruct from preserved content then explicitly surface whether tension resolved or requires human review☥

☥

SEC☩block_vocabulary☩level:1☸

CONCEPT☩nlp_block_types☩domain:syntax,certainty:stated☸
non-exhaustive starting vocabulary. custom types permitted with DEFINITIONS block.
STATEMENT: facts assertions declarations opinions.
QUESTION: information seeking clarification exploration.
DESCRIPTION: sensory visual environmental information.
INTENT: objectives goals desired outcomes.
EMOTION: emotional states sentiment mood.
INSTRUCTION: commands procedures directions.
NARRATIVE: temporal sequences cause and effect chains.
CONCEPT: abstract ideas definitions theoretical constructs.
PROTOCOL: systematic procedures workflows.
RULE: constraints requirements limitations☥

CONCEPT☩code_block_types☩domain:syntax,certainty:stated☸
FUNC: defines function — params, return type, async bool, complexity notation.
CLASS: defines class — inherits, access visibility, namespace scope.
control structures inline: IF☩condition☸action☥ELSE☸alternative☥ — LOOP☩type☩condition☸body☥ — TRY☸attempt☥CATCH☩exception☸handler☥ — SWITCH☩variable☸cases☥☥

☥

SEC☩relationship_types☩level:1☸

CONCEPT☩relationship_vocabulary☩domain:syntax,certainty:stated☸
logical: supports, contradicts, builds_on, evidences, derives_from, exemplifies.
causal: causes, results_in, enables, prevents, triggered_by, influences.
temporal: precedes, follows, concurrent, interrupts, resumes, cyclical.
semantic: defines, clarifies, contextualizes, generalizes, specifies, analogizes.
code specific: calls, implements, contains, throws, returns, inherits, depends_on.
cross domain: explains, documents, tests, validates, implements_concept☥

☥

SEC☩metadata☩level:1☸

CONCEPT☩metadata_rules☩domain:syntax,certainty:stated☸
required on every content block. key:value pairs separated by commas. underscores in place of spaces. custom keys permitted without DEFINITIONS entry — descriptive key names considered self-documenting. must be sufficient to disambiguate semantic content independently☥

CONCEPT☩reserved_metadata_keys☩domain:syntax,certainty:stated☸
level: SEC — hierarchical nesting depth.
ref:parent: EXAMPLE — links example to parent block.
scope: DEFINITIONS — scope of definitions block.
async: FUNC — asynchronous function flag.
complexity: FUNC — big O notation.
access: CLASS FUNC — visibility scope☥

CONCEPT☩common_metadata_categories☩domain:syntax,certainty:stated☸
certainty:level, domain:field, agent:actor, temporal:timeframe, spatial:location, intensity:level, valence:positive_negative_neutral, causality:type, safety:level, params:types, return:type☥

☥

SEC☩encoding_rules☩level:1☸

CONCEPT☩block_granularity☩domain:encoding,certainty:stated☸
one block per discrete concept. if RELATES edge could be drawn between two pieces of content they belong in separate blocks☥

CONCEPT☩preserve_rules☩domain:encoding,certainty:stated☸
preserve: nouns, verbs, adjectives, negations, quantifiers, domain terminology, semantic logic, architectural relationships☥

CONCEPT☩omit_rules☩domain:encoding,certainty:stated☸
omit: articles, most prepositions, conjunctions without logical weight, boilerplate, redundant restatements already in metadata☥

CONCEPT☩guiding_test☩domain:encoding,certainty:stated☸
if removing something changes block meaning keep it. if meaning survives without it omit it☥

CONCEPT☩fidelity_requirements☩domain:encoding,certainty:stated☸
all dependency relationships explicitly declared via RELATES — no implicit dependencies.
metadata sufficient to disambiguate semantic content independently.
ambiguous blocks use HOTSPOT — do not proceed with ambiguous encoding.
all comments notes editorial remarks preserved verbatim in ANNOTATION blocks — never compress or omit☥

CONCEPT☩corpus_encoding_rules☩domain:encoding,certainty:stated☸
use CORPUS when encoding two or more files with architectural relationships.
encode in architectural dependency order — dependencies before files that depend on them.
identifiers unique within CORPUS scope.
cross-document block references use DOC_identifier:block_identifier format.
declare document-level relationships via RELATES following each DOC block☥

☥

SEC☩expansion_rules☩level:1☸

CONCEPT☩expansion_nature☩domain:expansion,certainty:stated☸
intentionally probabilistic. two expansions of same encoding will differ in implementation details while preserving behavioral equivalence. expected behavior not failure. rules below exist to constrain expansion space toward faithful reconstruction of original intent☥

CONCEPT☩expansion_rule_0☩domain:expansion,certainty:stated☸
if CORPUS present read it first. establish architectural context of entire corpus. understand document-level relationships before expanding any individual DOC. expand in dependency order☥

CONCEPT☩expansion_rule_1☩domain:expansion,certainty:stated☸
traverse RELATES graph before beginning expansion. establish dependency order from declared relationship graph. expand dependencies before blocks that depend on them. do not rely on document order alone☥

CONCEPT☩expansion_rule_2☩domain:expansion,certainty:stated☸
metadata takes precedence when resolving ambiguity. metadata is semantic checksum. when metadata and semantic content conflict metadata wins☥

CONCEPT☩expansion_rule_3☩domain:expansion,certainty:stated☸
produce pragmatic idiomatic output in target language. functional equivalence is goal. do not infer add or expand upon anything not explicitly encoded. if encoding does not specify it do not produce it☥

CONCEPT☩expansion_rule_4☩domain:expansion,certainty:stated☸
handle HOTSPOT blocks explicitly. reconstruct using preserved content exactly as found. after full expansion complete review each HOTSPOT in context. explicitly state whether tension resolved or requires human review. surface analysis at end of expanded output☥

☥

SEC☩test_results☩level:1☸

STATEMENT☩results_caveat☩domain:testing,certainty:preliminary☸
all results reported here are preliminary observations gathered under specific conditions. not validated findings. more rigorous controlled testing currently in progress. community reproduction and critique actively encouraged☥

STATEMENT☩zero_shot_comprehension☩domain:testing,certainty:observed☸
zero-shot comprehension observed across multiple AI models without syntax guide or prior exposure. models correctly identified block types, relationships, and semantic content without instruction☥

STATEMENT☩token_compression_observations☩domain:testing,certainty:measured☸
deterministic token counts measured across four tokenizer families: OpenAI o200k, Meta Llama 3.1, Google Gemma 3, Mistral Codestral. compression observed increases with document length and structural repetition. short documents may show minimal or negative compression due to framework overhead☥

STATEMENT☩expansion_fidelity_observations☩domain:testing,certainty:observed☸
COBOL to Python expansion: 8 of 8 functional tests passing. FORTRAN to Python expansion: 7 of 7 functional tests passing. expansions performed by models with no access to original source. expanded code ran without modification☥

STATEMENT☩hotspot_emergence☩domain:testing,certainty:observed☸
in cold session testing model identified four suspicious locations in Gestalt encoded script through semantic reasoning alone without being prompted. behavior emerged unprompted from structure of encoding☥

☥

SEC☩research_directions☩level:1☸

CONCEPT☩open_research☩domain:research,certainty:unproven☸
optimal language selection for NLP semantic content — character-based language token density unvalidated.
whether explicit relational structure improves transformer reasoning versus raw input — untested.
reasoning quality comparison against AST serialization JSON summary markdown outline — no baseline established.
corpus encoding at scale — behavior on large multi-file repositories unproven.
agent behavior under context pressure with Gestalt encoded rules versus markdown rules — untested.
attention entropy impact of delimiter fertility — anecdotal observation only, requires controlled testing with model internals access.
encoder-to-expander guidance at section or document level — identified gap pending testing to confirm whether needed☥

☥

SEC☩provenance☩level:1☸

CONCEPT☩gestalt_provenance☩domain:attribution,version:4.0☸
Gestalt Syntax v4.0 — created by Ryan Connelly.
canonical specification, style guide, system prompt, test results, community contributions: https://github.com/ForwardCompatible/GestaltSyntax-4.0
license: CC BY-NC 4.0. commercial use requires separate license agreement☥

☥

☥