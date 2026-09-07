# Algolia Filter Syntax

[↑ Full comparison table](../summary.md)

- **Category**: Search/full-text
- **Official docs**: [filters](https://www.algolia.com/doc/api-reference/api-parameters/filters/)
- **Media type**: None known — Algolia's Search API accepts `filters` as a string field in the JSON body of `POST /1/indexes/{indexName}/query`, not a dedicated media type.
- **Evaluated**: 2026-09-07

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | Supports facet filters, boolean filters, numeric comparisons (<, <=, =, !=, >=, >), numeric ranges (`low TO high`), tag filters, and filtering on array/nested attributes, combined via AND/OR/NOT with parenthesized grouping, but it is purely a filter language — full-text relevance search is a separate `query` parameter, and there is no built-in sort clause within the filter string itself. |
| Simplicity | 4 | The SQL-like `attribute:value`/comparison shape with boolean operators and parentheses is easy to read, though the docs devote extensive space to quoting edge cases (spaces, reserved keywords, embedded single/double quotes) that a user must get right. |
| Flexibility | 2 | Only attributes explicitly declared in `attributesForFaceting` (or governed by `numericAttributesForFiltering`) can be filtered on, so the filter language is scoped to a pre-configured, indexed subset of fields rather than being usable against arbitrary attributes. |
| Community and Ecosystem | 3 | Algolia is a well-established search-as-a-service platform with broad SDK support across many languages and a solid developer community, though a narrower footprint than general-purpose search engines like Elasticsearch. |
| Extensibility | 1 | The set of filter types (facet, boolean, numeric, range, tag, array, nested) and operators is fixed and defined entirely by Algolia, with no mechanism for users to add new filter types or functions. |
| Transport Compatibility | 3 | Passed as a `filters` string field in the JSON body of the Search API's `query` request (used identically across all official SDKs), fitting well as a structured request parameter, though it is not typically embedded as a bare URL query string like some other languages surveyed. |
| Standardization | 1 | A closed, single-vendor (Algolia) proprietary filter syntax built into the Algolia SaaS product, with no published formal grammar specification or independent governance body. |
| Security | 3 | Structured `attribute:value`/comparison clauses with well-documented quoting and escaping rules reduce ambiguity, and current-generation API clients auto-escape values, though the docs show that legacy API clients historically required manual escaping — a documented historical footgun. |
| Performance | 4 | Filtering is restricted to attributes explicitly declared in `attributesForFaceting`/`numericAttributesForFiltering`, a deliberate index-time trade-off that lets Algolia pre-build fast filter structures for exactly the fields a developer opts into, typical of the search-as-a-service performance model. |
| Orthogonality | 3 | Facet, boolean, numeric, and range filters share a broadly consistent `attribute:value`/comparison shape and combine uniformly via AND/OR/NOT with parentheses, but tag filters use their own distinct `_tags:value` shorthand rather than the general attribute syntax. |

**Overall score (avg, informational only): 2.8**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.0**

## Summary

Algolia's filter syntax is a closed, SQL-like `attribute:value` filter language layered alongside Algolia's separate full-text `query` parameter, supporting facet, boolean, numeric, range, tag, and array/nested attribute filters combined via AND/OR/NOT with parentheses. It requires attributes to be explicitly declared for faceting/numeric filtering ahead of time, trading schema flexibility for fast, pre-indexed filtering, and has no sort clause of its own — sorting is instead configured via replica indices.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page.

```
filters: "category:electronics AND price > 100"
```

Algolia's filter syntax has no runtime ORDER BY: sorting by an arbitrary field like price (descending) requires pre-configuring a replica index with a custom ranking formula at index-settings time, not expressing it in the filters string. Pagination (page 2 of 10) is likewise controlled by separate `page`/`hitsPerPage` request parameters, not by the filters string.

## Sources

- Algolia. (n.d.). [*filters*](https://www.algolia.com/doc/api-reference/api-parameters/filters/).
