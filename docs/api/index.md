# GeoBTAA API Specification

**Version:** 0.1.0-pre-alpha   **Status:** *DRAFT*   **Release Date:** 2025‑08‑04

## Editors

* Eric Larson, Big Ten Academic Alliance  
* Karen Majewicz, Big Ten Academic Alliance  

Copyright © 2025 Editors and Contributors. Published by BTAA GIN under the [CC-BY license](https://creativecommons.org/licenses/by/4.0/), see disclaimer.

---

## TODOs

* SEE: [DRAFT OpenGeoMetadata API Pull Request](https://github.com/OpenGeoMetadata/opengeometadata.github.io/pull/114)  
  * OpenGeoMetadata Website  
    * API documentation  
    * JSON-LD profiles  
* Advanced Search  
  * Field level searching  
* Sanity check MCP section

---

## Introduction

The **GeoBTAA API** is an OpenGeoMetadata API-compliant, read‑only, web service for programmatically accessing, searching, and retrieving metadata records that conform to the BTAA GIN’s GeoBTAA extended-OGM Aardvark schema ([opengeometadata.org](http://opengeometadata.org) \+ [https://gin.btaa.org/metadata/b1g-custom-elements](https://gin.btaa.org/metadata/b1g-custom-elements)). The API is designed to be an efficient backend, powering search and geospatial discovery, for any frontend technology. 

In addition to structured metadata retrieval, the API can drive user interface components — such as field hints, thumbnails, citations, and viewer configurations — that support search, web service previews, and other interactive features within geospatial discovery applications.

This specification deliberately echoes the style and structure of the IIIF specifications ([iiif.io](https://iiif.io/api/image/3.0/?utm_source=chatgpt.com)), providing:

* A small, RESTful surface area with predictable, cache‑friendly URLs  
* Explicit parameter semantics  
* Normative requirements using **MUST**, **SHOULD**, **MAY** as defined by [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119)

The goal of this specification is to enable consistent client and server implementations across the OGM community.

## Scope

* **In scope** – Retrieval of individual resources, list endpoints, full‑text and spatial search, simple authentication, usage limits.  
* **Out of scope** – Write operations (create/update/delete), bulk harvesting, or authentication flows beyond API keys (e.g. OAuth 2).

## Audience

* BTAA GIN Member Libraries  
* Client developers (e.g. FastAPI-based geoportals, desktop GIS plugins)  
* Researchers automating metadata discovery

## Change Log

| Version | Date | Notes |
| :---- | :---- | :---- |
| 0.1.0 | 2025‑07‑22 | Initial draft. |

## Implementation Notes

* A reference implementation in FastAPI is available at [https://github.com/geobtaa/ogm-api](https://github.com/geobtaa/ogm-api).

* Example code snippets are provided in the repository README.

* JSON‑LD clients may apply the [OGM Aardvark context](https://opengeometadata/context/aardvark-v1.jsonld) ([https://opengeometadata/context/aardvark-v1.jsonld](https://opengeometadata/context/aardvark-v1.jsonld)) to treat field names as compact IRIs.

## Acknowledgements

This specification borrows heavily from the structure and editorial approach of the IIIF community ([iiif.io](https://iiif.io/api/image/3.0/?utm_source=chatgpt.com)) and benefits from prior work by the GeoBlacklight and OpenGeoMetadata communities.