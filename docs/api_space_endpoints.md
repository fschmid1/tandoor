# Space-Specific API Endpoints

This document describes the new API endpoints that allow admin users to retrieve foods, units, and keywords filtered by space ID.

## Overview

These endpoints are designed for admin users who need to access data from specific spaces. They provide a way to retrieve all items of a particular type (foods, units, or keywords) that belong to a specific space.

## Authentication

All endpoints require admin privileges. Users must have the 'admin' group permission to access these endpoints.

## Endpoints

### Get Keywords by Space

**Endpoint:** `GET /api/keyword/by_space/`

**Parameters:**

- `space_id` (required): The ID of the space to filter keywords by

**Example Request:**

```bash
curl -X GET "https://your-domain.com/api/keyword/by_space/?space_id=1" \
  -H "Authorization: Token your-token-here"
```

**Response:**

```json
[
  {
    "id": 1,
    "name": "Italian",
    "description": "Italian cuisine",
    "image": null,
    "parent": null,
    "numchild": 0,
    "numrecipe": 5,
    "created_at": "2023-01-01T00:00:00Z",
    "updated_at": "2023-01-01T00:00:00Z",
    "full_name": "Italian",
    "space": 1
  }
]
```

### Get Units by Space

**Endpoint:** `GET /api/unit/by_space/`

**Parameters:**

- `space_id` (required): The ID of the space to filter units by

**Example Request:**

```bash
curl -X GET "https://your-domain.com/api/unit/by_space/?space_id=1" \
  -H "Authorization: Token your-token-here"
```

**Response:**

```json
[
  {
    "id": 1,
    "name": "gram",
    "plural_name": "grams",
    "description": "Metric weight unit",
    "base_unit": "g",
    "numrecipe": 10,
    "image": null,
    "open_data_slug": "gram",
    "space": 1
  }
]
```

### Get Foods by Space

**Endpoint:** `GET /api/food/by_space/`

**Parameters:**

- `space_id` (required): The ID of the space to filter foods by

**Example Request:**

```bash
curl -X GET "https://your-domain.com/api/food/by_space/?space_id=1" \
  -H "Authorization: Token your-token-here"
```

**Response:**

```json
[
  {
    "id": 1,
    "name": "tomato",
    "plural_name": "tomatoes",
    "description": "Fresh tomatoes",
    "shopping": false,
    "recipe": null,
    "inherit_fields": [],
    "child_inherit_fields": [],
    "food_onhand": false,
    "substitute_onhand": false,
    "substitute": [],
    "parent": null,
    "properties": [],
    "properties_food_unit": null,
    "properties_food_amount": null,
    "supermarket_category": null,
    "image": null,
    "numchild": 0,
    "numrecipe": 3,
    "full_name": "tomato",
    "ignore_shopping": false,
    "substitute_siblings": false,
    "substitute_children": false,
    "open_data_slug": "tomato",
    "space": 1
  }
]
```

## Error Responses

### Unauthorized (403)

```json
{
  "detail": "Only admin users can access this endpoint"
}
```

### Bad Request (400)

```json
{
  "space_id": "space_id parameter is required"
}
```

or

```json
{
  "space_id": "space_id must be a valid integer"
}
```

## Usage Notes

1. **Admin Only**: These endpoints are restricted to users with admin privileges
2. **No Pagination**: Results are returned without pagination for easier processing
3. **Space Filtering**: All results are filtered by the specified space ID
4. **Full Data**: Returns complete object data including all related fields

## Use Cases

- **Data Migration**: Moving data between spaces
- **Space Management**: Admin tools for managing multiple spaces
- **Data Analysis**: Analyzing data across different spaces
- **Backup/Restore**: Exporting data from specific spaces

## Security Considerations

- Only admin users can access these endpoints
- The space ID parameter is validated to ensure it's a valid integer
- Results are filtered by the specified space ID to prevent data leakage
