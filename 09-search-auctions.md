# Search Auctions

```
POST /api/public/auction/{regionCode}/{realmCode}/search
```

Searches auction listings using a natural language query. The query is processed by an AI model to extract item filters (name, quality, item level, slot, etc.) and sort criteria, which are then used to find and rank matching items.

## Path Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `regionCode` | string | Region code (`eu`, `us`, `kr`, `tw`) |
| `realmCode` | string | Realm slug (e.g. `draenor`) |

## Request Body

```json
{
  "naturalQuery": "epic plate helm ilvl 600+"
}
```

| Field | Type | Required | Constraints |
|-------|------|----------|-------------|
| `naturalQuery` | string | yes | 1-200 characters |

## Response

`200 OK` — array of [Auction Item](shared-types.md#auction-item-object) objects, sorted by the inferred sort criteria (e.g. buyout ascending, item level descending, name).

```json
{
  "data": [
    {
      "auction_id": "200001",
      "item_id": 12345,
      "buyout": "1500000",
      "bid": null,
      "quantity": 1,
      "time_left": "LONG",
      "bonus_lists": [],
      "modifiers": [],
      "context": null,
      "game_item": { ... },
      "item_stats": { ... }
    }
  ]
}
```

When no items match the query:

```json
{
  "data": []
}
```

## Errors

| Status | Error Code | Description |
|--------|------------|-------------|
| 400 | *(varies)* | Query could not be processed |
| 404 | `auction_data_not_found` | No auction snapshot available for this realm |

```json
{
  "error_code": "natural_query_parse_error",
  "message": "Could not understand the search query."
}
```
