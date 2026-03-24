# Session Notes - 2026-03-23

## What We Did

- Confirmed that live Fantasy Grounds item edits must go into `db.xml`, not `db.session.*.xml`.
- Reviewed and used the `fgu-db-workflow` skill as the base workflow for safe record insertion.
- Confirmed the `item` section is mixed content and can contain both direct `id-xxxxx` records and nested `<category>` containers.
- Used existing nearby item records as templates instead of inventing a schema from scratch.
- Added a shared cross-category reference file:
  - `automation-effect-syntax-rules.md`
- Confirmed that the official Fantasy Grounds page `5E Effects for Advanced Automation` should remain the source of truth for automation syntax.
- Generated draft item XML blocks for:
  - `Can of Sprite`
  - `Can of Dr Pepper`
- Generated and tested a draft/live insert for:
  - `Cup of Green Tea`
- Inserted live item records into `db.xml` for:
  - `Can of Sprite` as top-level `item` record `id-00085`
  - `Can of Dr Pepper` as top-level `item` record `id-00087`
- Updated the soda item effect strings to use the newer syntax format:
  - `SKILL: 1, perception`
- Identified that some IDs such as `id-00086` were already occupied by existing live records, so new inserts must be checked against the actual local sibling list.
- Removed the soda draft files and standalone soda records after testing.
- Inserted `Cup of Green Tea` into the `item > category name="(Potions)"` container for testing, then removed it after discovering ID collision behavior in Fantasy Grounds.

## Key Lessons

- A draft XML file by itself will not make a record appear in Fantasy Grounds.
- The safest generation method is:
  - inspect live XML first
  - choose a nearby known-good template
  - assign the next safe sibling ID
  - insert into `db.xml`
  - reload Fantasy Grounds and verify the record appears
- Structurally valid XML is not enough. Records can still fail in FGU if required gameplay or automation fields are missing or malformed.
- This skill currently works best as a `db.xml structure + insertion workflow` skill, not yet as a complete rules reference for all FGU record types.
- Official automation syntax guidance is useful, but repo behavior still has to be verified in Fantasy Grounds after insertion.
- For this campaign, `item` record IDs appear to need broader uniqueness than just local category uniqueness. Reusing `id-00058` under `"(Potions)"` while `"(Effects)"` already had `id-00058` caused an apparent conflict with `Effect: Disoriented`.

## Risks We Identified

- Editing the wrong file, especially `db.session.*.xml` instead of `db.xml`
- Reusing a sibling `id-xxxxx`
- Reusing an `id-xxxxx` anywhere under the broader `item` namespace may still cause Fantasy Grounds conflicts even if the XML is structurally valid
- Copying the wrong template shape for the record type
- Missing automation fields that make the item appear but not work
- Inserting in the wrong container when a section mixes records and categories
- FGU or other local activity introducing unrelated churn in `db.xml`
- Assuming XML-local ID rules match Fantasy Grounds UI/runtime behavior

## What We Want Next

- Add a self-check layer so the workflow can validate inserts automatically.
- Keep the current skill as the parent workflow skill.
- Expand the skill with record-specific guidance instead of immediately splitting into many separate skills.

## Planned Next Steps

1. Add a short validation reference file for the skill.
2. Create a local validator script, likely PowerShell first, for `item` records.
3. Have the validator check:
   - XML parse success
   - target record exists in `db.xml`
   - uniqueness across the effective `item` namespace, not just local sibling uniqueness
   - presence of required item fields
   - nested child ID collisions in `powers`, `actions`, and similar lists
   - suspicious empty or missing automation fields
   - category placement sanity for mixed-content `item` containers
4. Expand references with more record-specific docs such as:
   - `spell-rules.md`
   - `power-rules.md`
   - `validation-checklist.md`
   - `automation-effect-syntax-rules.md`
5. After the validation workflow feels solid for items, reuse the same approach for spells, abilities, feats, and other record types.

## Suggested Workflow Going Forward

1. Build a draft record from a known-good template.
2. Validate the draft against item rules.
3. Before insertion, confirm the new `item` record ID is safe across the broader `item` section, not only inside one category.
4. Insert into live `db.xml`.
5. Run the validator on `db.xml`.
6. Reload FGU and confirm the item appears and behaves correctly.

## Open Questions

- Which item fields are truly required versus just commonly present in this campaign?
- Which automation syntax patterns should be treated as canonical for this repo?
- Should the validator support only `item` first, or should it be designed from day one to support multiple record types?
- Should `item` ID assignment become globally unique across all direct records and all item subcategories in this repo, even if Fantasy Grounds XML technically permits local reuse?
