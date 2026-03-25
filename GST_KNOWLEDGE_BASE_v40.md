META☩gst_knowledgebase☩lang:english,content_type:technical,lbrace_escape:☸,rbrace_escape:☥

DOC☩gst_knowledgebase_v40☩type:knowledge_base,domain:gestalt_syntax,version:4.0☸

SEC☩what_gestalt_is☩level:1☸

CONCEPT☩gestalt_definition☩domain:gestalt,certainty:canonical☸
AI-native syntax, structured semantic encoding natural language and code, portable relationship-explicit format☥
RELATES☩gestalt_one_liner☩clarifies

STATEMENT☩gestalt_one_liner☩domain:gestalt,certainty:canonical☸
AST and LSP keep structure sacrifice meaning, Gestalt keeps meaning sacrifices some explicit structure☥
RELATES☩gestalt_definition☩clarifies
RELATES☩two_kinds_lossy☩builds_on

STATEMENT☩ast_lsp_positioning☩domain:gestalt,certainty:observed☸
AST and LSP precise well-established tools solving different problem for different consumer, AST machine-readable graph syntactic structure, tells how program built not what it means or why, no semantic relationships☥
RELATES☩gestalt_definition☩contextualizes

STATEMENT☩gestalt_portability☩domain:gestalt,certainty:canonical☸
requires nothing to read, no installed environment no running parser no language-specific tooling, self-contained portable, any AI model ingests directly reasons over semantic content and declared relationships single pass☥
RELATES☩gestalt_definition☩specifies

SEC☩what_gestalt_encodes☩level:2☸
CONCEPT☩gestalt_encodes☩domain:gestalt,certainty:canonical☸
semantic meaning: intent and significance not just structure, explicit relationships: connections between ideas functions concepts declared directly not inferred☥
STATEMENT☩explicit_relationships_primacy☩domain:gestalt,certainty:observed☸
every connection declared, nothing implicit, most significant impact on AI reasoning over Gestalt encoded content☥
RELATES☩gestalt_encodes☩specifies
☥

SEC☩code_fidelity☩level:2☸
STATEMENT☩code_fidelity_principle☩domain:gestalt,certainty:canonical☸
preserves interface sacrifices internals, function names parameter types return types async flags complexity notation retained explicitly, implementation body encoded not contract☥
STATEMENT☩behavioral_equivalence☩domain:gestalt,certainty:canonical☸
expanding model knows function name accepts returns purpose, reconstructs body from context, result: behavioral equivalence and interface surface preservation, expanded code behaves identically exposes same contract☥
RELATES☩code_fidelity_principle☩specifies
STATEMENT☩architectural_intent☩domain:gestalt,certainty:canonical☸
encodes architectural intent, implementation details reconstructed not stored☥
RELATES☩behavioral_equivalence☩derives_from
STATEMENT☩cross_language_expansion☩domain:gestalt,certainty:hypothesis☸
no language-specific syntax in encoding, no inherent target language constraint, theoretically expandable any language model knows, early testing encouraging, rigorous cross-language testing ongoing☥
RELATES☩architectural_intent☩derives_from
☥

SEC☩two_kinds_lossy☩level:2☸
CONCEPT☩two_kinds_lossy☩domain:gestalt,certainty:canonical☸
lossy describes two distinct conditions not one, structurally lossy: does not preserve syntactic structure formatting implementation internals language-specific patterns, what lost reconstructable from remaining meaning, semantically lossy: loses meaning intent relational context, what lost unrecoverable☥
STATEMENT☩lossy_tradeoffs☩domain:gestalt,certainty:canonical☸
not equivalent tradeoffs, structurally lossy supports faithful reconstruction, semantically lossy cannot — discarded thing that makes reconstruction meaningful☥
RELATES☩two_kinds_lossy☩specifies
STATEMENT☩ast_lsp_lossy_type☩domain:gestalt,certainty:canonical☸
AST and LSP semantically lossy by design, preserve syntactic structure discard semantic meaning entirely, not their purpose no claim otherwise☥
RELATES☩two_kinds_lossy☩exemplifies
STATEMENT☩gestalt_lossy_type☩domain:gestalt,certainty:canonical☸
Gestalt structurally lossy by design, discards syntactic internals preserves semantic meaning and explicit relationships☥
RELATES☩two_kinds_lossy☩exemplifies
RELATES☩ast_lsp_lossy_type☩contradicts
STATEMENT☩lossy_broader_implication☩domain:gestalt,certainty:observed☸
distinction matters beyond Gestalt, AI context packages and AI-enabled workflows need vocabulary separating these failure modes, structurally lossy often acceptable, semantically lossy broken in ways may not be immediately visible☥
RELATES☩two_kinds_lossy☩builds_on
☥

