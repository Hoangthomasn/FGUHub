# db.xml Structure Notes

These notes are specific to the current repo's `db.xml`.

## Root

The file uses a `<root>` document element with attributes such as:

- `version`
- `dataversion`
- `release`

These must be preserved during rebuild.

## Current Top-Level Sections

Observed top-level child nodes include:

- `aggro_manager`
- `background`
- `battle`
- `battlerandom`
- `calendar`
- `charsheet`
- `class`
- `class_specialization`
- `class_spell_list`
- `combattracker`
- `combattracker_groups`
- `currencies`
- `DB`
- `effects`
- `encounter`
- `extensionvcupgrades`
- `feat`
- `forge`
- `image`
- `item`
- `itemtemplate`
- `languages`
- `library`
- `location`
- `MKshops`
- `modifiers`
- `motd`
- `notes`
- `npc`
- `options`
- `partysheet`
- `picture`
- `portals`
- `quest`
- `race`
- `reference`
- `requestsheet`
- `RRdirty`
- `settings`
- `shops`
- `skill`
- `soundset`
- `spell`
- `spellbooks`
- `storytemplate`
- `tableimport`
- `tables`
- `temp`
- `treasureparcels`
- `vehicle`

## Category Guidance

Content-like sections commonly include:

- `item`
- `npc`
- `spell`
- `feat`
- `background`
- `class`
- `class_specialization`
- `race`
- `languages`
- `reference`
- `tables`
- `shops`
- `treasureparcels`
- `vehicle`

Campaign/system sections commonly include:

- `charsheet`
- `combattracker`
- `battle`
- `calendar`
- `options`
- `settings`
- `effects`
- `partysheet`
- `notes`
- `quest`

This classification is for workflow convenience only. Reassembly must still preserve the actual source order from `db.xml`.
