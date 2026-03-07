# Shared Types

## Auction Item Object

Represents a single auction listing enriched with item metadata and calculated stats.

| Field | Type | Description |
|-------|------|-------------|
| `auction_id` | string | Blizzard auction ID |
| `item_id` | integer | WoW item ID |
| `buyout` | string or null | Buyout price in copper. Null for bid-only auctions. |
| `bid` | string or null | Current bid price in copper |
| `quantity` | integer | Number of items in this listing |
| `time_left` | string | Time remaining: `SHORT`, `MEDIUM`, `LONG`, `VERY_LONG` |
| `bonus_lists` | integer[] | Bonus IDs applied to the item (warforged, sockets, etc.) |
| `modifiers` | object[] | Item modifiers, each with `type` (int) and `value` (int) |
| `context` | integer or null | Item context (drop source identifier) |
| `game_item` | [Game Item](#game-item-object) or null | Static item metadata from the game catalog |
| `item_stats` | [Item Stats](#item-stats-object) or null | Calculated stats based on bonus IDs |

```json
{
  "auction_id": "100001",
  "item_id": 19019,
  "buyout": "5000000",
  "bid": null,
  "quantity": 1,
  "time_left": "LONG",
  "bonus_lists": [1502, 6652],
  "modifiers": [{"type": 9, "value": 30}],
  "context": 5,
  "game_item": { ... },
  "item_stats": { ... }
}
```

---

## Game Item Object

Static item metadata from the WoW game catalog.

| Field | Type | Description |
|-------|------|-------------|
| `name` | string | Item display name |
| `quality` | integer | Quality tier (see table below) |
| `item_level` | integer | Base item level |
| `required_level` | integer | Minimum character level to equip |
| `inventory_type` | integer | Equipment slot ID (0 = non-equippable, 1 = head, 5 = chest, etc.) |
| `item_class_id` | integer | Item class (0 = consumable, 1 = container, 2 = weapon, 4 = armor, etc.) |
| `item_subclass_id` | integer | Item subclass within its class |
| `bonding` | integer | Bind type (see table below) |
| `expansion_id` | integer | Expansion ID (see table below) |
| `icon_url` | string or null | URL to the item icon image |
| `allowable_class` | integer | Class restriction bitmask. `-1` = all classes. |

**Quality tiers:**

| Value | Name |
|-------|------|
| 0 | Poor |
| 1 | Common |
| 2 | Uncommon |
| 3 | Rare |
| 4 | Epic |
| 5 | Legendary |
| 6 | Artifact |

**Bonding types:**

| Value | Name |
|-------|------|
| 0 | None |
| 1 | Binds on Pickup |
| 2 | Binds on Equip |
| 3 | Binds on Use |

**Expansion IDs:**

| Value | Expansion |
|-------|-----------|
| 0 | Classic |
| 1 | The Burning Crusade |
| 2 | Wrath of the Lich King |
| 3 | Cataclysm |
| 4 | Mists of Pandaria |
| 5 | Warlords of Draenor |
| 6 | Legion |
| 7 | Battle for Azeroth |
| 8 | Shadowlands |
| 9 | Dragonflight |
| 10 | The War Within |

```json
{
  "name": "Thunderfury, Blessed Blade of the Windseeker",
  "quality": 5,
  "item_level": 80,
  "required_level": 60,
  "inventory_type": 17,
  "item_class_id": 2,
  "item_subclass_id": 7,
  "bonding": 1,
  "expansion_id": 0,
  "icon_url": "https://cdn.example.com/icons/56/inv_sword_39.jpg",
  "allowable_class": 1
}
```

---

## Item Stats Object

Calculated item stats based on the auction's bonus IDs. Present when the item has bonus modifiers that affect stats.

| Field | Type | Description |
|-------|------|-------------|
| `item_level` | integer | Effective item level after bonuses |
| `pvp_item_level` | integer | PvP item level |
| `quality` | integer | Effective quality tier after bonuses |
| `quality_name` | string | Quality display name (e.g. `Epic`, `Legendary`) |
| `socket_count` | integer | Number of gem sockets |
| `stats` | object | Map of stat name to value |

Known stat keys: `stamina`, `intellect`, `agility`, `strength`, `haste`, `critical_strike`, `mastery`, `versatility`.

```json
{
  "item_level": 100,
  "pvp_item_level": 90,
  "quality": 5,
  "quality_name": "Legendary",
  "socket_count": 0,
  "stats": {
    "stamina": 50,
    "haste": 30,
    "critical_strike": 25
  }
}
```
