# Model Context Protocol (MCP)

{% include-markdown "includes/wip.md" %}

TODO — Explore FastAPI’s MCP add-on for conformity

The OpenGeoMetadata API supports the [Model Context Protocol (MCP)](https://modelcontextprotocol.io/specification/2025-06-18), a formal specification for declaring the processing and behavioral context of an API response. MCP enables generic clients, validators, and AI agents to understand how to interpret metadata records and response payloads in a consistent, machine-readable way.

## Usage

API responses MAY declare one or more MCP \`profile\` URIs to advertise behavior:

| {"jsonapi": {  "version": "1.1",  "profile": \[    "https://opengeometadata.org/profile/aardvark",    "https://opengeometadata.org/profile/ui-hints",    "https://opengeometadata.org/profile/mcp/search"  \]} |
| :---- |

## Profile URIs

Each URI in the profile array MUST resolve to a valid MCP document, which includes:

* @context: MUST include the MCP context (https://modelcontextprotocol.io/context/v1.jsonld)  
* @type: SHOULD be ModelContextProfile  
* title, description, appliesTo: for human/machine interpretation  
* features: optional keys describing supported behaviors, fields, or UI expectations

## Example MCP Profile (abridged)

| {  "@context": "https://modelcontextprotocol.io/context/v1.jsonld",  "@type": "ModelContextProfile",  "id": "https://opengeometadata.org/profile/mcp/search",  "title": "OGM Search Results Profile",  "description": "Describes the structure and interpretation of search results.",  "appliesTo": "https://opengeometadata.org/api/v1/search",  "features": {    "search": {      "supportsGeoFilters": true,      "maxResults": 1000,      "defaultSort": "relevance"    },    "ui": {      "viewer": true,      "facets": true,      "pagination": true    }  }} |
| :---- |

## Benefits

* Allows automated agents to reason about what’s returned  
* Enables consistent UI rendering and schema interpretation  
* Provides potential future extensibility without API versioning