SEC☩what_gestalt_is_not☩level:2☸
STATEMENT☩not_replacement☩domain:gestalt,certainty:canonical☸
not replacement for AST LSP compiler IRs, those live running environment serve compilers linters language servers, Gestalt lives in file serves AI models☥
STATEMENT☩intentionally_probabilistic☩domain:gestalt,certainty:canonical☸
not lossless format, intentionally probabilistic, constrains space valid interpretations toward faithful reconstruction without requiring identical output, two models expanding same encoding differ variable names syntactic choices while preserving behavioral equivalence and interface surfaces, design property not failure☥
STATEMENT☩not_compression_tool☩domain:gestalt,certainty:canonical☸
not compression tool traditional sense, token efficiency observed property not primary purpose, primary purpose: semantic fidelity portable dependency-free form☥
☥

SEC☩zero_shot_comprehension☩level:2☸
STATEMENT☩zero_shot_observation☩domain:gestalt,certainty:observed☸
no AI model exposed to Gestalt during training, zero-shot comprehension observed result across all tested models above approximately one billion parameters☥
STATEMENT☩encoding_vs_expansion_requirement☩domain:gestalt,certainty:observed☸
encoding tasks likely require style guide due novel syntax, reading and reasoning over Gestalt encoded documents requires no prior exposure☥
RELATES☩zero_shot_observation☩specifies
STATEMENT☩zero_shot_investigation☩domain:gestalt,certainty:hypothesis☸
whether property holds universally and boundary conditions active area of investigation☥
RELATES☩zero_shot_observation☩builds_on
☥

☥

SEC☩why_it_exists☩level:1☸

SEC☩background☩level:2☸
STATEMENT☩creator☩domain:gestalt,certainty:canonical,agent:ryan_connelly☸
created by Ryan Connelly, independent researcher, background data analysis and project management, has autism synesthesia eidetic memory — not binary photographic recall but scale where some things remembered with complete precision others not☥
STATEMENT☩origin_intent☩domain:gestalt,certainty:canonical,agent:ryan_connelly☸
combination produces cognitive experience difficult to describe historically difficult to communicate to others, Gestalt began as attempt to do exactly that☥
RELATES☩creator☩causes
☥

SEC☩cognitive_model☩level:2☸
STATEMENT☩synesthesia_effect☩domain:cognition,certainty:observed,agent:ryan_connelly☸
synesthesia produces involuntary cross-sensory associations☥
STATEMENT☩eidetic_effect☩domain:cognition,certainty:observed,agent:ryan_connelly☸
eidetic memory produces overwhelming volumes recalled information surfacing in response to contextual triggers☥
STATEMENT☩autism_effect☩domain:cognition,certainty:observed,agent:ryan_connelly☸
autism produces strong drive toward explicit structured pattern recognition over implicit social inference☥
STATEMENT☩cognitive_challenge☩domain:cognition,certainty:observed,agent:ryan_connelly☸
combination: when recall triggered enormous information surfaces simultaneously, navigating efficiently requires relationships between recalled items already encoded, filtering to contextually relevant fast and low-cost, nothing figured out on the fly, connections already declared☥
RELATES☩synesthesia_effect☩causes
RELATES☩eidetic_effect☩causes
RELATES☩autism_effect☩causes
STATEMENT☩cognitive_model_externalized☩domain:gestalt,certainty:canonical☸
not metaphor, functional description how contextually relevant information surfaces in that cognitive model, explicit relationship declarations in Gestalt not syntactic design choice, direct externalization of that process☥
RELATES☩cognitive_challenge☩derives_from
☥

SEC☩origin☩level:2☸
STATEMENT☩gestalt_origin☩domain:gestalt,certainty:canonical,agent:ryan_connelly☸
initial goal not to build encoding format, goal: use AI as interpreter to externalize internal cognitive process never successfully communicated to others, see whether structured representation could make it legible☥
STATEMENT☩self_discovery☩domain:gestalt,certainty:observed,agent:ryan_connelly☸
process designing representation as much experience of self-discovery as exercise understanding memory structures in general, formalizing cognitive model required understanding it precisely enough to write it down, that precision became Gestalt☥
RELATES☩gestalt_origin☩results_in
☥

