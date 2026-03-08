# Get Auction Item (Markdown)

```
GET /api/public/auction/{regionCode}/{realmCode}/items/{itemId}/markdown
```

Same data as [Get Auction Item](03-get-auction-item.md) but formatted as Markdown. Designed for AI agent consumption.

## Path Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `regionCode` | string | Region code (`eu`, `us`, `kr`, `tw`) |
| `realmCode` | string | Realm slug (e.g. `draenor`) |
| `itemId` | integer | WoW item ID |

## Example

```bash
curl -s https://ah.seramate.com/api/public/auction/eu/draenor/items/194642/markdown
```

## Response

`200 OK` — `Content-Type: text/markdown`

```markdown
## Thunderfury, Blessed Blade of the Windseeker

| Field | Value |
|---|---|
| Item ID | 19019 |
| Quality | Legendary |
| Base Item Level | 80 |
| Required Level | 60 |
| Slot | Two-Hand |
| Type | Weapon > One-Handed Sword |
| Usable By | Warrior |
| Bonding | Binds on Pickup |
| Expansion | Classic |

### Auctions (2)

| Buyout | Qty | Listings | iLvl | Quality | PvP iLvl | Sockets | Stats |
|---|---|---|---|---|---|---|---|
| 500g | 1 | 1 | 100 | Legendary | 100 | 0 | Sta 50, Haste 30, Crit 25 |
| 450g | 5 | 1 | 80 | Legendary | 80 | 1 | Sta 40, Vers 20 |
```

Returns plain text `No auctions found.` if the item has no active listings.

## Errors

Errors are returned as JSON, not Markdown.

| Status | Error Code | Description |
|--------|------------|-------------|
| 404 | `auction_data_not_found` | No auction snapshot available for this realm |
