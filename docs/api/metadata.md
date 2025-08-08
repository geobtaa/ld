# Metadata

{% include-markdown "includes/wip.md" %}

## OGM Aardvark

[OGM Aardvark](https://opengeometadata.org/ogm-aardvark/) ([https://opengeometadata.org/ogm-aardvark](https://opengeometadata.org/ogm-aardvark)) is a lightweight metadata profile for geospatial discovery. Every resource is a single JSON object that **MUST** include the following required properties:

| Field | Type | Description |
| :---- | :---- | :---- |
| `id` | string | Stable identifier (slug or UUID). |
| `dct_title_s` | string | Human‑readable title. |
| `dct_accessRights_s` | string | Only one of two values are allowed: Public or Restricted. |
| `gbl_resourceClass_sm` | array of strings | Provides a top level set of categories for classifying the resource. |
| `gbl_mdModified_dt` | string (date‑time) | Last modified timestamp. |
| `gbl_mdVersion_s` | string | MUST be `Aardvark`. |
| [Full OGM Aardvark Schema Definition](https://opengeometadata.org/ogm-aardvark/) |  |  |

## GeoBTAA Metadata Profile 

Every resource **MUST** include the following required BTAA properties:

| Field | Type | Description |
| :---- | :---- | :---- |
| `b1g_code_s` | string | To group records based upon their source. |
| `b1g_dct_accrualMethod_s` | string | To describe how the record was obtained. |
| `b1g_dateAccessioned_s` | string | To store the date a record was harvested. |
| `b1g_publication_state_s` | string | To communicate if the resource is public or hidden. |
| `b1g_language_sm` | string | To display the spelled out string (in English) of a language code to users. |
| [Full BTAA Extension Schema Definition](https://gin.btaa.org/metadata/b1g-custom-elements/) |  |  |

## OGM+GeoBTAA

Combined OGM+GeoBTAA required attributes:

| Field | Type | Description |
| :---- | :---- | :---- |
| `id` | string | Stable identifier (slug or UUID). |
| `dct_title_s` | string | Human‑readable title. |
| `dct_accessRights_s` | string | Only one of two values are allowed: Public or Restricted. |
| `gbl_resourceClass_sm` | array of strings | Provides a top level set of categories for classifying the resource. |
| `gbl_mdModified_dt` | string (date‑time) | Last modified timestamp. |
| `gbl_mdVersion_s` | string | MUST be `Aardvark`. |
| `b1g_code_s` | string | To group records based upon their source |
| `b1g_dct_accrualMethod_s` | string | To describe how the record was obtained. |
| `b1g_dateAccessioned_s` | string | To store the date a record was harvested. |
| `b1g_publication_state_s` | string | To communicate if the resource is public or hidden. |
| `b1g_language_sm` | string | To display the spelled out string (in English) of a language code to users. |

The obligation for all other fields defined in the canonical Aardvark schema is **MAY**.

## JSON Schema

**TODO: JSON Schema for OGM+GeoBTAA**

JSON Schema file for OGM+GeoBTAA resources is maintained at: [https://opengeometadata.org/schema/geoblacklight-schema-aardvark.json](https://opengeometadata.org/schema/geoblacklight-schema-aardvark.json)

## JSON-LD Context

**TODO: Initial implementation within WIP PR on GIN website:**

JSON-LD context for OGM+BTAA Aardvark records: [DRAFT PR](https://raw.githubusercontent.com/OpenGeoMetadata/opengeometadata.github.io/18896025536dae80b632aa5b059fb001d3d42c56/docs/context/aardvark.json)

## CSV

OGM+GeoBTAA also has a tabular CSV expression with an [Open Knowledge Foundation](https://okfn.org/en/) \> [Frictionless Data](https://frictionlessdata.io/) \> [Table Schema](https://datapackage.org/standard/table-schema/) schema definition. Unlike OGM+GeoBTAA Aardvark JSON, OGM+GeoBTAA Aardvark CSV is comprised of two files:

1. Primary — The primary Aardvark metadata elements (primary.csv)  
2. Distributions — The dct\_reference\_s elements (distributions.csv)

## Table Schema

### CSV File Examples

**TODO: Create examples**  
These example CSV files use the GeoBlacklight fixture set.

* Primary — [gbl\_fixtures\_primary.csv](https://github.com/OpenGeoMetadata/opengeometadata.github.io/blob/api/docs/schema/gbl_fixtures_primary.csv)  
* Distributions — [gbl\_fixtures\_distributions.csv](https://github.com/OpenGeoMetadata/opengeometadata.github.io/blob/api/docs/schema/gbl_fixtures_distributions.csv)

### Table Schema Files

**TODO: Create schema files**  
These files can be used to validate the CSV examples against our CSV schema.

* Primary — [ogm\_aardvark\_primary.schema.json](https://github.com/OpenGeoMetadata/opengeometadata.github.io/blob/api/docs/schema/ogm_aardvark_primary.schema.json)  
* Distributions — [ogm\_aardvark\_distributions.schema.json](https://github.com/OpenGeoMetadata/opengeometadata.github.io/blob/api/docs/schema/ogm_aardvark_distributions.schema.json)