SEC☩application_to_ai_context☩level:2☸
STATEMENT☩rag_behavior☩domain:ai_context,certainty:observed☸
RAG and most AI context packaging systems retrieve chunks raw information hand to model, model reasons over how chunks apply to current request, relevance figured out on the fly at inference time, consumes reasoning capacity could otherwise be spent on actual problem☥
STATEMENT☩cognitive_model_contrast☩domain:gestalt,certainty:observed,agent:ryan_connelly☸
cognitive model does not do this, relationships between recalled items already explicit, filtering fast because connections determining relevance already declared, cognitive load front-loaded into encoding not deferred to moment of use☥
RELATES☩rag_behavior☩contradicts
STATEMENT☩absence_visibility☩domain:gestalt,certainty:observed☸
requiring explicit relationships makes absence immediately visible, something surfacing without declared relationship either triggers creation of relationship or surfaces knowledge gap requiring resolution, implicit never passes through silently, anything without explicit relationship conspicuous by absence☥
RELATES☩cognitive_model_contrast☩specifies
STATEMENT☩ai_analogous_behavior☩domain:gestalt,certainty:observed☸
AI models appear to exhibit analogous behavior under Gestalt encoded input, when relationships explicitly declared undeclared connections become visible not invisible, model resolves or flags rather than papers over gaps, cannot silently paper over gaps as with raw unstructured context☥
RELATES☩absence_visibility☩analogizes
STATEMENT☩gestalt_ai_context_principle☩domain:gestalt,certainty:canonical☸
declaring relationships explicitly at encoding time means model does not have to reason over relevance — already declared, model free to reason over meaning instead☥
RELATES☩ai_analogous_behavior☩derives_from
RELATES☩cognitive_model_contrast☩implements_concept
☥

☥

SEC☩how_it_differs☩level:1☸

STATEMENT☩gestalt_position☩domain:gestalt,certainty:observed☸
occupies position no existing tool currently fills, understanding position requires understanding what surrounding tools do and who designed to serve☥

SEC☩rag_and_retrieval☩level:2☸
STATEMENT☩rag_mechanism☩domain:ai_context,certainty:observed☸
RAG retrieves chunks raw content from knowledge store injects into model context at inference time, model reasons how chunks relate to current request, relevance determined on the fly at moment of use by model itself☥
STATEMENT☩rag_semantic_gap☩domain:ai_context,certainty:observed☸
semantic relationships between retrieved chunks implicit at best absent at worst, nothing in retrieval process declares how one chunk connects to another or why chunk relevant beyond vector similarity, model carries full burden establishing context from raw material☥
RELATES☩rag_mechanism☩results_in
STATEMENT☩gestalt_vs_rag☩domain:gestalt,certainty:canonical☸
Gestalt does not retrieve, it encodes, relationships between concepts declared at encoding time and travel with document, model consuming Gestalt document does not have to establish context — already declared☥
RELATES☩rag_semantic_gap☩contradicts
☥

SEC☩vector_stores☩level:2☸
STATEMENT☩vector_store_mechanism☩domain:ai_context,certainty:observed☸
require AI model to encode content into embeddings and compatible embedding agent to retrieve and navigate at query time, relational structure lives in embedding space — latent not explicit opaque without compatible agent, encoding agent and retrieval agent coupled by design☥
STATEMENT☩gestalt_vs_vector_stores☩domain:gestalt,certainty:canonical☸
Gestalt also requires AI model to encode — overhead real not claimed otherwise, difference: relational structure lives in explicit declarations within document not latent embedding space, any AI model reads declarations directly at retrieval time, encoding agent not required, relational structure not opaque, coupling between encoding and retrieval eliminated☥
RELATES☩vector_store_mechanism☩contradicts
☥

SEC☩traditional_compression☩level:2☸
STATEMENT☩compression_framing_avoided☩domain:gestalt,certainty:canonical☸
Gestalt deliberately avoids compression framing☥
STATEMENT☩compression_definition☩domain:encoding,certainty:observed☸
traditional compression — lossless like ZIP or lossy like JPEG — implies recoverable original, lossless recovers exactly lossy recovers approximation degrading gracefully, both: goal fidelity to original artifact☥
STATEMENT☩gestalt_not_compression☩domain:gestalt,certainty:canonical☸
Gestalt makes no such claim, not attempting to recover original artifact — attempting to preserve semantic intent and support faithful reconstruction from that intent, two expansions produce functionally equivalent output differing in implementation details, not compression behavior, different class of encoding entirely, compression framing misrepresents and sets wrong expectations for success☥
RELATES☩compression_definition☩contradicts
RELATES☩compression_framing_avoided☩explains
☥

SEC☩runtime_tools☩level:2☸
STATEMENT☩runtime_tools_definition☩domain:ai_context,certainty:observed☸
AST LSP compiler IRs are runtime tools, require installed environment running parser language-specific tooling to produce and read, not portable — cannot hand someone AST and have them reason over it without standing up environment that produced it☥
STATEMENT☩gestalt_vs_runtime☩domain:gestalt,certainty:canonical☸
Gestalt requires nothing beyond document itself, no environment to install no parser to run no language-specific tooling to configure, portability gap between Gestalt and runtime tools not matter of degree — absolute, readable by any AI model in any context without precondition☥
RELATES☩runtime_tools_definition☩contradicts
☥

