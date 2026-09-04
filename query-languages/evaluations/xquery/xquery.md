# XQuery

[↑ Full comparison table](../summary.md)

- Category: Path/document navigation
- Official docs: [XQuery](https://www.w3.org/XML/Query/) (list.csv link; direct fetch returned HTTP 403, so this evaluation is sourced from Wikipedia's citation-backed coverage instead, following the same pattern used for SPARQL in Batch 3)
- Media type: None known / not registered — despite XQuery being a mature W3C Recommendation, no `application/xquery` (or similar) media type is registered with IANA.
- Evaluated: 2026-09-04

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 5 | A full functional programming language with FLWOR expressions (SQL-like joins via For, Let, Where, Order by, Return), user-defined functions, node construction, and a superset of XPath expression syntax. |
| Simplicity | 3 | Usability studies cited by Wikipedia found XQuery easier to learn than XSLT, especially for users with prior database-language experience, but as a full functional language with a rich XML-Schema-based type system, it has real depth beyond simple path queries. |
| Flexibility | 4 | Designed to query "collections of XML files... like databases" and extends to relational data and office documents via implementation-specific extensions, with the third-party JSONiq extension further adding native JSON support. |
| Community and Ecosystem | 3 | Implemented by multiple established XML database systems and processors (BaseX, eXist, MarkLogic, Saxon, Berkeley DB XML), a real but comparatively niche technology community relative to mainstream SQL or NoSQL ecosystems. |
| Extensibility | 4 | Supports formal W3C extension standards (XQuery Update Facility for data modification, Full-Text 1.0 for full-text search) plus a modular function/library system, with third-party extensions like JSONiq built directly on top of it. |
| Transport Compatibility | 2 | Typically embedded or executed within XML database engines or invoked via APIs (e.g. the XQuery API for Java); the third-party RESTXQ standard adds RESTful HTTP annotations, but this is not part of the core language itself. |
| Standardization | 5 | A formal W3C Recommendation (1.0 in January 2007, 3.0 in April 2014, 3.1 in March 2017), developed by the W3C XML Query working group in close coordination with the XSLT working group, sharing the same underlying XDM data model. |
| Security | 2 | Designed as a side-effect-free, functional language which reduces certain classes of risk and aids static analysis, but there is no documented built-in anti-injection mechanism for dynamically constructed queries. |
| Performance | 3 | Wikipedia notes XQuery is "very amenable to static analysis, which is essential to achieve the level of optimization needed in database query languages", though actual performance ultimately depends on the specific engine implementation. |
| Orthogonality | 4 | Wikipedia explicitly notes XQuery "is more orthogonal, in that any expression can be used in any syntactic context", directly contrasted with XSLT's more restrictive two-language system where XPath expressions can be nested in XSLT instructions but not vice versa. |

**Overall score (avg, informational only): 3.5**

## Summary

XQuery is a formally W3C-standardized, functional query and transformation language for XML that extends XPath with SQL-like FLWOR expressions and a highly orthogonal composition model, implemented across several established XML database engines, but it remains a comparatively niche technology outside the XML-database space, with no native HTTP transport of its own and no documented built-in defense against query injection.

## Sources

- Wikipedia. (2026, June 10). [*XQuery*](https://en.wikipedia.org/wiki/XQuery).
