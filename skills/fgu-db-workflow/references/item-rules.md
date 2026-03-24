# Item Rules

These notes capture the current `item` behavior observed in this repo.

## Item Container Behavior

The `item` section is mixed content. It contains both:

- direct record containers such as `<id-00011>...</id-00011>`
- nested category containers such as `<category name="(Potions)">...</category>`

Do not flatten this into a simple list of item records.

## Item Record Identity

The outer `id-xxxxx` node is the item's record container and local database key inside its parent container.

Example:

```xml
<id-00011>
  <name type="string">Potion Bandolier(Tier I-IV)</name>
</id-00011>
```

- `id-00011` is the internal record node
- `<name>` is the human-facing label

## Nested Child IDs

Items can contain nested child collections, for example:

- `powers`
- `actions`
- `spells`

Nested `id-xxxxx` values are local to their parent container.

Example:

```xml
<id-00011>
  <powers>
    <id-00001>
      <actions>
        <id-00001>
        </id-00001>
      </actions>
    </id-00001>
  </powers>
</id-00011>
```

Rules:

- the item's outer record ID does not reset to `id-00001` in an existing `item` list
- a brand-new nested list often begins at `id-00001`
- copied child blocks may need renumbering if they collide with existing siblings

## Rich Item Example

`Potion Bandolier(Tier I-IV)` is a good stress-test record because it includes:

- many normal item fields
- large `formattedtext` description content
- repeated `holder` nodes
- nested `powers`
- nested `actions` under `powers`

Use a record like this to validate round-trip safety for the `item` category.
