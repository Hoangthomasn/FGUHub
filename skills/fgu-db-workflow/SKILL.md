---
name: fgu-db-workflow
description: Use when working with Fantasy Grounds Unity campaign db.xml files that need to be analyzed by category, disassembled into stable working sections, or reassembled into a valid db.xml without corrupting record structure, IDs, or top-level node ordering.
---

# FGU DB Workflow

Use this skill for `db.xml` workflow design and execution in this repo. The goal is lossless round-trip handling:

`db.xml -> category-aware working representation -> rebuilt db.xml`

## Use This Skill When

- The user wants to break down `db.xml` by category such as `item`, `npc`, `spell`, `feat`, or similar.
- The user wants to create or refine a disassembly/reassembly workflow before using it for real edits.
- The user wants help inserting new records while preserving Fantasy Grounds XML structure.
- The user wants to understand category boundaries, record IDs, nested child IDs, or rebuild safety rules.

## Core Rules

1. Treat the current `db.xml` as the source of truth. Do not invent category structure that conflicts with the live file.
2. Preserve the `<root>` attributes and top-level child node order unless the user explicitly wants a different rebuild policy.
3. Preserve node names exactly, including record container nodes like `id-00001`.
4. Preserve local child-list structure. Nested collections such as `powers`, `actions`, `spells`, `npclist`, and similar must retain their own local `id-xxxxx` containers.
5. For new records, assign IDs based on the target sibling container, not globally across the whole file.
6. Do not flatten mixed containers. Example: `item` contains both direct item records and nested `<category name="...">` nodes.
7. Prefer proving the workflow on one category first, but keep the design general enough to expand.
8. When uncertain, inspect the existing XML in this repo rather than assuming standard FG behavior.

## Workflow

### 1. Inspect First

- Read the live `db.xml`.
- Identify the relevant top-level nodes under `<root>`.
- For the target category, inspect whether it contains:
  - direct `id-xxxxx` records
  - nested `<category>` nodes
  - mixed content
  - nested child collections with their own IDs

For current repo structure and known category notes, read [references/dbxml-structure.md](references/dbxml-structure.md).

### 2. Define the Working Boundary

Before disassembly or insertion, determine:

- target top-level category, such as `item`, `npc`, `spell`, or `feat`
- whether the operation is read-only analysis, record insertion, or full split/rebuild
- whether the target category contains subcategories that must be preserved

For `item`, also read [references/item-rules.md](references/item-rules.md).

### 3. Disassemble Safely

When splitting `db.xml`, prefer category-level extraction that keeps each top-level node intact as XML, rather than flattening records into lossy data structures.

Minimum safe decomposition:

- capture the XML declaration and root attributes
- capture each top-level child node under `<root>` as its own preserved section
- inside a category, preserve direct child order and raw XML structure unless the user explicitly wants normalization

Preferred mental model:

- `root-metadata`
- `top-level-sections/<category>.xml`
- optional deeper working files only after the category round-trips safely

### 4. Reassemble Safely

When rebuilding:

- recreate the original XML declaration
- recreate the `<root>` node with original attributes
- reinsert top-level sections in original order
- ensure every section remains valid XML before final assembly
- verify that the rebuilt file is structurally parseable

Do not claim a rebuild is safe unless it has at least:

- successful XML parse
- preserved root attributes
- preserved top-level node order
- preserved category container names

### 5. Record Insertion Rules

When inserting a new record:

- place it in the correct top-level category
- if needed, place it inside the correct nested category container
- assign the next unused `id-xxxxx` among siblings in that target container
- for new nested child lists, the first child often starts at `id-00001`
- if copying an existing nested structure, renumber only when a sibling collision would occur

### 6. Communicate Assumptions

When generating or inserting records:

- state what came directly from the XML
- state what is inferred from similar records
- state what is still unknown or user-defined

## Output Style

Prefer compact, operational outputs:

- category map
- record template
- insertion checklist
- rebuild checklist
- explicit risk notes when structure is uncertain

Avoid long theoretical XML explanations when the user needs a practical move.