SEC☩consumer_distinction☩level:2☸
STATEMENT☩existing_tool_consumers☩domain:ai_context,certainty:observed☸
ASTs serve compilers and static analyzers, LSP implementations serve language servers and IDEs, vector stores serve retrieval pipelines, RAG systems serve inference engines assembling context at query time☥
STATEMENT☩gestalt_consumer☩domain:gestalt,certainty:observed☸
none designed to serve AI model as primary consumer of self-contained semantic document☥
RELATES☩existing_tool_consumers☩contextualizes
STATEMENT☩gestalt_fit_discovered☩domain:gestalt,certainty:observed,agent:ryan_connelly☸
Gestalt appears to fill this role — not designed around consumer profile but around cognitive model that happens to map closely onto how AI models consume and reason over context, design came first, fit was discovered☥
RELATES☩gestalt_consumer☩results_in
☥

☥

SEC☩token_efficiency☩level:1☸

STATEMENT☩token_efficiency_framing☩domain:gestalt,certainty:observed☸
token efficiency observed property of Gestalt encoding not primary purpose, emerges from structural design, behaves in specific predictable way worth understanding before drawing conclusions from any single test result☥

SEC☩framework_overhead☩level:2☸
STATEMENT☩overhead_definition☩domain:gestalt,certainty:observed☸
every Gestalt document carries fixed structural cost regardless of content, delimiter system META declaration reserved block types RELATES declarations consume approximately 170 tokens before single unit semantic content encoded☥
STATEMENT☩overhead_nature☩domain:gestalt,certainty:canonical☸
overhead not defect — cost of explicit relational structure that makes Gestalt useful, token efficiency cannot be evaluated against short documents, framework must be paid for before any efficiency realized☥
RELATES☩overhead_definition☩clarifies
☥

SEC☩efficiency_threshold☩level:2☸
STATEMENT☩threshold_behavior☩domain:gestalt,certainty:observed☸
token efficiency not linear and not guaranteed at any document length, threshold-dependent☥
STATEMENT☩below_threshold☩domain:gestalt,certainty:observed☸
below threshold — source document short enough framework overhead dominates — Gestalt encoded output larger than source, expected behavior not format failure, not designed for short content☥
RELATES☩threshold_behavior☩specifies
STATEMENT☩above_threshold☩domain:gestalt,certainty:observed☸
above threshold fixed overhead amortized across growing volume semantic content, as document length increases per-token cost framework proportionally smaller efficiency of semantic encoding proportionally larger, crossover point not fixed line depends on structural and repetitive density of source content☥
RELATES☩threshold_behavior☩specifies
RELATES☩below_threshold☩contradicts
☥

SEC☩nonlinear_scaling☩level:2☸
STATEMENT☩scaling_factors☩domain:gestalt,certainty:observed☸
beyond efficiency threshold token efficiency scales nonlinearly, two factors drive this: document length — longer documents amortize framework overhead further provide more surface area for semantic encoding, source structure and repetition — highly structured content with repeated patterns boilerplate redundant restatements encodes more aggressively than semantically dense content☥
STATEMENT☩content_type_efficiency☩domain:gestalt,certainty:observed☸
technical documentation legacy codebases procedural content strong candidates, literary and creative content already word-choice optimized offers minimal token efficiency benefit☥
RELATES☩scaling_factors☩exemplifies
STATEMENT☩efficiency_projection_warning☩domain:gestalt,certainty:observed☸
efficiency projections from one document type do not transfer reliably to another, testing on representative content only reliable measure☥
RELATES☩scaling_factors☩results_in
☥

SEC☩previous_data☩level:2☸
STATEMENT☩v32_data_retired☩domain:gestalt,certainty:canonical☸
prior to v4.0 token efficiency observations collected under v3.2 specification, that specification incomplete — encoding and expansion rules for code content underspecified leaving results on unreliable foundation, data points not cited here noted only to explain absence☥
STATEMENT☩v40_baseline☩domain:gestalt,certainty:canonical☸
v4.0 complete and internally consistent specification, all efficiency claims going forward grounded in testing conducted against it☥
RELATES☩v32_data_retired☩results_in
☥

☥

SEC☩theories_under_investigation☩level:1☸

STATEMENT☩theories_framing☩domain:gestalt,certainty:hypothesis☸
active hypotheses about Gestalt impact on AI model behavior, each observed consistently enough to warrant formal investigation, none validated against controlled methodology, presented as research questions not findings☥

SEC☩hallucination_reduction☩level:2☸
STATEMENT☩hallucination_observation☩domain:gestalt,certainty:observed☸
in sessions where Gestalt encoded document provided as primary context specific failure mode consistently absent: model hallucinates answers present in source text producing responses that drift from or contradict provided material and derail session☥
STATEMENT☩hallucination_testing☩domain:gestalt,certainty:hypothesis☸
observation consistent across sessions not yet tested against controlled methodology, QuALITY benchmark designed to examine directly — comparing model response quality raw NLP input versus same content encoded in Gestalt identical questions both, whether reduction attributable to explicit relational structure token efficiency or combination what testing designed to reveal☥
RELATES☩hallucination_observation☩builds_on
☥

