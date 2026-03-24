# Automation Effect Syntax Rules

This reference is intended to be shared across record categories that use 5E automation effects in Fantasy Grounds, including:

- `item`
- `spell`
- `feat`
- `npc`
- any record that uses nested `powers`, `actions`, `effects`, or similar automation blocks

## Purpose

Use this file as the shared syntax reference for effect automation strings and related action fields.

This is intentionally named broadly so other category-specific guides can reference it without implying it only applies to items or spells.

## Scope

This reference is for:

- effect label/value syntax
- duration and targeting conventions
- conditional effect syntax
- automation-oriented action structure

This reference is not for:

- top-level `db.xml` placement
- sibling `id-xxxxx` assignment rules
- category container structure

Those rules should remain in:

- `dbxml-structure.md`
- category-specific files such as `item-rules.md`

## Primary Source

Primary reference:

- Fantasy Grounds Customer Portal: `5E Effects for Advanced Automation`
- URL: `https://fantasygroundsunity.atlassian.net/wiki/spaces/FGCP/pages/996642031/5E+Effects+for+Advanced+Automation`
- Page date observed: `November 17, 2025`

## Working Rule

When a generated record includes automation text such as an effect string, validate it against:

1. this shared reference
2. the official Fantasy Grounds automation documentation
3. known-good working records already present in this repo

## Initial Guidance

- Prefer known-good local effect syntax patterns when generating new records.
- Treat automation syntax as shared behavior across categories, even when XML containers differ.
- Validate both the surrounding XML structure and the effect text itself.
- Do not assume a record is correct just because it parses as XML.
- If a local working record and the official docs disagree, flag the difference and verify behavior before standardizing it.

## Planned Expansion

This file should later capture repo-approved conventions for:

- effect string formatting
- capitalization and token usage
- `IF` / `IFT` conditions
- duration notation
- targeting conventions
- item and spell automation examples
- validation heuristics for suspicious or incomplete effect strings
