# Get Auction Item List (Markdown)

```
POST /api/public/auction/{regionCode}/{realmCode}/items/markdown
```

Same data as [Get Auction Item List](04-get-auction-item-list.md) but formatted as Markdown. Designed for AI agent consumption. Returns a section per item, each containing an item info table and an auctions table.

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

## Response

`200 OK` — `Content-Type: text/markdown`

Returns Markdown with a section per item. See [Get Auction Item (Markdown)](05-get-auction-item-markdown.md) for the output format.

Returns plain text `No auctions found.` if none of the requested items have active listings.

## Errors

Errors are returned as JSON, not Markdown.

| Status | Error Code | Description |
|--------|------------|-------------|
| 400 | *(validation)* | Invalid or missing `itemIds` |
| 404 | `auction_data_not_found` | No auction snapshot available for this realm |
