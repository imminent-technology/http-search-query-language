# RSQL/FIQL

[↑ Full comparison table](../summary.md)

- **Category**: API/data-fetching
- **Official docs**: [RSQL / FIQL parser](https://github.com/jirutka/rsql-parser)
- **Media type**: None known — RSQL/FIQL expressions are embedded as a plain-text query-string parameter (e.g. a `query` or `filter` param) on a REST API's URL; no IANA-registered or vendor-documented media type exists for either syntax.
- **Evaluated**: 2026-09-05

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 3 | Both grammars express boolean AND/OR combinations of comparisons (with parenthesized grouping to override the default AND-before-OR precedence) and RSQL adds set-membership operators (`=in=`/`=out=`) with parenthesized multi-value arguments, but the language is scoped purely to filtering — it has no built-in concept of sorting, aggregation, field projection, or joins across resources. |
| Simplicity | 4 | RSQL's own README explicitly motivates its friendlier alternative operators (`>`, `<`, `and`, `or`) by noting that "FIQL's syntax is not very intuitive"; a query like `director.lastName==Nolan and year>=2000` reads close to plain English, though FIQL's raw punctuation-only form (`;`, `,`, `=ge=`) remains terser and less approachable on its own. |
| Flexibility | 4 | The RSQL grammar explicitly does not constrain selector syntax ("the specific syntax of the selector is not enforced by this parser"), letting it address arbitrary resource fields including nested paths (e.g. `director.lastName`), and its AST-based design has been retargeted to multiple backends (JPA Specifications/QueryDSL, MongoDB queries) by independent converter libraries. |
| Community and Ecosystem | 3 | The reference `jirutka/rsql-parser` Java implementation has roughly 800 GitHub stars and is a declared dependency of about 750 other repositories, with several independent derivative libraries (rsql-jpa-specification, rsql-mongodb, q-builders) and adoption in Corda's Vaultaire query layer, but it remains a single open-source project's grammar rather than a language with multiple independent, cross-vendor implementations. |
| Extensibility | 4 | The reference parser documents a concrete extension mechanism for adding custom comparison operators via `RSQLOperators.defaultOperators()` plus `operators.add(new ComparisonOperator(...))`, letting consumers add operators like a custom `=all=` without forking the grammar. |
| Transport Compatibility | 4 | FIQL's specification states it is "optimised and intended for use in the query component of an HTTP URI" specifically because its operator characters need no percent-encoding; RSQL preserves this URL-friendliness while its alternative operators (`>`, `<`) reintroduce a small amount of encoding overhead in a raw query string. |
| Standardization | 1 | FIQL exists only as an individual, non-working-group IETF Internet-Draft (draft-nottingham-atompub-fiql-00) that expired in June 2008 without ever advancing to RFC status, and RSQL itself has no specification beyond a single open-source project's README grammar — neither has any standards-body governance today. |
| Security | 3 | Like other client-constructed filter-expression languages, RSQL/FIQL queries are typically raw strings with no built-in parameterization; safety depends entirely on how the consuming application translates the parsed AST into a backend query (e.g. safely into a JPA `Specification`) rather than on any protection built into the grammar itself. |
| Performance | 3 | Neither specification defines indexing, planning, or evaluation-order semantics, but because RSQL/FIQL expressions are designed to be translated into a backend's own optimizable query (SQL/JPA Criteria, MongoDB query documents) rather than evaluated in-memory by the parser itself, actual performance depends on and can benefit from that backend's own optimizer. |
| Orthogonality | 4 | The grammar composes uniformly: any comparison or parenthesized sub-expression can appear as an operand of AND/OR at any nesting depth, and every comparison operator accepts the same value/multi-value argument forms, giving predictable, composable behavior across the whole grammar. |

**Overall score (avg, informational only): 3.3**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.6**

## Summary

RSQL and FIQL are evaluated together as a single, closely related pair: FIQL (the Feed Item Query Language) is Mark Nottingham's 2007 IETF Internet-Draft for a URL-friendly Atom/RSS feed filter syntax that expired in 2008 without becoming an RFC, and RSQL is Jakub Jirutka's open-source superset of FIQL that adds friendlier alternative operators (`>`, `<`, `and`, `or`) for use in RESTful API filtering. Neither has formal standards-body backing, but RSQL's reference parser has real ecosystem traction — hundreds of dependent projects and independent converters targeting JPA, QueryDSL, and MongoDB — and its extensible operator model and URL-native design make it a practical, if narrowly filter-scoped, choice for REST API query parameters.

## Sources

- Nottingham, M. (2007, December 12). [*FIQL: The Feed Item Query Language (draft-nottingham-atompub-fiql-00)*](https://datatracker.ietf.org/doc/html/draft-nottingham-atompub-fiql-00). IETF.
- Jirutka, J. (n.d.). [*RSQL / FIQL parser*](https://github.com/jirutka/rsql-parser).