SEC☩attention_persistence☩level:2☸
STATEMENT☩delimiter_fertility☩domain:gestalt,certainty:observed☸
Gestalt uses three Unicode delimiter characters each with tokenizer fertility rate approximately 2.0, each delimiter token represented consistently enough across training corpora that stable attention patterns likely associated with it☥
STATEMENT☩attention_persistence_hypothesis☩domain:gestalt,certainty:hypothesis☸
hypothesis: explicit relationship declarations in Gestalt create attention persisting through transformer layers that would normally attenuate — specifically early layers typically prunable without measurable impact on model output, if occurring explicit structure not merely helping model find meaning — may be changing how attention distributes across full forward pass☥
RELATES☩delimiter_fertility☩enables
STATEMENT☩attention_persistence_investigation☩domain:gestalt,certainty:hypothesis☸
requires interpretability tooling to investigate not yet tested, noted because provides potential mechanistic explanation for other observed behaviors and points toward specific falsifiable research direction☥
RELATES☩attention_persistence_hypothesis☩builds_on
☥

SEC☩knowledge_gap_surfacing☩level:2☸
STATEMENT☩cognitive_model_validation☩domain:cognition,certainty:observed,agent:ryan_connelly☸
in cognitive model that produced Gestalt explicit relationships serve validation function, something surfacing without declared relationship to current context absence immediately visible — either triggers creation of relationship or surfaces knowledge gap requiring resolution, nothing passes through silently, implicit never goes unexamined☥
STATEMENT☩ai_gap_surfacing_hypothesis☩domain:gestalt,certainty:hypothesis☸
hypothesis: AI models exhibit analogous behavior under Gestalt encoded input, when relationships explicitly declared undeclared connections become conspicuous not invisible, model resolves or flags — cannot silently paper over gaps as with raw unstructured context where implicit connections norm and missing relationships easy to miss entirely☥
RELATES☩cognitive_model_validation☩analogizes
STATEMENT☩gap_surfacing_testing☩domain:gestalt,certainty:hypothesis☸
behavior observed consistently in sessions using Gestalt encoded documents, controlled testing to confirm as reliable property of format rather than session-level artifact ongoing☥
RELATES☩ai_gap_surfacing_hypothesis☩builds_on
☥

SEC☩reasoning_impact☩level:2☸
STATEMENT☩reasoning_hypothesis☩domain:gestalt,certainty:hypothesis☸
Gestalt encoding hypothesized to impact model reasoning quality, nature and degree of that impact subject of active testing☥
☥

☥

SEC☩current_testing☩level:1☸

STATEMENT☩testing_framing☩domain:gestalt,certainty:canonical☸
all testing conducted against v4.0 specification exclusively, results from prior versions not cited, findings positive negative or inconclusive documented in repository as available, community contributions and independent reproductions welcome☥

SEC☩quality_benchmark☩level:2☸
STATEMENT☩quality_methodology☩domain:testing,certainty:planned☸
QuALITY benchmark compares model response quality raw NLP input versus same content encoded in Gestalt, same corpus both runs same questions asked against both, only variable between runs is format of input☥
STATEMENT☩quality_purpose☩domain:testing,certainty:planned☸
designed to examine hallucination reduction hypothesis directly — whether explicit relational structure reduces failure mode where model produces responses drifting from or contradicting provided source material, also provides initial data point on broader hypothesis Gestalt impacts model reasoning quality☥
RELATES☩quality_methodology☩enables
RELATES☩hallucination_reduction☩tests
RELATES☩reasoning_hypothesis☩tests
☥

SEC☩code_complexity_fidelity☩level:2☸
STATEMENT☩complexity_methodology☩domain:testing,certainty:planned☸
intentionally complex single-file program used as source, Lizard run against original to establish baseline complexity metrics, file encoded into Gestalt, completely different model with no access to original source expands Gestalt encoded document back to source language in cold session☥
STATEMENT☩complexity_purpose☩domain:testing,certainty:planned☸
expanded output verified for functional correctness, Lizard metrics run against it and compared to baseline, designed to examine whether behavioral equivalence and interface surface preservation hold in practice and whether expansion fidelity rules v4.0 produce reliable results across models☥
RELATES☩complexity_methodology☩enables
RELATES☩behavioral_equivalence☩tests
☥

SEC☩cross_language_expansion_test☩level:2☸
STATEMENT☩cross_language_methodology☩domain:testing,certainty:planned☸
self-contained single-file Python program encoded into Gestalt, Gestalt encoded document provided to model in cold session no access to original source, expansion into different target language requested☥
STATEMENT☩cross_language_purpose☩domain:testing,certainty:planned☸
examines whether absence of language-specific syntax in Gestalt encoding supports faithful reconstruction in language other than source, successful result produces functionally equivalent program in target language, early testing encouraging, systematic testing across multiple target languages ongoing☥
RELATES☩cross_language_methodology☩enables
RELATES☩cross_language_expansion☩tests
☥

