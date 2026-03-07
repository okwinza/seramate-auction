# Get WoW Token Price

```
GET /api/public/auction/{regionCode}/token
```

Returns the current WoW Token price for a region.

## Path Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `regionCode` | string | Region code (`eu`, `us`, `kr`, `tw`) |

Note: this endpoint does not require a `realmCode` — the token price is region-wide.

## Response

`200 OK`

```json
{
  "data": {
    "price": 3174599
  }
}
```

| Field | Type | Description |
|-------|------|-------------|
| `price` | integer | Current WoW Token price in copper |
