# Firebase Realtime Database Query Language

- **Category**: Document/NoSQL
- **Official docs**: [Retrieving Data](https://firebase.google.com/docs/database/admin/retrieve-data)
- **Media type**: None known — query parameters are passed via the URL query string on the REST API; responses use generic `application/json`.
- **Evaluated**: 2026-09-04

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 2 | Queries can only order by one child key/value/key at a time (orderByChild, orderByKey, orderByValue) combined with limit/range methods; there is no compound filtering across multiple fields, no joins, and no aggregation. |
| Simplicity | 4 | A small, easy-to-learn set of ordering and range methods (orderByChild, limitToFirst, startAt, endAt, equalTo) that compose in simple chains. |
| Flexibility | 3 | Works over a single large schema-less JSON tree, but the lack of compound queries means complex access patterns often require denormalizing data rather than relying on flexible querying. |
| Community and Ecosystem | 3 | Long-established as Firebase's original 2012 product with solid official docs and multi-language SDKs, though Google has steered new development toward Firestore as its successor. |
| Extensibility | 1 | The query surface is fixed to the documented ordering/range/limit methods, with no mechanism for custom query logic beyond client-side filtering after retrieval. |
| Transport Compatibility | 3 | Reachable via a REST API where query parameters (orderBy, startAt, etc.) can be passed directly on the URL in addition to persistent SDK connections, giving partial URL-based usability. |
| Standardization | 1 | A proprietary Google/Firebase API with no independent specification. |
| Security | 3 | Queries are built via SDK method chains rather than raw strings and are gated by Realtime Database security rules, though the product's historically permissive default configuration has caused real-world data exposure incidents. |
| Performance | 3 | Requires explicit .indexOn rules for production-scale ordered queries; without them, ad hoc queries can be slow, as the documentation explicitly warns. |
| Orthogonality | 2 | Ordering functions cannot be combined (e.g., calling orderByChild() twice throws an error), and range/limit methods only layer on top of a single ordering choice, a notable composability limitation. |

**Overall score (avg, informational only): 2.5**

## Summary

Firebase Realtime Database's query language offers a small, easy-to-learn set of single-key ordering and range methods well suited to simple lookups, but it cannot combine multiple ordering criteria or filter compound conditions, making it the least expressive of Firebase's two database query languages and largely superseded by Firestore.

## Sources

- Google. (2026, September 1). [*Retrieving Data*](https://firebase.google.com/docs/database/admin/retrieve-data).
- Wikipedia. (2026, July 20). [*Firebase*](https://en.wikipedia.org/wiki/Firebase).
