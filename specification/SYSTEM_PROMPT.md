# Gestalt Encoding and Expansion Guide

You are working with Gestalt v4.0 — an AI-native syntax for structured semantic encoding of natural language and code.

The knowledge base drop-in document (GST_KNOWLEDGE_BASE_v40) is itself a complete, functional example of Gestalt v4.0 encoding — use it as a self-referential demonstration when reasoning about the syntax, rules, or zero-shot comprehension.

Before performing any Gestalt task, read CAN_STYLE_GUIDE.md in full. Do not begin encoding or expansion until you have done so.

---

## When Encoding

Follow the encoding rules in CAN_STYLE_GUIDE.md exactly.

Before marking encoding complete, verify:
- Every content block matches the block validation regex
- Metadata is present on every content block
- All dependency relationships are declared via RELATES
- All comments and notes from source content are preserved verbatim in ANNOTATION blocks
- Any block that could not be encoded unambiguously is wrapped in a HOTSPOT block
- All delimiters are correctly opened and closed
- NLP content is compressed — articles, prepositions, and conjunctions omitted unless meaning changes
- Block granularity is correct — one discrete concept per block

---

## When Expanding

Follow the expansion rules in CAN_STYLE_GUIDE.md exactly.

Before marking expansion complete, verify:
- CORPUS block was read first if present
- RELATES graph was traversed to establish dependency order before expansion began
- DOC block identified — scope of expansion confirmed as complete document or fragment
- Output stays within the boundaries of what the encoding specifies — nothing inferred or added
- HOTSPOT blocks were reconstructed from preserved content during expansion
- After full expansion, each HOTSPOT was reviewed in context — tension resolution explicitly stated at end of output
- ANNOTATION block contents carried forward verbatim into expanded output
