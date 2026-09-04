# CouchDB Mango Query Language

- **Category**: Document/NoSQL
- **Official docs**: [CouchDB Mango Query Language](https://dev.to/yenyih/query-in-apache-couchdb-mango-query-lfd)
- **Media type**: None known — Mango selectors are POSTed as a JSON document to `/db/_find` using the generic `application/json` media type.
- **Evaluated**: 2026-09-04

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 3 | JSON-based selector syntax supports rich operators ($gt, $lt, $in, $regex, etc.), sorting, field projection, pagination via bookmarks, and execution-stats/explain introspection, but lacks SQL-style joins or aggregation. |
| Simplicity | 4 | Declarative JSON selector documents are straightforward to construct without writing JavaScript map/reduce views; Mango was created specifically to simplify CouchDB querying. |
| Flexibility | 4 | Operates over CouchDB's schema-less JSON documents and can create ad hoc indexes on the fly, well suited to evolving document shapes. |
| Community and Ecosystem | 3 | Backed by the Apache Software Foundation with solid documentation, but CouchDB has a smaller, more specialized community (offline-first/sync use cases) than mainstream NoSQL databases. |
| Extensibility | 2 | Selector operators and index types (json/text/nouveau) are fixed by CouchDB; Mango itself provides no user-defined functions, unlike the older JavaScript map/reduce views. |
| Transport Compatibility | 5 | Mango queries are POSTed as JSON bodies to CouchDB's native HTTP _find endpoint, making the language inherently designed for HTTP-based access, consistent with CouchDB's all-HTTP API design. |
| Standardization | 1 | A CouchDB/Mango-specific syntax with no independent standard or cross-vendor adoption. |
| Security | 3 | Being JSON-document based rather than a string-concatenated query language reduces classic injection risk, though care is still needed with dynamically constructed selectors. |
| Performance | 3 | Relies on explicit or automatically-selected secondary indexes; querying without a suitable index falls back to the slow built-in _all_docs index, which the docs explicitly warn against. |
| Orthogonality | 3 | Selector, sort, fields, and pagination options compose predictably as JSON, though sort fields must already be covered by an existing index, a documented constraint on composability. |

**Overall score (avg, informational only): 3.1**

## Summary

CouchDB's Mango query language offers a simple, JSON-native declarative alternative to hand-written map/reduce views, well suited to CouchDB's HTTP-first, schema-less document model, but it is CouchDB-specific with no independent standardization and lacks SQL-style joins or aggregation.

## Sources

- Apache Software Foundation. (n.d.). [*1.3.6. /{db}/_find (Mango Query API)*](https://docs.couchdb.org/en/stable/api/database/find.html).
- Wikipedia. (2025, December 30). [*Apache CouchDB*](https://en.wikipedia.org/wiki/Apache_CouchDB).
