# Parameter Reference

{% include-markdown "includes/wip.md" %}

| Name | Type | Default | Description |
| :---- | :---- | :---- | :---- |
| `q` | string | `*:*` | Lucene/Solr‑style search string. |
| `page` | integer | 1 |  |
| `per_page` | integer (1‑100) | 10 | Page size. |
| `sort` | string | — | \` \<asc desc\>`; multiple separated by` ,\`. |
| `fields` | string (CSV) | — | Response field projection. |
| `facets` | string (CSV) | — | Fields to facet and count distinct values. |
| `filters` | object | — | Active facet filters |
| `include_ui` | boolean | true | Include Meta UI section |
| `callback` | string | — | JSONP callback name |
| `format` | string | JSON | Format options (JSON, CSV) |

## TODOs

* This is currently inchoate.