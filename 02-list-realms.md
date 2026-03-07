# List Realms

```
GET /api/public/region/{regionCode}/realms
```

Returns all available realms for a given region. Response is cached until midnight.

## Path Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `regionCode` | string | Region code (`eu`, `us`, `kr`, `tw`) |

## Response

`200 OK`

```json
{
  "data": [
    {
      "id": "550e8400-e29b-41d4-a716-446655440000",
      "name": "Draenor",
      "code": "draenor",
      "lang": "en_GB",
      "blizzard_id": 1403,
      "category": "English"
    }
  ]
}
```

| Field | Type | Description |
|-------|------|-------------|
| `id` | string (UUID) | Internal realm identifier |
| `name` | string | Realm display name |
| `code` | string | Realm slug, used in other endpoint paths |
| `lang` | string | Realm locale (e.g. `en_GB`, `de_DE`) |
| `blizzard_id` | integer | Blizzard's realm ID |
| `category` | string or null | Realm language category (e.g. `English`, `German`) |
