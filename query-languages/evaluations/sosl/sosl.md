# SOSL

[↑ Full comparison table](../summary.md)

- **Category**: Search/full-text
- **Official docs**: [Salesforce Object Search Language (SOSL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_sosl.htm)
- **Media type**: None known — Salesforce's REST API accepts SOSL as a `q` URL query parameter on the `GET /services/data/vXX.X/search` endpoint, not a dedicated media type.
- **Evaluated**: 2026-09-07

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | A single FIND {...} clause can search text across ALL FIELDS/NAME FIELDS/EMAIL FIELDS/PHONE FIELDS/SIDEBAR FIELDS and return results scoped to multiple different standard and custom Salesforce objects at once via RETURNING, each with its own WHERE/ORDER BY/LIMIT — genuine multi-object full-text search in one query, though it is not a general relational query language and has no explicit join syntax. |
| Simplicity | 3 | The core FIND {...} shape is simple, but the full grammar layers many optional clauses in a required order (IN, RETURNING, WITH DivisionFilter, WITH DATA CATEGORY, WITH SNIPPET, WITH NETWORK, WITH PricebookId, WITH METADATA, LIMIT, UPDATE), making advanced queries verbose. |
| Flexibility | 3 | A single SOSL query can span many different standard and custom Salesforce objects in one search, adapting well to varied CRM data models, though every object and field must still be predefined in the Salesforce schema rather than being schema-free. |
| Community and Ecosystem | 4 | Salesforce is one of the most widely adopted enterprise CRM platforms, and SOSL/SOQL are core, extensively documented parts of its developer platform (Apex, REST/SOAP APIs, Trailhead training). |
| Extensibility | 2 | SOSL has no user-defined function mechanism within the query language itself; its adaptability comes from Salesforce's underlying custom-object/custom-field platform rather than from extensible query syntax. |
| Transport Compatibility | 4 | Executed via the SOAP API's search() call, the REST API's Search resource as a `q` URL query parameter, or Apex, fitting naturally into a URL query string for REST-based access. |
| Standardization | 1 | A closed, single-vendor (Salesforce) proprietary query language embedded in the Salesforce platform, with no published formal grammar specification or independent governance body. |
| Security | 3 | The FIND clause takes a curly-brace-delimited search string while RETURNING/WHERE use structured field=value syntax, and Apex supports bind variables to avoid string concatenation, but the documented behavior of silently converting AND to OR when a search string exceeds 4,000 characters is a notable footgun that can unintentionally broaden results. |
| Performance | 3 | Runs against Salesforce's dedicated search index (separate from the SOQL relational query engine) for fast term-based lookups, but results are explicitly capped at 2,000 rows via LIMIT (200 for API versions before 28.0), a documented ceiling for large result sets. |
| Orthogonality | 2 | The official syntax reference states that after the required FIND clause, all optional clauses must appear "in the following order" — the grammar is a fixed clause sequence rather than freely composable clauses, and OFFSET/WHERE/ORDER BY are nested inside RETURNING's FieldSpec rather than being top-level, independent clauses. |

**Overall score (avg, informational only): 2.9**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.0**

## Summary

SOSL (Salesforce Object Search Language) is Salesforce's full-text search language for finding text across multiple standard and custom objects in a single query, returning per-object results via a RETURNING clause that nests its own WHERE, ORDER BY, LIMIT, and OFFSET. It is a closed, single-vendor language with a fixed, ordered clause grammar, but its ability to search and filter across many object types in one request gives it real expressiveness for CRM-style multi-entity search.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page.

```sosl
FIND {electronics} IN ALL FIELDS RETURNING Product2(Name, UnitPrice WHERE Family = 'Electronics' AND UnitPrice > 100 ORDER BY UnitPrice DESC LIMIT 10 OFFSET 10)
```

SOSL maps all three ingredients natively: the WHERE filter, ORDER BY, LIMIT, and OFFSET are all embedded inside the RETURNING clause's per-object FieldSpec grammar rather than being separate top-level clauses, and LIMIT/OFFSET together express "page 2 of 10."

## Sources

- Salesforce. (n.d.). [*Salesforce Object Search Language (SOSL)*](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_sosl.htm).
- Salesforce. (n.d.). [*SOSL Syntax*](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_sosl_syntax.htm).
