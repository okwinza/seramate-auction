# Seramate Auction House API

Base URL: `https://ah.seramate.com`

## Conventions

- All JSON responses use `Content-Type: application/json`.
- Markdown endpoints use `Content-Type: text/markdown`.
- Monetary values (buyout, bid, prices) are strings representing **copper** (1 gold = 10,000 copper).
- Error responses always return JSON, even on Markdown endpoints.

## Common Path Parameters

| Parameter | Type | Description | Example |
|-----------|------|-------------|---------|
| `regionCode` | string | Game region code | `eu`, `us`, `kr`, `tw` |
| `realmCode` | string | Realm slug | `draenor`, `ragnaros` |
| `itemId` | integer | WoW game item ID | `19019` |

## Endpoints

| # | Method | Path | Description |
|---|--------|------|-------------|
| 1 | `GET` | [`/`](01-health-check.md) | Health check |
| 2 | `GET` | [`/api/public/region/{regionCode}/realms`](02-list-realms.md) | List realms for a region |
| 3 | `GET` | [`/api/public/auction/{regionCode}/{realmCode}/items/{itemId}`](03-get-auction-item.md) | Get auctions for a single item |
| 4 | `POST` | [`/api/public/auction/{regionCode}/{realmCode}/items`](04-get-auction-item-list.md) | Get auctions for multiple items |
| 5 | `GET` | [`/api/public/auction/{regionCode}/{realmCode}/items/{itemId}/markdown`](05-get-auction-item-markdown.md) | Get auctions for a single item (Markdown) |
| 6 | `POST` | [`/api/public/auction/{regionCode}/{realmCode}/items/markdown`](06-get-auction-item-list-markdown.md) | Get auctions for multiple items (Markdown) |
| 7 | `POST` | [`/api/public/auction/{regionCode}/{realmCode}/prices`](07-get-auction-prices.md) | Get minimum buyout prices |
| 8 | `GET` | [`/api/public/auction/{regionCode}/token`](08-get-token-price.md) | Get WoW Token price |
| 9 | `POST` | [`/api/public/auction/{regionCode}/{realmCode}/search`](09-search-auctions.md) | Natural language auction search |
| 10 | `POST` | [`/api/public/auction/{regionCode}/{realmCode}/search/markdown`](10-search-auctions-markdown.md) | Natural language auction search (Markdown) |

## Shared Types

Reusable response objects are documented in [shared-types.md](shared-types.md):

- [Auction Item Object](shared-types.md#auction-item-object)
- [Game Item Object](shared-types.md#game-item-object)
- [Item Stats Object](shared-types.md#item-stats-object)

## Error Responses

All error responses return a JSON body:

| HTTP Status | Error Code | When |
|-------------|------------|------|
| 400 | *(validation)* | Request body failed validation |
| 400 | *(varies)* | Natural language query could not be processed |
| 404 | `auction_data_not_found` | No auction snapshot available for the realm |
| 404 | `realm_not_found` | The specified realm does not exist |

Validation errors:

```json
{
  "code": 400,
  "message": "\"itemIds\" must not be empty."
}
```

Domain errors:

```json
{
  "error_code": "auction_data_not_found",
  "message": "No auction data available for this realm."
}
```
