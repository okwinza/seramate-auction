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
  "naturalQuery": "epic plate helm ilvl 600+",
  "page": 1,
  "per_page": 20
}
```

| Field | Type | Required | Constraints | Description |
|-------|------|----------|-------------|-------------|
| `naturalQuery` | string | yes | 1-200 characters | Natural language search query |
| `page` | integer | no | min: 1, default: 1 | Page number |
| `per_page` | integer | no | min: 1, max: 100 | Results per page. When omitted, the AI determines result count from the query |

## Example

```bash
curl -s -X POST https://ah.seramate.com/api/public/auction/eu/draenor/search/markdown \
  -H 'Content-Type: application/json' \
  -d '{"naturalQuery": "epic swords under 1000g"}'
```

## Response

`200 OK` — `Content-Type: text/markdown`

Returns Markdown with a section per matching item. See [Get Auction Item (Markdown)](05-get-auction-item-markdown.md) for the output format.

A pagination footer is appended at the end of the response:

```
---
Page 1 of 5 (42 items total)
```

Returns plain text `No auction results found.` if no items match the query or the requested page is beyond results.

## Errors

Errors are returned as JSON, not Markdown.

| Status | Error Code | Description |
|--------|------------|-------------|
| 400 | *(varies)* | Query could not be processed |
| 404 | `auction_data_not_found` | No auction snapshot available for this realm |
