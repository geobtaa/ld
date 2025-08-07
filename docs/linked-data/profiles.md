# Profiles

JSON-LD profiles define specific subsets of vocabularies and constraints for particular use cases, enabling targeted data exchange and validation within the GeoBTAA ecosystem.

## Overview

Profiles in this repository define:

- **Vocabulary subsets**: Curated sets of terms from broader vocabularies
- **Use case constraints**: Specific requirements for different data exchange scenarios
- **Validation rules**: Profile-specific validation and business logic
- **Interoperability guarantees**: Assurances about data compatibility
- **Implementation guidance**: Best practices for profile adoption

## What are JSON-LD Profiles?

JSON-LD profiles are specifications that define how to use JSON-LD in a particular context or for a specific purpose. They provide:

- **Constrained vocabularies**: Only specific terms from broader vocabularies
- **Mandatory properties**: Required fields for profile compliance
- **Value constraints**: Allowed values and formats
- **Extension points**: Where and how to add custom properties
- **Implementation guidance**: How to use the profile effectively

## Available Profiles

### GeoBTAA Core Profile

**Purpose**: Basic geospatial resource description for general discovery and cataloging

**Scope**: Essential metadata for geospatial resources in the GeoBTAA network

**Key Features**:
- Dublin Core metadata compliance
- Basic spatial and temporal coverage
- Access rights and licensing information
- Provenance tracking
- Minimal required fields for discovery

**Required Properties**:
- `@type` - Resource type (Dataset, Service, etc.)
- `dct:title` - Resource title
- `dct:description` - Resource description
- `dct:language` - Language(s) of the resource
- `dct:accessRights` - Access rights information
- `dct:license` - License information
- `dct:spatial` - Spatial coverage
- `dct:temporal` - Temporal coverage (if applicable)
- `prov:wasGeneratedBy` - Data generation process
- `geobtaa:code` - GeoBTAA identifier

**Example Usage**:

```json
{
  "@context": "https://raw.githubusercontent.com/geobtaa/ld/main/contexts/core.jsonld",
  "@type": "Dataset",
  "dct:title": "Midwest Population Density 2020",
  "dct:description": "Population density data for the Midwest United States",
  "dct:language": "en",
  "dct:accessRights": "Public",
  "dct:license": "https://creativecommons.org/licenses/by/4.0/",
  "dct:spatial": "Midwest United States",
  "dct:temporal": "2020",
  "prov:wasGeneratedBy": "US Census Bureau",
  "geobtaa:code": "MIDWEST_POP_2020"
}
```

### GeoBTAA Extended Profile

**Purpose**: Comprehensive geospatial resource description with detailed metadata

**Scope**: Full metadata description including technical specifications, quality information, and administrative details

**Key Features**:
- All Core Profile requirements
- Technical specifications and formats
- Quality and accuracy information
- Detailed administrative metadata
- Extended spatial and temporal coverage
- Related resource links

**Additional Required Properties**:
- `dct:format` - File format or media type
- `dct:creator` - Resource creator
- `dct:publisher` - Resource publisher
- `dct:issued` - Publication date
- `dct:modified` - Last modification date
- `geo:hasGeometry` - Detailed spatial geometry
- `geobtaa:qualityScore` - Data quality assessment
- `geobtaa:updateFrequency` - Update frequency
- `geobtaa:contactPoint` - Contact information

**Example Usage**:

```json
{
  "@context": "https://raw.githubusercontent.com/geobtaa/ld/main/contexts/core.jsonld",
  "@type": "Dataset",
  "dct:title": "Midwest Population Density 2020",
  "dct:description": "Population density data for the Midwest United States",
  "dct:language": "en",
  "dct:accessRights": "Public",
  "dct:license": "https://creativecommons.org/licenses/by/4.0/",
  "dct:spatial": "Midwest United States",
  "dct:temporal": "2020",
  "dct:format": "application/zip",
  "dct:creator": "US Census Bureau",
  "dct:publisher": "GeoBTAA",
  "dct:issued": "2024-01-15",
  "dct:modified": "2024-01-15",
  "geo:hasGeometry": {
    "@type": "geo:Geometry",
    "geo:asWKT": "POLYGON((-104.0 36.0, -80.0 36.0, -80.0 49.0, -104.0 49.0, -104.0 36.0))"
  },
  "geobtaa:qualityScore": 0.95,
  "geobtaa:updateFrequency": "Decennial",
  "geobtaa:contactPoint": "data@geobtaa.org",
  "prov:wasGeneratedBy": "US Census Bureau",
  "geobtaa:code": "MIDWEST_POP_2020"
}
```

### GeoBTAA Harvest Profile

**Purpose**: Optimized for automated harvesting and indexing

**Scope**: Streamlined metadata for efficient harvesting and processing

**Key Features**:
- Minimal required fields for harvesting
- Optimized for machine processing
- Standardized identifiers and URLs
- Harvest-specific metadata

**Required Properties**:
- `@id` - Unique resource identifier
- `@type` - Resource type
- `dct:title` - Resource title
- `dct:description` - Resource description
- `dct:identifier` - Persistent identifier
- `dct:source` - Source URL for harvesting
- `dct:modified` - Last modification date
- `geobtaa:harvestDate` - Date of last harvest
- `geobtaa:harvestStatus` - Harvest status

## Profile Validation

### Profile Compliance

Each profile defines specific validation rules that data must satisfy:

```python
import json
from jsonschema import validate

def validate_profile(data, profile_name):
    """Validate data against a specific profile."""
    profile_schema = load_profile_schema(profile_name)
    
    try:
        validate(instance=data, schema=profile_schema)
        return True, "Profile validation passed"
    except ValidationError as e:
        return False, f"Profile validation failed: {e.message}"
```

### Profile Selection

Choose the appropriate profile based on your use case:

- **Core Profile**: Basic discovery and cataloging
- **Extended Profile**: Comprehensive metadata management
- **Harvest Profile**: Automated harvesting and indexing

## Implementation Guidelines

### Creating Profile-Compliant Data

1. **Select the appropriate profile** for your use case
2. **Include the required context** for the profile
3. **Provide all mandatory properties** as specified
4. **Follow value constraints** and format requirements
5. **Validate your data** against the profile schema

### Profile Extensions

Profiles can be extended with additional properties:

```json
{
  "@context": "https://raw.githubusercontent.com/geobtaa/ld/main/contexts/core.jsonld",
  "@type": "Dataset",
  "dct:title": "Example Dataset",
  // ... core profile properties ...
  
  // Profile extensions
  "custom:specialProperty": "Custom value",
  "custom:internalId": "INT-001"
}
```

### Best Practices

- **Use consistent identifiers** across your data
- **Provide meaningful descriptions** for all resources
- **Include appropriate spatial and temporal coverage**
- **Maintain provenance information** for data lineage
- **Regularly validate** against profile schemas
- **Document any extensions** to standard profiles

## Profile Evolution

Profiles are versioned and may evolve over time:

- **Backward compatibility** is maintained when possible
- **New versions** are clearly documented
- **Migration guides** are provided for breaking changes
- **Deprecation notices** are given for removed features

## Related Documentation

- [Contexts](contexts.md) - JSON-LD context definitions
- [Schemas](schemas.md) - JSON Schema validation
- [Vocabularies](vocabularies.md) - Term definitions and usage
- [Ontologies](ontologies.md) - Semantic relationships and constraints
