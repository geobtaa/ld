# GeoBTAA API & Linked Data

{% include-markdown "includes/wip.md" %}

Welcome to the GeoBTAA API & Linked Data repository. This comprehensive platform provides both a RESTful API for geospatial metadata discovery and a collection of linked data assets for the Big Ten Academic Alliance (BTAA) geospatial data infrastructure.

## Overview

The GeoBTAA platform consists of two main components:

### 🔌 **GeoBTAA API**
A read-only, OpenGeoMetadata API-compliant web service for programmatically accessing, searching, and retrieving metadata records that conform to the BTAA GIN's GeoBTAA extended-OGM Aardvark schema.

**Key Features:**
- **RESTful Design** - Predictable, cache-friendly URLs
- **OpenGeoMetadata Compliance** - Built on open standards
- **Spatial Search** - Full-text and geospatial discovery
- **Structured Metadata** - JSON-LD formatted responses
- **Client-Friendly** - Powers search interfaces and GIS applications

### 🔗 **Linked Data Assets**
A collection of semantic web resources that provide standardized data models, vocabularies, and schemas for geospatial metadata.

**Available Assets:**
- **Contexts** - JSON-LD context files for data modeling
- **Profiles** - JSON-LD data profiles and specifications
- **Schemas** - JSON Schema definitions for validation

## Quick Start

### For API Users

1. **Read the [API Documentation](api/index.md)** - Complete specification and examples
2. **Check [Authentication](api/authentication.md)** - API key requirements
3. **Explore [Endpoints](api/requests.md)** - Available API operations
4. **Review [Rate Limits](api/rate_limiting.md)** - Usage guidelines

### For Linked Data Developers

1. **Browse [Linked Data Assets](linked-data/)** - Contexts, vocabularies, ontologies, and schemas
2. **Check [Schemas](linked-data/schemas.md)** - JSON Schema validation
3. **Review [API Reference](linked-data/reference.md)** - Technical specifications
4. **Explore [Standards](api/standards.md)** - Compliance and interoperability

## Use Cases

### 🏛️ **Academic Libraries**
- Power geospatial discovery interfaces
- Integrate with existing library systems
- Provide standardized metadata access

### 🔬 **Researchers**
- Automate metadata discovery workflows
- Access structured geospatial data
- Build reproducible research pipelines

### 🛠️ **Developers**
- Create GIS applications and plugins
- Build search and discovery tools
- Integrate with existing geospatial workflows

### 🌐 **Data Providers**
- Standardize metadata formats
- Ensure interoperability
- Improve data discoverability

## Technical Stack

- **API**: RESTful web service with JSON-LD responses
- **Schema**: OpenGeoMetadata Aardvark with BTAA extensions
- **Authentication**: API key-based access
- **Documentation**: MkDocs with Material theme
- **Standards**: IIIF-inspired specification structure

## Getting Started

### Local Development

```bash
# Install dependencies
pip install -r requirements-docs.txt

# Start documentation server
mkdocs serve

# Access at http://localhost:8000
```

### API Access

```bash
# Example API request
curl -H "Authorization: Bearer YOUR_API_KEY" \
     https://api.geobtaa.org/resources
```

### Schema Validation

```bash
# Validate your data against our schemas
python scripts/validate_schema.py --schema schemas/resource.json --data your-data.json
```

## Support & Community

- **Issues**: [GitHub Issues](https://github.com/geobtaa/ld/issues)
- **Discussions**: [GitHub Discussions](https://github.com/geobtaa/ld/discussions)
- **Email**: geobtaa@lists.illinois.edu
- **Documentation**: This site and [API Reference](api/index.md)

---

*This project is part of the Big Ten Academic Alliance Geospatial Data Infrastructure.* 