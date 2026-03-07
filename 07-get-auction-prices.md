# Get Auction Prices

```
POST /api/public/auction/{regionCode}/{realmCode}/prices
```

Returns the minimum buyout price for each requested item. Useful for quick price lookups without full auction details.

## Path Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `regionCode` | string | Region code (`eu`, `us`, `kr`, `tw`) |
| `realmCode` | string | Realm slug (e.g. `draenor`) |

## Request Body

```json
{
  "itemIds": [19019, 72120]
}
```

| Field | Type | Required | Constraints |
|-------|------|----------|-------------|
| `itemIds` | integer[] | yes | 1-100 items, all values must be integers |

## Response

`200 OK`

```json
{
  "data": {
    "prices": {
      "19019": "4500000",
      "72120": "120000"
    }
  }
}
```

| Field | Type | Description |
|-------|------|-------------|
| `prices` | object | Map of item ID (string key) to minimum buyout in copper (string value). Items with no auctions are omitted. |

When none of the requested items have auctions:

```json
{
  "data": {
    "prices": {}
  }
}
```

## Errors

| Status | Error Code | Description |
|--------|------------|-------------|
| 400 | *(validation)* | Invalid or missing `itemIds` |
| 404 | `auction_data_not_found` | No auction snapshot available for this realm |
