# Requests (Endpoints)

JSON-LD context for search requests:

* Future: https://opengeometadata/api/search/1.0/context/request.json  
* Draft PR: [Online here](https://raw.githubusercontent.com/OpenGeoMetadata/opengeometadata.github.io/18896025536dae80b632aa5b059fb001d3d42c56/docs/api/search/1.0/context/request.json)

## Service Document

| Method | Path | Description |
| :---- | :---- | :---- |
| GET | `/service` | Returns API metadata, conformance, contact, and example URLs. |

Example response (abridged):

```json
{
  "@context": "https://gin.btaa.org/ns/service-context.jsonld",
  "id": "https://api.geo.btaa.org/v1/service",
  "type": "Service",
  "label": "GeoBTAA API Service Document",
  "endpoints": {
    "resources": {
      "url": "/resources/{id}",
      "schema": "https://ogm.example.org/schemas/resource.json"
    },
    "search": {
      "url": "/search{?q,page,per_page,sort,callback}",
      "schema": "https://ogm.example.org/schemas/search-results.json"
    },
    "suggestions": {
      "url": "/suggestions{?q}",
      "schema": "https://ogm.example.org/schemas/suggestions.json"
    },
    "validate": {
      "url": "/validate",
      "schema": "https://ogm.example.org/schemas/validate-request.json"
    }
  }
}
```

**TODO** — Create JSON schemas for the response objects

## Resource Retrieval

| Method | Path | Notes |
| :---- | :---- | :---- |
| GET | `/resources/{id}` | Returns a single Aardvark record, wrapped in JSON:API frontmatter. Supports `fields` param for field projection. |

**Parameters**

| Name | Type | Req? | Description |
| :---- | :---- | :---- | :---- |
| `id` | string | ✔️ | Canonical record ID |

## Resource OGM Aardvark Retrieval

| Method | Path | Notes |
| :---- | :---- | :---- |
| GET | `/resources/{id}/ogm` | Returns a single raw Aardvark record. |

**Parameters**

| Name | Type | Req? | Description |
| :---- | :---- | :---- | :---- |
| `id` | string | ✔️ | Canonical record ID |
| `fields` | string (CSV) |  | Subset of fields to include |

## List Resources

| Method | Path | Notes |
| :---- | :---- | :---- |
| GET | `/resources/` | Returns a list of Aardvark records. |

**Parameters**

| Name | Type | Req? | Description |
| :---- | :---- | :---- | :---- |
| `id` | string | ✔️ | Canonical record ID |
| `page` | integer | Current page of results |
| `per_page` | integer | Number of results to return |
| `fields` | string (CSV) |  | Subset of fields to include |

## Search

Supports both GET (simple) and POST (complex) forms.

### GET `/search`

| Parameter | Type | Description |
| :---- | :---- | :---- |
| `q` | string | Full‑text query (default `*:*`). |
| `page` | integer | Current page of results |
| `per_page` | integer | Number of results to return |
| `sort` | string | Sort option (relevance, year\_desc, year\_asc, title\_asc, title\_desc) |
| `callback` | string | JSONP callback name |
| `include_ui` | boolean | Include UI (default true) |
| `fields` | string (CSV) | List of fields to return |
| `facets` | string (CSV) | List of facets to return |
| `filters` | object | Active facet filters |
| `format` | string | Format option (JSON, CSV) |

Example request:

GET /api/v1/search?q=soil+survey\&per\_page=20

### POST `/search`

Accepts a JSON body with the same parameters plus structured filters.

```json
{
  "q": "land cover",
  "filters": {
    "dct_provenance_s": ["Minnesota"],
    "gbl_resourceClass_sm": ["Datasets"]
  },
  "page": 1,
  "per_page": 50,
  "sort": "year_desc"
}
```

## Geospatial Search

Support for geospatial queries:

* Bounding Box  
* Distance-Radius  
* Polygon  
* Shape \+ Relation

### Bounding Box (bbox)

GET /search?q=land+cover\\  
\&filters\[geo\]\[type\]=bbox\\  
\&filters\[geo\]\[field\]=location\\  
\&filters\[geo\]\[top\_left\]\[lat\]=45.1\\  
\&filters\[geo\]\[top\_left\]\[lon\]=-94.0\\  
\&filters\[geo\]\[bottom\_right\]\[lat\]=44.7\\  
\&filters\[geo\]\[bottom\_right\]\[lon\]=-92.9\\  
\&limit=50\\  
\&sort=dct\_temporal\_sm%20desc

POST (`application/json`)

```json
{
  "q": "land cover",
  "filters": {
    "geo": {
      "type": "bbox",
      "field": "location",
      "top_left":     { "lat": 45.1, "lon": -94.0 },
      "bottom_right": { "lat": 44.7, "lon": -92.9 }
    }
  },
  "limit": 50,
  "sort": "dct_temporal_sm desc"
}
```

### Distance-Radius (`distance`)

GET /search?q=land+cover\\  
\&filters\[geo\]\[type\]=distance\\  
\&filters\[geo\]\[field\]=location\\  
\&filters\[geo\]\[center\]\[lat\]=44.98\\  
\&filters\[geo\]\[center\]\[lon\]=-93.27\\  
\&filters\[geo\]\[distance\]=25km\\  
\&limit=50

POST

```json
{
  "q": "land cover",
  "filters": {
    "geo": {
      "type": "distance",
      "field": "location",
      "center":   { "lat": 44.98, "lon": -93.27 },
      "distance": "25km"
    }
  },
  "limit": 50
}
```

### Polygon (`polygon`)

GET /search?q=land+cover\\  
\&filters\[geo\]\[type\]=polygon\\  
\&filters\[geo\]\[field\]=location\\  
\&filters\[geo\]\[points\]\[0\]\[lat\]=44.9\\  
\&filters\[geo\]\[points\]\[0\]\[lon\]=-93.4\\  
\&filters\[geo\]\[points\]\[1\]\[lat\]=45.2\\  
\&filters\[geo\]\[points\]\[1\]\[lon\]=-93.2\\  
\&filters\[geo\]\[points\]\[2\]\[lat\]=45.0\\  
\&filters\[geo\]\[points\]\[2\]\[lon\]=-92.8

(Add more `points[n]` pairs for polygons with \>3 vertices.)

POST

```json
{
  "q": "land cover",
  "filters": {
    "geo": {
      "type": "polygon",
      "field": "location",
      "points": [
        { "lat": 44.9, "lon": -93.4 },
        { "lat": 45.2, "lon": -93.2 },
        { "lat": 45.0, "lon": -92.8 }
      ]
    }
  }
}
```

### Shape (`shape` \+ relation)

Relation options:

* intersects  
* disjoint  
* within  
* contains

GET /search?q=land+cover\\  
\&filters\[geo\]\[type\]=shape\\  
\&filters\[geo\]\[field\]=location\\  
\&filters\[geo\]\[relation\]=within\\  
\&filters\[geo\]\[shape\]\[type\]=envelope\\  
\&filters\[geo\]\[shape\]\[coordinates\]\[0\]\[0\]=-94\\  
\&filters\[geo\]\[shape\]\[coordinates\]\[0\]\[1\]=46\\  
\&filters\[geo\]\[shape\]\[coordinates\]\[1\]\[0\]=-92\\  
\&filters\[geo\]\[shape\]\[coordinates\]\[1\]\[1\]=44

(Here the shape is a GeoJSON-style envelope; any GeoJSON geometry works.)

POST

```json
{
  "q": "land cover",
  "filters": {
    "geo": {
      "type": "shape",
      "field": "location",
      "relation": "within",
      "shape": {
        "type": "envelope",
        "coordinates": [[-94, 46], [-92, 44]]
      }
    }
  }
}
```

## Suggestions Endpoint

Endpoint for autocomplete search suggestions.

### GET /suggestions?q=minn**

| Parameter | Type | Description |
| :---- | :---- | :---- |
| `q` | string | Full‑text query (default `*:*`). |
| `callback` | string | JSONP callback name |

## Validation Endpoint

**TODO** — How can this validate CSVs via Table Schema

This endpoint allows clients to POST a single metadata record (as a JSON object) and receive a validation report indicating whether it conforms to the OpenGeoMetadata Aardvark schema.

| Method | Path | Description |
| :---- | ----- | ----- |
| POST | /validate | Validate a single Aardvark JSON record |

### Request Body

```json
{
  "data": {
    "type": "resource",
    "attributes": {
      "id": "stanford-abc123",
      "dct_title_s": "Sample Map",
      "gbl_resourceClass_sm": ["Maps"],
      "dct_accessRights_s": "Public",
      "gbl_mdVersion_s": "Aardvark",
      "gbl_mdModified_dt": "2025-07-20T18:43:00Z"
      // ... other fields ...
    }
  }
}
```

* The body MUST be a single JSON object using type: "resource" and an attributes map.  
* The record MUST be structured according to the Aardvark profile defined at: [https://opengeometadata.org/schema/geoblacklight-schema-aardvark.json](https://opengeometadata.org/schema/geoblacklight-schema-aardvark.json)

### Response

If the record is valid:

```json
{
  "valid": true,
  "errors": [],
  "warnings": [],
  "profile": [
    "https://opengeometadata.org/profile/aardvark",
    "https://opengeometadata.org/profile/mcp/validate"
  ]
}
```

}

If the record is invalid:

```json
{
  "valid": false,
  "errors": [
    {
      "field": "dct_title_s",
      "message": "This field is required and must be a string."
    },
    {
      "field": "gbl_mdVersion_s",
      "message": "Value must be 'Aardvark'."
    }
  ],
  "warnings": [],
  "profile": [
    "https://opengeometadata.org/profile/aardvark",
    "https://opengeometadata.org/profile/mcp/validate"
  ]
}
```

### Notes

* This endpoint is non-mutating — it does not store or alter the record.  
* It is useful for QA tools, CI pipelines, and metadata editors.  
* The server SHOULD use a strict JSON Schema validator and MAY support additional lint rules or MCP profiles.