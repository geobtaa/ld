# Schemas

JSON Schemas provide structural validation for linked data, ensuring data quality and consistency across the GeoBTAA ecosystem.

## Overview

Schemas in this repository define:

- **Data structure**: Required and optional fields
- **Data types**: String, number, object, array constraints
- **Value constraints**: Enumerations, ranges, patterns
- **Relationships**: References between different data types
- **Validation rules**: Business logic and constraints

## Available Schemas

### GeoBTAA OGM Aardvark Resource Record

**File**: `schemas/resource.json`

Validates OpenGeoMetadata Aardvark schema fields with GeoBTAA B1G custom elements for geospatial resource records.

**Key Features**:
- OpenGeoMetadata Aardvark compliance
- GeoBTAA B1G custom extensions
- Dublin Core metadata validation
- Spatial and temporal coverage validation
- Access rights and licensing validation
- Provenance and administrative metadata

**Required Fields**:
- `id` - Resource identifier
- `gbl_mdVersion_s` - Metadata version (must be "Aardvark")
- `schema_provider_s` - Schema provider
- `dct_title_s` - Resource title
- `dct_description_sm` - Resource descriptions
- `dct_language_sm` - Languages
- `dct_accessRights_s` - Access rights ("Public" or "Restricted")
- `dct_license_sm` - License URIs
- `b1g_code_s` - GeoBTAA custom code
- `b1g_dct_accrualMethod_s` - Accrual method
- `b1g_dateAccessioned_s` - Accession date
- `b1g_publication_state_s` - Publication state
- `b1g_language_sm` - B1G languages

**Example Usage**:

```json
{
  "id": "example-resource-001",
  "gbl_mdVersion_s": "Aardvark",
  "schema_provider_s": "GeoBTAA",
  "dct_title_s": "Midwest Population Density Data",
  "dct_description_sm": ["Population density data for the Midwest United States"],
  "dct_language_sm": ["en"],
  "dct_accessRights_s": "Public",
  "dct_license_sm": ["https://creativecommons.org/licenses/by/4.0/"],
  "b1g_code_s": "MIDWEST_POP_2020",
  "b1g_dct_accrualMethod_s": "manual",
  "b1g_dateAccessioned_s": "2024-01-15",
  "b1g_publication_state_s": "published",
  "b1g_language_sm": ["en"],
  "dct_spatial_sm": ["Midwest United States"],
  "dcat_bbox": "-104.0,36.0,-80.0,49.0",
  "dcat_centroid": "-92.0,42.5"
}
```

## Validation

### Command Line Validation

```bash
# Validate schema files themselves
python scripts/validate_schema.py --validate-schemas

# Validate data against a specific schema
python scripts/validate_schema.py --schema schemas/dataset.json --data data/example.json

# Using jsonschema CLI
pip install jsonschema
jsonschema -i data/dataset.json schemas/dataset.json
```

### Programmatic Validation

```python
import json
from jsonschema import validate, ValidationError

def validate_dataset(data):
    """Validate dataset against GeoBTAA schema."""
    with open('schemas/dataset.json') as f:
        schema = json.load(f)
    
    try:
        validate(instance=data, schema=schema)
        return True, None
    except ValidationError as e:
        return False, e.message

# Usage
data = {
    "@context": "https://raw.githubusercontent.com/geobtaa/ld/main/contexts/core.jsonld",
    "@type": "Dataset",
    "name": "Test Dataset",
    "description": "A test dataset"
}

is_valid, error = validate_dataset(data)
if is_valid:
    print("✓ Dataset is valid")
else:
    print(f"✗ Validation error: {error}")
```

### Integration with JSON-LD

Schemas work alongside JSON-LD contexts to provide both structural validation and semantic meaning:

```json
{
  "$schema": "https://geobtaa.org/schemas/dataset.json",
  "@context": "https://raw.githubusercontent.com/geobtaa/ld/main/contexts/geospatial.jsonld",
  "@type": "Dataset",
  "name": "Validated Dataset",
  "description": "This dataset passes both schema and context validation"
}
```

## Schema Development

### Creating New Schemas

1. **Follow JSON Schema Draft 7** standards
2. **Use descriptive `$id`** URIs for canonical identification
3. **Include comprehensive descriptions** for all properties
4. **Test with sample data** to ensure validation works correctly
5. **Document all constraints** and business rules

### Schema Structure

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "$id": "https://geobtaa.org/schemas/example.json",
  "title": "Example Schema",
  "description": "Description of what this schema validates",
  "type": "object",
  "required": ["field1", "field2"],
  "properties": {
    "field1": {
      "type": "string",
      "description": "Description of field1",
      "minLength": 1
    },
    "field2": {
      "type": "number",
      "description": "Description of field2",
      "minimum": 0
    }
  },
  "additionalProperties": false
}
```

### Best Practices

- **Reuse existing schemas** when possible through `$ref`
- **Use consistent naming** conventions across all schemas
- **Provide clear error messages** through descriptive constraints
- **Test edge cases** thoroughly with various data scenarios
- **Version schemas** appropriately when making breaking changes
- **Document all constraints** and their business rationale

## Schema Registry

All schemas are registered with canonical URIs:

- `https://gin.btaa.org/ld/schemas/resource.json`

These URIs can be referenced in `$schema` fields for IDE support and validation tools.

## Validation Tools

The repository includes several validation tools:

- **`validate_schema.py`** - Validate data against schemas
- **`validate_context.py`** - Validate JSON-LD contexts
- **`validate_vocabulary.py`** - Validate controlled vocabularies

These tools can be used individually or as part of CI/CD pipelines to ensure data quality. 