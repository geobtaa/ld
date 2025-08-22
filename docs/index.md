# GeoBTAA API & Linked Data

{% include-markdown "includes/wip.md" %}

Welcome to the GeoBTAA API and Linked Data homepage. This comprehensive platform provides both a RESTful API for geospatial metadata discovery and a collection of linked data assets for the Big Ten Academic Alliance (BTAA) geospatial data infrastructure.

## Overview

The GeoBTAA API platform consists of two primary components: 1) the [**GeoBTAA API**](#geobtaa-api) and 2) our [**Linked Data Assets**](#linked-data-assets)

![Strategic Technology Plan](images/strategic-tech-plan.png)

### **GeoBTAA API**
A read-only, OpenGeoMetadata API-compliant web service for programmatically accessing, searching, and retrieving metadata records that conform to the BTAA GIN's GeoBTAA extended-OGM Aardvark schema.

[GeoBTAA API Documentation :octicons-arrow-right-24:](/api){ .md-button .md-button--primary }

#### Key Features

* **RESTful Design** - Predictable, cache-friendly URLs
* **OpenGeoMetadata API Compliance** - Built on open standards
* **Faceted Spatial Search** - Full-text, faceted geospatial discovery
* **Structured Metadata** - JSON-LD formatted responses
* **Client-Friendly** - Powers search interfaces and GIS applications

### **Linked Data Assets**
A collection of semantic web resources that provide standardized data models and schemas for BTAA geospatial metadata.

[Linked Data Asset Documentation :octicons-arrow-right-24:](/ld){ .md-button .md-button--primary }

**Available Assets:**

* **Contexts** - JSON-LD context files for data modeling
* **Profiles** - JSON-LD data profiles and specifications
* **Schemas** - JSON Schema definitions for validation

## Quick Start

### For API Users

1. **Read the [API Documentation](api/index.md)** - Complete specification and examples
2. **Check [Authentication](api/authentication.md)** - API key requirements
3. **Explore [Endpoints](api/requests.md)** - Available API operations
4. **Review [Rate Limits](api/rate_limiting.md)** - Usage guidelines

### For Linked Data Developers

1. **Browse [Linked Data Assets](linked-data/)** - Contexts, profiles, and schemas
2. **Check [Schemas](linked-data/schemas.md)** - JSON Schema validation
3. **Review [API Reference](linked-data/reference.md)** - Technical specifications
4. **Explore [Standards](api/standards.md)** - Compliance and interoperability

## Use Cases

### **Academic Libraries**
- Power geospatial discovery interfaces, like the BTAA Geoportal
- Integrate with existing library systems
- Provide standardized metadata access

### **Researchers**
- Automate metadata discovery workflows
- Access structured geospatial data
- Build reproducible research pipelines

### **Developers**
- Create GIS applications and plugins
- Build search and discovery tools
- Integrate with existing geospatial workflows

### **Data Providers**
- Standardized metadata formats
- Ensure interoperability
- Improve data discoverability

## Getting Started

### API Access

```bash
# Example API request
curl -H "Authorization: Bearer YOUR_API_KEY" \
     https://api.geobtaa.org/resources
```

## Support & Community

- **Contact Us**: [Feedback](https://geo.btaa.org/feedback)
- **Issues**: [GitHub Issues](https://github.com/geobtaa/ld/issues)
- **Discussions**: [GitHub Discussions](https://github.com/geobtaa/ld/discussions)
- **Documentation**: [API Reference](api/index.md)

---

*This project is part of the Big Ten Academic Alliance Geospatial Data Infrastructure.* 