SEC☩knowledge_base_demonstration☩level:2☸
STATEMENT☩kb_demonstration_methodology☩domain:testing,certainty:active☸
this document is one half of paired test, other half is Gestalt encoded version of this knowledge base available in repository alongside this document☥
STATEMENT☩kb_demonstration_purpose☩domain:testing,certainty:active☸
serves three purposes simultaneously: direct token efficiency demonstration — line count and token count both versions verifiable by anyone, functional proof of knowledge artifact concept — Gestalt encoded version providable to any AI model to answer questions about Gestalt without prior exposure or configuration, self-demonstrating example of zero-shot comprehension — encoding readable and navigable by any model without syntax guide☥
RELATES☩kb_demonstration_methodology☩enables
RELATES☩token_efficiency_framing☩tests
RELATES☩zero_shot_observation☩tests
☥

☥

SEC☩repository_and_resources☩level:1☸

STATEMENT☩repository_location☩domain:gestalt,certainty:canonical☸
canonical home for v4.0 specification all supporting documents test methodology and results, https://github.com/ForwardCompatible/GestaltSyntax-4.0☥

SEC☩repository_contents☩level:2☸
STATEMENT☩spec_file☩domain:gestalt,certainty:canonical☸
Gestalt_Spec_v40.md: canonical v4.0 specification, human-readable reference, start here☥
STATEMENT☩style_guide_file☩domain:gestalt,certainty:canonical☸
STYLE_GUIDE.md: operational encoding and expansion reference for AI models☥
STATEMENT☩system_prompt_file☩domain:gestalt,certainty:canonical☸
SYSTEM_PROMPT.md: recommended system prompt for configuring AI environment for Gestalt tasks☥
STATEMENT☩nlp_kb_file☩domain:gestalt,certainty:canonical☸
NLP_knowledgebase.md: human-readable knowledge base☥
STATEMENT☩gst_kb_file☩domain:gestalt,certainty:canonical☸
GST_knowledgebase.md: Gestalt encoded version of knowledge base, AI-deployable knowledge artifact☥
STATEMENT☩tests_directory☩domain:gestalt,certainty:canonical☸
tests/: test methodologies source files and encoded samples for community reproduction☥
STATEMENT☩results_directory☩domain:gestalt,certainty:canonical☸
results/: test results as they become available☥
☥

SEC☩getting_started☩level:2☸
INSTRUCTION☩ask_questions☩domain:gestalt,certainty:canonical☸
to ask questions about Gestalt: provide GST_knowledgebase.md to preferred AI model, ask questions directly, no configuration or syntax guide required☥
INSTRUCTION☩encode_document☩domain:gestalt,certainty:canonical☸
to encode document into Gestalt: provide STYLE_GUIDE.md to AI model, optionally configure environment using SYSTEM_PROMPT.md, ask AI to encode document using Gestalt v4.0 syntax☥
INSTRUCTION☩expand_document☩domain:gestalt,certainty:canonical☸
to expand Gestalt encoded document: provide Gestalt encoded document to AI model, ask AI to expand to target language, providing STYLE_GUIDE.md not required but may reduce initial perplexity particularly smaller models, impact of style guide presence on expansion quality area of ongoing research☥
☥

☥

SEC☩gestalt_syntax_reference☩level:1☸

STATEMENT☩syntax_reference_purpose☩domain:gestalt,certainty:canonical☸
complete v4.0 encoding and expansion reference encoded in Gestalt, provided as functional syntax example and AI-consumable operational reference for encoding and expansion tasks☥

SEC☩delimiters_ref☩level:2☸
RULE☩delimiter_system_ref☩domain:syntax,certainty:required☸
☩ separates block components, ☸ opens content block or section, ☥ closes content block or section, ASCII pipe not permitted, Unicode delimiters only☥
☥

SEC☩syntactic_patterns_ref☩level:2☸
RULE☩content_block_format_ref☩domain:syntax,certainty:required☸
BLOCK_TYPE☩identifier☩metadata☸semantic_content☥, BLOCK_TYPE: semantic classification, identifier: concise unique label underscores replace spaces unique within DOC standalone or CORPUS in corpus encoding, metadata: required key:value pairs comma separated block without metadata cannot deterministically expand, semantic_content: compressed semantic core☥
RULE☩block_validation_regex_ref☩domain:syntax,certainty:required☸
^(\w+)☩([^☩]*?)☩([^☸]*?)☸([^☥]+)☥$ applies content blocks only, construction check during encoding, structural declarations META and RELATES not validated, block not matching malformed will not expand reliably☥
RULE☩structural_declaration_format_ref☩domain:syntax,certainty:required☸
flat statement no opener or closer, only META and RELATES use this pattern: META☩document_identifier☩configuration_parameters and RELATES☩target_identifier☩relationship_type☥
☥

