# Protocol &amp; Versioning

{% include-markdown "includes/wip.md" %}

* API Base URI:  
  * [`https://api.geo.btaa.org/v1`](https://api.geo.btaa.org/v1)  
* Content types:  
  * `application/json` (default)  
  * `application/ld+json` (when `Accept` header includes JSON‑LD)  
  * text/csv (when Accept header includes CSV)  
* HTTP 1.1 or HTTP/2 over TLS 1.2+ **MUST** be supported.  
* HTTP/3 **RECOMMENDED**  
* Minor revisions to this spec will increment the *patch* version (e.g., `1.0.1`) and **MUST NOT** introduce breaking changes.