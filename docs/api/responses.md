# Responses

{% include-markdown "includes/wip.md" %}

JSON-LD context for search responses:

* Future: https://opengeometadata/api/search/1.0/context/response.json  
* Draft PR: [Online here](https://raw.githubusercontent.com/OpenGeoMetadata/opengeometadata.github.io/18896025536dae80b632aa5b059fb001d3d42c56/docs/api/search/1.0/context/response.json)

## Resource Response

GET /api/v1/resource/91663ad7f1444494900f7e1cf063bfe5

```json
{
  "jsonapi": {
    "version": "1.1",
    "profile": [
      "https://opengeometadata.org/profile/aardvark",
      "https://opengeometadata.org/profile/ui-hints",
      "https://opengeometadata.org/profile/mcp/search"
    ]
  },

  "links": {
    "self": "https://api.example.org/v1/resource/91663ad7f1444494..."
  },

  "data": {
    "type": "resource",
    "id":   "91663ad7f1444494900f7e1cf063bfe5",

    "attributes": {
      "dct_title_s":          "Land Cover [Global]",
      "dct_alternative_sm":   ["Land Cover"],
      "dct_description_sm":   ["Global land cover type ..."],
      "dct_language_sm":      ["eng"],
      "schema_provider_s":    "University of Minnesota",
      "gbl_resourceClass_sm": ["Web services"],
      "dcat_theme_sm":        ["Land cover"],
      "dcat_keyword_sm":      ["Land Cover","Agriculture","Global",...],
      "dct_issued_s":         "2016-11-22",
      "gbl_dateRange_drsim":  ["[* TO *]"],
      "locn_geometry": {
        "type": "Polygon",
        "coordinates": [[[179,-75],[-179,-75],[-179,85],[179,85],[179,-75]]]
      },
      "dcat_bbox": {
        "type": "Polygon",
        "coordinates": [[[179,-75],[-179,-75],[-179,85],[179,85],[179,-75]]]
      },
      "dct_accessRights_s":   "Public",
      "gbl_fileSize_bytes":   81168384
    },

    "meta": {
      "@context": "https://static.opengeometadata.org/contexts/aardvark-1.0.jsonld",
      "@type":    "AardvarkRecord",
      "geometry": {
        "locn_geometry":   "ENVELOPE(179,-179,85,-75)",
        "dcat_bbox":       "ENVELOPE(179,-179,85,-75)",
        "dcat_centroid":   "5.0,0.0"
      },
      "human_readable": { "file_size": "77.4 MB" },
      "ui": {
        "viewer": {
          "protocol":  "arcgis_feature_layer",
          "endpoint":  "https://services.arcgis.com/8df8p0NlLFEShl0r/arcgis/rest/services/Land_Cover/FeatureServer/0",
          "geometry":  { "type": "Polygon", "coordinates": [[[179,-75],[-179,-75],[-179,85],[179,85],[179,-75]]] }
        },
        "citation": "U-Spatial. (2016-11-22). Land Cover [Global].",
        "relationships": {
          "member_of": {
            "links": { "related":     ".../resource/b0153110-e455-4ced-9114-9b13250a7093" },
            "data": [               { "type": "resource",                  "id": "b0153110-e455-4ced-9114-9b13250a7093"}]
         }
        }
      }
    }
  }
}
```

### META block

The META block MAY contain these potential user interface component entries (see 8.5):

| Feature | Key(s) | Description | Example Value(s) |
| :---- | :---- | :---- | :---- |
| Citation | citation | Generic citation format. String. | {"citation": "\[Creator not found\], (1932). A food map of the United States. https://quod.lib.umich.edu/c/clark1ic/x-003289100/39015091916158 (pictorial map)."} |
| Data Dictionary | dictionary | CSV | `document_data_dictionary_id,friendlier_id,field_name,field_type,values,definition,definition_source,parent_field_name,position` |
| Downloads | downloads | Convenience presentation of dct\_references\_s’ downloads. Array of objects. | {"downloads": \[{"label": "Download Shapefile", "url": "https://stacks.stanford.edu/object/cf162mm8787"}\]} |
| Metadata | metadata | Convenience presentation of dct\_references\_s’ metadata entries. Array of objects. | {"metadata": \[{"label": "ISO 19139", "url": "https://web.s3.wisc.edu/rml-gisdata/metadata/Bayfield\_Trails\_2020.xml"}\]} |
| Relationships | relationships | Convenience presentation of OGM Aardvark relationship fields. Nested Objects. | {"relationships": { "member\_of": { "links": { "related":     ".../resource/b0153110-e455-4ced-9114-9b13250a7093" }, "data": \[{ "type": "resource", "id": "b0153110-e455-4ced-9114-9b13250a7093"}\]}} |
| Viewer | viewer: protocol endpoint geometry | The viewer key contains all the necessary values to display an npm \`@geoblacklight-frontend\` package-driven item viewer. Object. | {"viewer": {"protocol": "iiif\_manifest", "endpoint": "https://quod.lib.umich.edu/cgi/i/image/api/search/clark1ic:003289100","geometry": { "type":"Polygon", "coordinates": \[\[\[\-124.98,49.31\],\[\-67.18,49.31\],\[\-67.18,22.61\],\[\-124.98,22.61\],\[\-124.98,49.31\]\]\] }}} |
| Thumbnail | thumbnail: url alt\_text | Thumbnail object, including URL and Alt Text entries. Object. | {"thumbnail": { "url":  "https://quod.lib.umich.edu/cgi/i/image/api/image/clark1ic:003289100:39015091916158/full/400,/0/default.jpg", "alt-text": "A food map of the United States"}} |

## Autosuggestion Response

GET /api/v1/suggest?q=minn

```json
{
  "jsonapi": {
    "version": "1.1",
    "profile": [
      "https://opengeometadata.org/profile/aardvark",
      "https://opengeometadata.org/profile/ui-hints",
      "https://opengeometadata.org/profile/mcp/search"
    ]
  },

  "links": {
    "self": "https://api.example.org/v1/suggest?q=minn&size=5"
  },

  "meta": {
    "query":          "minn",
    "took_ms":        191,
    "fuzzy":          true,
    "size":           5,

    "@context": "https://static.opengeometadata.org/contexts/aardvark-1.0.jsonld",

    /* --- optional diagnostics, gated by `debug=true` --- */
    "debug": {
      "es_query":   { /* redacted for brevity */ },
      "es_profile": { /* only if ?profile=true */ }
    }
  },

  "data": [
    {
      "type": "suggestion",
      "id":   "p16022coll245:1056",

      "attributes": {
        "label": "(Minneapolis, Minn.?)",
        "title": "University of Minnesota : plan of main campus"
      },

      "meta": { "score": 3 }
    },

    {
      "type": "suggestion",
      "id":   "international-boundary-collection",
      "attributes": {
        "label": "Mina de Oro St",
        "title": "International Boundary collection"
      },
      "meta": { "score": 3 }
    }

    /* ...three more suggestion objects ... */
  ]
}
```

## Search Results Response

GET /api/v1/search?q=land+cover

```json
{
  "jsonapi": {
    "version": "1.1",
    "profile": [
      "https://opengeometadata.org/profile/aardvark",
      "https://opengeometadata.org/profile/ui-hints",
      "https://opengeometadata.org/profile/mcp/search"
    ]
  },

  "links": {
    "self":  "https://api.example.org/v1/search?q=land+cover&page[number]=1&page[size]=10",
    "first": "https://api.example.org/v1/search?q=land+cover&page[number]=1&page[size]=10",
    "prev":  null,
    "next":  "https://api.example.org/v1/search?q=land+cover&page[number]=2&page[size]=10",
    "last":  "https://api.example.org/v1/search?q=land+cover&page[number]=155&page[size]=10"
  },

  "meta": {
    "query_time_ms": {
      "search":      958,
      "processing":    2185,
      "thumbnaill":  2178,
      "citation":   0,
      "viewer":     6,
      "total":              3143
    },
    "pagination": {
      "current": 1,
      "next":    2,
      "prev":    null,
      "total":  155,
      "per_page":     10,
      "offset":       0,
      "total_count":  1547
    },
    "spelling_suggestions": []
  },

  "data": [
    {
      "type": "document",
      "id":   "gm833zf4048",

      "attributes": {
        "dct_title_s":           "Urban Land Cover, Teheran, Iran, 1990",
        "dct_language_sm":       ["eng"],
        "schema_provider_s":     "Stanford",
        "gbl_resourceClass_sm":  ["Datasets"],
        "dcat_theme_sm":         ["Land Cover","Society","Imagery"],
        "dct_issued_s":          "2012",
        "locn_geometry":         "ENVELOPE(50.6773354,52.08805,36.2348092,34.8881922)",
        "dcat_bbox":             "ENVELOPE(50.6773354,52.08805,36.2348092,34.8881922)",
        "dct_accessRights_s":    "Public",
        "gbl_mdmodified_dt":     "2016-11-17T00:00:00",
        "gbl_mdversion_s":       "Aardvark"
      },

      "meta": {
        "score": 29.54668,
        "ui": {
          "viewer": {
            "protocol":  "oembed",
            "endpoint":  "https://purl.stanford.edu/embed.json?hide_title=true&url=https%3A%2F%2Fpurl.stanford.edu%2Fgm833zf4048",
            "geometry": {
              "type":        "Polygon",
              "coordinates": [[[50.6773354,36.2348092],[50.6773354,34.8881922],
                               [52.08805,34.8881922],[52.08805,36.2348092],
                               [50.6773354,36.2348092]]]
            }
          },
          "thumbnail_url": "https://geowebservices.stanford.edu/geoserver/wms/reflect?FORMAT=image/png&TRANSPARENT=TRUE&WIDTH=200&HEIGHT=200&LAYERS=druid:gm833zf4048",
          "citation":      "Angel, Shlomo ... (2012). Urban Land Cover, Teheran, Iran, 1990. Lincoln Institute of Land Policy. https://purl.stanford.edu/gm833zf4048 (raster data)",
          "ui_downloads": [
            {
              "label": "Download Shapefile",
              "url": [
                {
                  "url": "https://stacks.stanford.edu/object/mf519gg2738",
                  "label": "Zipped object"
                }
              ],
              "type": "shapefile"
            }
          ]
        },
        "@context": "https://static.opengeometadata.org/contexts/aardvark-1.0.jsonld",
        "@type":    "AardvarkRecord"
      }
    }
  ],

  "included": [
    {
      "type": "facet",
      "id":   "spatial_agg",
      "attributes": {
        "label":   "Spatial",
        "buckets": [
          { "label": "Earth (Planet)", "value": "Earth (Planet)", "hits": 1033 },
          { "label": "California",     "value": "California",     "hits":   38 }
        ]
      }
    },
    {
      "type": "facet",
      "id":   "resource_class_agg",
      "attributes": {
        "label":   "Resource Class",
        "buckets": [
          { "label": "Datasets", "value": "Datasets", "hits": 1513 },
          { "label": "Maps",     "value": "Maps",     "hits":   26 }
        ]
      }
    }
  ]
}
```

## UI Component Support

A list of the frontend feature components this OGM API can support. 

See the BTAA proof of concept React UI for an example implementation:  
[https://github.com/geobtaa/rui](https://github.com/geobtaa/rui)

### Search

* Autocomplete  
* Search  
* Map Search  
* Results  
* Result Thumbnails  
* Facets  
* Pagination  
* Per Page  
* Sorting  
* Spelling Suggestions  
* Constraints

### Resource View

* Viewer  
* Context  
  * Breadcrumb  
  * Sidebar Map  
  * More Like This  
* Metadata Text  
* Metadata Links  
* Citation  
* Downloads  
* Relationships