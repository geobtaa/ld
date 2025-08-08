# Contexts

{% include-markdown "includes/wip.md" %}

JSON-LD contexts provide mappings between terms used in JSON documents and IRIs. They are essential for creating interoperable linked data.

## Overview

Contexts in this repository define:

- **Term mappings**: Short names for IRIs
- **Type coercions**: Automatic type conversion
- **Language mappings**: Default language for string values
- **Namespace prefixes**: Short prefixes for common vocabularies

## Available Contexts

### Core Context

The core context provides basic mappings for common properties and types:

```json
{
  "@context": {
    "@vocab": "https://schema.org/",
    "dc": "http://purl.org/dc/terms/",
    "geo": "http://www.opengis.net/ont/geosparql#",
    "prov": "http://www.w3.org/ns/prov#"
  }
}
```

### Geospatial Context

Specialized context for geospatial data:

```json
{
  "@context": {
    "@vocab": "https://schema.org/",
    "geo": "http://www.opengis.net/ont/geosparql#",
    "wgs84": "http://www.w3.org/2003/01/geo/wgs84_pos#",
    "geojson": "https://purl.org/geojson/vocab#"
  }
}
```

## Usage

### Including Contexts

```json
{
  "@context": "https://raw.githubusercontent.com/geobtaa/ld/main/contexts/core.jsonld",
  "@type": "Dataset",
  "name": "Example Dataset",
  "description": "A sample dataset"
}
```

### Local Context

For local development, you can reference contexts from the repository:

```json
{
  "@context": "./contexts/core.jsonld",
  "@type": "Dataset",
  "name": "Local Dataset"
}
```