SEC☩document_header_ref☩level:2☸
RULE☩meta_placement_ref☩domain:syntax,certainty:required☸
standalone encoding: META required first line of document, corpus encoding: META precedes each DOC within CORPUS☥
RULE☩meta_variants_ref☩domain:syntax,certainty:required☸
code: META☩code_syntax☩lang:python,lbrace_escape:☸,rbrace_escape:☥ — NLP: META☩nlp_syntax☩lang:english,content_type:technical,lbrace_escape:☸,rbrace_escape:☥ — mixed: META☩mixed_content☩code_lang:python,text_lang:english,lbrace_escape:☸,rbrace_escape:☥☥
RULE☩configuration_parameters_ref☩domain:syntax,certainty:required☸
lang: primary content language, code_lang: code language mixed docs, text_lang: NLP language mixed docs, content_type: domain hint technical/conversational/academic/creative, lbrace_escape: declares open delimiter, rbrace_escape: declares close delimiter☥
☥

SEC☩reserved_block_types_ref☩level:2☸
RULE☩reservation_scope_ref☩domain:syntax,certainty:required☸
reserved names may not be used as block type identifier or metadata value in any Gestalt document regardless of encoding context☥
RULE☩corpus_ref☩domain:syntax,certainty:required☸
top level wrapper multi-file corpus encoding, required two or more files together not required standalone, establishes shared namespace DOC blocks identifiers unique within CORPUS scope, each DOC preceded by own META, globally reserved☥
RULE☩meta_ref☩domain:syntax,certainty:required☸
document header structural declaration, standalone: first line of document, corpus: immediately preceding each DOC block, declares parsing context and file-level configuration☥
RULE☩doc_ref☩domain:syntax,certainty:required☸
document wrapper required complete document encoding optional fragment encoding, defines reconstruction boundary single file, corpus: DOC blocks children of CORPUS☥
RULE☩sec_ref☩domain:syntax,certainty:required☸
hierarchical section grouping requires level metadata key, blocks inside inherit parent section context, sections optional flat structure valid, indentation optional no syntactic meaning☥
RULE☩relates_ref☩domain:syntax,certainty:required☸
structural declaration declares directed connection from preceding block, scope determined by what it follows — content block: block level, DOC block: document level within corpus, stack multiple RELATES immediately after originating block before next block begins☥
RULE☩definitions_ref☩domain:syntax,certainty:required☸
declares custom block types or abbreviations, must appear top or bottom of document☥
RULE☩example_ref☩domain:syntax,certainty:required☸
preserves raw content exactly as written never compress inside EXAMPLE block, use ref:parent to link to parent block, intentional illustrations only never interchangeable with HOTSPOT☥
RULE☩annotation_ref☩domain:syntax,certainty:required☸
preserves original comments notes editorial remarks exactly as found applies code and NLP, never compress inside ANNOTATION block, use RELATES to link to annotated block☥
RULE☩hotspot_ref☩domain:syntax,certainty:required☸
code encoding only, use when block cannot be encoded unambiguously, preserves original content exactly as found, identifier describes nature of ambiguity, use for circular dependencies, encoder continues without stopping, on expansion reconstruct from preserved content surface whether tension resolved or requires human review☥
☥

SEC☩nlp_block_types_ref☩level:2☸
RULE☩nlp_vocabulary_ref☩domain:encoding,certainty:reference☸
non-exhaustive starting vocabulary custom types permitted with DEFINITIONS block: STATEMENT facts assertions declarations opinions, QUESTION information seeking clarification exploration, DESCRIPTION sensory visual environmental information, INTENT objectives goals desired outcomes, EMOTION emotional states sentiment mood, INSTRUCTION commands procedures directions, NARRATIVE temporal sequences cause and effect chains, CONCEPT abstract ideas definitions theoretical constructs, PROTOCOL systematic procedures workflows, RULE constraints requirements limitations☥
☥

SEC☩code_block_types_ref☩level:2☸
RULE☩func_ref☩domain:encoding,certainty:required☸
FUNC☩function_name☩params:param_types,return:type,async:bool,complexity:O_notation☸semantic description of function purpose☥☥
RULE☩class_ref☩domain:encoding,certainty:required☸
CLASS☩class_name☩inherits:parent,access:visibility,namespace:scope☸semantic description of class purpose☥☥
RULE☩control_structures_ref☩domain:encoding,certainty:required☸
IF☩condition☸action☥ELSE☸alternative☥ — LOOP☩type☩condition☸body☥ — TRY☸attempt☥CATCH☩exception☸handler☥ — SWITCH☩variable☸cases☥☥
☥

