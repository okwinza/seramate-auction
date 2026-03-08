# Get Auction Item List

```
POST /api/public/auction/{regionCode}/{realmCode}/items
```

Returns auction listings for multiple items at once. Duplicate item IDs are deduplicated.

## Path Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `regionCode` | string | Region code (`eu`, `us`, `kr`, `tw`) |
| `realmCode` | string | Realm slug (e.g. `draenor`) |

## Request Body

```json
{
  "itemIds": [19019, 72120, 52078]
}
```

| Field | Type | Required | Constraints |
|-------|------|----------|-------------|
| `itemIds` | integer[] | yes | 1-100 items, all values must be integers |

## Example

```bash
curl -s -X POST https://ah.seramate.com/api/public/auction/eu/draenor/items \
  -H 'Content-Type: application/json' \
  -d '{"itemIds": [19019, 72120, 52078]}'
```

## Response

`200 OK` — array of [Auction Item](shared-types.md#auction-item-object) objects. Same structure as [Get Auction Item](03-get-auction-item.md), with listings for all requested items combined.

## Errors

| Status | Error Code | Description |
|--------|------------|-------------|
| 400 | *(validation)* | Invalid or missing `itemIds` |
| 404 | `auction_data_not_found` | No auction snapshot available for this realm |

```json
{
  "code": 400,
  "message": "\"itemIds\" must not be empty."
}
```
