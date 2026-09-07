# Stripe Search Query Syntax

[↑ Full comparison table](../summary.md)

- **Category**: Search/full-text
- **Official docs**: [Search](https://docs.stripe.com/search)
- **Media type**: None known — Stripe's Search API accepts the query as a `query` URL/form parameter on `GET` requests (e.g. `GET /v1/charges/search?query=...`), not a dedicated media type.
- **Evaluated**: 2026-09-07

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 2 | Supports field:value clauses (token exact match, string exact/substring, numeric exact/comparison), a `~` substring operator, `-` negation, and up to 10 clauses combined by AND or OR, but a single query cannot mix AND and OR (and has no parentheses for precedence), and there is no ORDER BY/sort capability at all. |
| Simplicity | 4 | The `field:operator:value` clause shape is small, consistent, and documented per resource with clear type rules (token/string/numeric), making individual clauses easy to read and write. |
| Flexibility | 2 | Searchable fields are fixed per API resource (Charges, Customers, Invoices, PaymentIntents, Prices, Products, Subscriptions) and documented individually, so the language cannot be pointed at arbitrary or evolving data outside Stripe's own object model — though open-ended `metadata[key]:value` search adds some schema flexibility. |
| Community and Ecosystem | 4 | Stripe is a very widely adopted payments platform with an extensive developer community and SDK ecosystem, though its Search API is a narrower, comparatively newer sub-feature of Stripe's much larger REST API surface. |
| Extensibility | 1 | The set of searchable fields, operators, and clause limits (max 10 clauses) is fixed and defined entirely by Stripe per resource, with no mechanism for users to add fields, operators, or functions. |
| Transport Compatibility | 4 | Passed as a `query` parameter on Search API GET requests (e.g. `GET /v1/charges/search?query=...`), fitting naturally into a URL query string, consistent with the rest of Stripe's REST API conventions. |
| Standardization | 1 | A closed, single-vendor (Stripe) proprietary query syntax built into the Stripe API, with no published formal grammar specification or independent governance body. |
| Security | 4 | Requires quoted string values with documented escaping rules (`\"` for embedded quotes), giving clause parsing a well-defined structure rather than relying on ad hoc string concatenation, and the API is read-only and scoped to the authenticated account's own data. |
| Performance | 3 | Stripe's own docs state search data is indexed asynchronously with up to roughly a one-minute delay, recommend regular list-with-filters API calls instead of Search for read-after-write cases, and cap Search endpoints at 20 read requests per second — explicit, documented trade-offs versus Stripe's directly indexed list APIs. |
| Orthogonality | 2 | Clauses compose predictably via space/AND/OR/negation, but the documented rule that AND and OR cannot be mixed within the same query (with no parentheses to express precedence) is a real composability gap that forces restructuring rather than free combination. |

**Overall score (avg, informational only): 2.7**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 2.8**

## Summary

Stripe's search query syntax is a small, closed field:operator:value language for full-text and structured search over specific Stripe API resources (Charges, Customers, Invoices, PaymentIntents, Prices, Products, Subscriptions), supporting token/string/numeric field types, substring matching, negation, and metadata search. It has no sorting capability and cannot mix AND/OR in one query, trading expressiveness for a small, easy-to-learn syntax tightly scoped to Stripe's own resource model.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page.

```
metadata["category"]:"electronics" AND amount>100
```

Adapted to a Stripe resource with a numeric field (Charges' `amount`), since Stripe's documented Products/Prices search fields do not include a numeric price field; "category" is expressed via a custom metadata key since it is not a built-in field. Stripe's search syntax has no ORDER BY/sort clause at all, so results cannot be sorted by price, and there is no offset/page-number pagination — only cursor-based pagination via the `next_page` token returned in the previous response, which can only move strictly forward rather than jump to an arbitrary page.

## Sources

- Stripe. (n.d.). [*Search*](https://docs.stripe.com/search).
