# Get Auction Item

```
GET /api/public/auction/{regionCode}/{realmCode}/items/{itemId}
```

Returns all current auction listings for a single item on the specified realm.

## Path Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `regionCode` | string | Region code (`eu`, `us`, `kr`, `tw`) |
| `realmCode` | string | Realm slug (e.g. `draenor`) |
| `itemId` | integer | WoW item ID |

## Example

```bash
curl -s https://ah.seramate.com/api/public/auction/eu/draenor/items/194642
```

## Response

`200 OK` — array of [Auction Item](shared-types.md#auction-item-object) objects.

```json
{
  "data": [
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
      "game_item": {
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
      },
      "item_stats": {
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
    },
    {
      "auction_id": "100002",
      "item_id": 19019,
      "buyout": "4500000",
      "bid": "4000000",
      "quantity": 5,
      "time_left": "SHORT",
      "bonus_lists": [],
      "modifiers": [],
      "context": null,
      "game_item": {
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
      },
      "item_stats": null
    }
  ]
}
```

## Errors

| Status | Error Code | Description |
|--------|------------|-------------|
| 404 | `auction_data_not_found` | No auction snapshot available for this realm |
