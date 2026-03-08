# Search Auctions

```
POST /api/public/auction/{regionCode}/{realmCode}/search
```

Searches auction listings using a natural language query. The query is processed by an AI model to extract item filters (name, quality, item level, slot, price constraints, etc.) and sort criteria, which are then used to find and rank matching items. Price constraints like "under 1000g" or "between 10g and 50g" are supported.

## Path Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `regionCode` | string | Region code (`eu`, `us`, `kr`, `tw`) |
| `realmCode` | string | Realm slug (e.g. `draenor`) |

## Request Body

```json
{
  "naturalQuery": "epic plate helm ilvl 600+",
  "page": 1,
  "per_page": 20
}
```

| Field | Type | Required | Constraints | Description |
|-------|------|----------|-------------|-------------|
| `naturalQuery` | string | yes | 1-200 characters | Natural language search query |
| `page` | integer | no | min: 1, default: 1 | Page number |
| `per_page` | integer | no | min: 1, max: 100 | Results per page. When omitted, the AI determines result count from the query (e.g. "show me 50 bows" → 50 results) |

## Example

```bash
# Search for epic plate helms with item level 600+
curl -s -X POST https://ah.seramate.com/api/public/auction/eu/draenor/search \
  -H 'Content-Type: application/json' \
  -d '{"naturalQuery": "epic plate helm ilvl 600+"}'

# Search for cheap legendary weapons
curl -s -X POST https://ah.seramate.com/api/public/auction/eu/draenor/search \
  -H 'Content-Type: application/json' \
  -d '{"naturalQuery": "legendary weapons sorted by price"}'

# Search with price constraints
curl -s -X POST https://ah.seramate.com/api/public/auction/eu/draenor/search \
  -H 'Content-Type: application/json' \
  -d '{"naturalQuery": "epic swords under 1000g"}'

# Search with price range
curl -s -X POST https://ah.seramate.com/api/public/auction/eu/draenor/search \
  -H 'Content-Type: application/json' \
  -d '{"naturalQuery": "rare gems between 10g and 50g"}'

# Search with explicit pagination
curl -s -X POST https://ah.seramate.com/api/public/auction/eu/draenor/search \
  -H 'Content-Type: application/json' \
  -d '{"naturalQuery": "rare cloth chest from war within", "page": 2, "per_page": 10}'
```

## Response

`200 OK` — array of aggregated item results with pagination metadata, sorted by the inferred sort criteria (e.g. buyout ascending, item level descending, name). Each entry represents one item with aggregated auction data (min buyout, min bid, auction count, total quantity).

```json
{
  "data": [
    {
      "item_id": 12345,
      "min_buyout": "1500000",
      "min_bid": null,
      "auction_count": 5,
      "total_quantity": 12,
      "game_item": { ... },
      "item_stats": { ... }
    }
  ],
  "total_items": 42,
  "total_pages": 3
}
```

When no items match the query:

```json
{
  "data": [],
  "total_items": 0,
  "total_pages": 0
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
