# Search Auctions (Markdown)

```
POST /api/public/auction/{regionCode}/{realmCode}/search/markdown
```

Same data as [Search Auctions](09-search-auctions.md) but formatted as Markdown. Designed for AI agent consumption.

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

`200 OK` — `Content-Type: text/markdown`

Returns Markdown with a section per matching item. See [Get Auction Item (Markdown)](05-get-auction-item-markdown.md) for the output format.

Returns plain text `No auction results found.` if no items match the query.

## Errors

Errors are returned as JSON, not Markdown.

| Status | Error Code | Description |
|--------|------------|-------------|
| 400 | *(varies)* | Query could not be processed |
| 404 | `auction_data_not_found` | No auction snapshot available for this realm |
