# Parameter Reference

**TODO** — This is currently inchoate.

| Name | Type | Default | Description |
| :---- | :---- | :---- | :---- |
| `q` | string | `*:*` | Lucene/Solr‑style search string. |
| `page` | integer | 1 |  |
| `per_page` | integer (1‑100) | 10 | Page size. |
| `sort` | string | — | \` \<asc desc\>`; multiple separated by` ,\`. |
| `fields` | string (CSV) | — | Response field projection. |
| `facets` | string (CSV) | — | Fields to facet and count distinct values. |
| `filters` | object | — | Active facet filters |
| `pretty` | boolean | false | Human‑readable JSON. SHOULD NOT be used in production. |
| `include_ui` | boolean | true | Include Meta UI section |
| `include_geom` | boolean | true | Include Meta GEOM section |
| `callback` | string | — | JSONP callback name |
| `format` | string | JSON | Format options (JSON, CSV) |