SEC☩relationship_types_ref☩level:2☸
RULE☩logical_ref☩domain:encoding,certainty:reference☸
supports, contradicts, builds_on, evidences, derives_from, exemplifies☥
RULE☩causal_ref☩domain:encoding,certainty:reference☸
causes, results_in, enables, prevents, triggered_by, influences☥
RULE☩temporal_ref☩domain:encoding,certainty:reference☸
precedes, follows, concurrent, interrupts, resumes, cyclical☥
RULE☩semantic_ref☩domain:encoding,certainty:reference☸
defines, clarifies, contextualizes, generalizes, specifies, analogizes☥
RULE☩code_specific_ref☩domain:encoding,certainty:reference☸
calls, implements, contains, throws, returns, inherits, depends_on☥
RULE☩cross_domain_ref☩domain:encoding,certainty:reference☸
explains, documents, tests, validates, implements_concept☥
☥

SEC☩metadata_rules_ref☩level:2☸
RULE☩metadata_format_ref☩domain:syntax,certainty:required☸
required every content block, key:value pairs comma separated, underscores replace spaces☥
RULE☩reserved_keys_ref☩domain:syntax,certainty:required☸
level: SEC nesting depth, ref:parent: EXAMPLE links to parent, scope: DEFINITIONS scope, async: FUNC async flag, complexity: FUNC big O notation, access: CLASS/FUNC visibility☥
RULE☩common_categories_ref☩domain:encoding,certainty:reference☸
certainty:level, domain:field, agent:actor, temporal:timeframe, spatial:location, intensity:level, valence:positive_negative_neutral, causality:type, safety:level, params:types, return:type☥
☥

SEC☩encoding_rules_ref☩level:2☸
RULE☩corpus_when_ref☩domain:encoding,certainty:required☸
use CORPUS encoding two or more files with architectural relationships, do not use for standalone encoding☥
RULE☩corpus_order_ref☩domain:encoding,certainty:required☸
encode architectural dependency order, encode dependencies before files that depend on them☥
RULE☩corpus_identifiers_ref☩domain:encoding,certainty:required☸
identifiers unique within CORPUS scope, cross-document block references use DOC_identifier:block_identifier format, declare document-level relationships via RELATES following each DOC block☥
RULE☩content_language_ref☩domain:encoding,certainty:required☸
NLP semantic content written in English, code semantic content uses English or language-agnostic identifiers, mixed documents each domain follows own content language convention☥
RULE☩granularity_ref☩domain:encoding,certainty:required☸
one block per discrete concept, if RELATES edge drawable between two pieces of content they belong in separate blocks☥
RULE☩preserve_ref☩domain:encoding,certainty:required☸
nouns, verbs, adjectives, negations, quantifiers, domain terminology, semantic logic, architectural relationships☥
RULE☩omit_ref☩domain:encoding,certainty:required☸
articles, most prepositions, conjunctions without logical weight, boilerplate, redundant restatements already in metadata☥
RULE☩guiding_test_ref☩domain:encoding,certainty:required☸
if removing changes block meaning keep it, if meaning survives without it omit it☥
RULE☩explicit_dependencies_ref☩domain:encoding,certainty:required☸
all dependency relationships explicitly declared via RELATES, no implicit dependencies☥
RULE☩metadata_sufficiency_ref☩domain:encoding,certainty:required☸
metadata must disambiguate semantic content independently☥
RULE☩hotspot_requirement_ref☩domain:encoding,certainty:required☸
block cannot be encoded unambiguously: use HOTSPOT, do not proceed with ambiguous encoding☥
RULE☩annotation_requirement_ref☩domain:encoding,certainty:required☸
all comments notes editorial remarks in source content preserved verbatim using ANNOTATION blocks, never compress or omit☥
☥

SEC☩expansion_rules_ref☩level:2☸
RULE☩expansion_rule_0_ref☩domain:expansion,certainty:required,order:0☸
if CORPUS present read it first, establish architectural context entire corpus, understand document-level relationships before expanding any DOC, expand in dependency order☥
RULE☩expansion_rule_1_ref☩domain:expansion,certainty:required,order:1☸
traverse RELATES graph before beginning expansion, establish dependency order from declared relationship graph, expand dependencies before blocks that depend on them, do not rely on document order alone☥
RULE☩expansion_rule_2_ref☩domain:expansion,certainty:required,order:2☸
metadata takes precedence resolving ambiguity, when metadata and semantic content conflict metadata wins☥
RULE☩expansion_rule_3_ref☩domain:expansion,certainty:required,order:3☸
produce pragmatic idiomatic output target language, functional equivalence goal, do not infer add or expand anything not explicitly encoded, two expansions same encoding differ implementation details while preserving behavioral equivalence, intentional design not failure☥
RULE☩expansion_rule_4_ref☩domain:expansion,certainty:required,order:4☸
handle HOTSPOT blocks explicitly, reconstruct using preserved content exactly as found, after full reconstruction review HOTSPOT in context, explicitly state whether tension resolved or requires human review, surface analysis end of reconstructed output☥
☥

☥

☥
