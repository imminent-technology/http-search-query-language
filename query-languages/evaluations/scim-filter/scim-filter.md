# SCIM Filter

[↑ Full comparison table](../summary.md)

- **Category**: API/data-fetching
- **Official docs**: [RFC 7644 §3.4.2.2 "Filtering"](https://datatracker.ietf.org/doc/html/rfc7644#section-3.4.2.2)
- **Media type**: `application/scim+json` — IANA-registered per RFC 7644 §8.1 (intended usage: COMMON, with restrictions).
- **Evaluated**: 2026-09-05

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | The filter grammar (RFC 7644 §3.4.2.2) offers ten attribute operators (eq, ne, co, sw, ew, pr, gt, ge, lt, le), logical and/or/not, parenthesized grouping, and a distinctive bracketed complex-attribute filter (`emails[type eq "work" and value co "@example.com"]`) that scopes sub-expressions to the same value of a multi-valued attribute — richer than a typical flat predicate language, though scoped purely to filtering with no sorting/projection built in (those are separate sortBy/attributes parameters). |
| Simplicity | 4 | Filters read close to plain English (`userName eq "bjensen"`, `title pr and userType eq "Employee"`), and RFC 7644 explicitly makes attribute names and operators case-insensitive to reduce friction, though the bracketed complex-attribute grouping adds some learning curve beyond simple equality checks. |
| Flexibility | 3 | Attribute paths can address nested sub-attributes (`name.givenName`) and schema-extension-qualified names via URN prefixes (`urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:employeeNumber`), but filtering is still bound to the SCIM resource/schema model (User, Group, and registered extensions) rather than being usable against arbitrary, schema-less data. |
| Community and Ecosystem | 4 | SCIM 2.0 is a mature, widely deployed provisioning standard implemented by major identity providers and SaaS platforms (Okta, Microsoft Entra ID, Salesforce, Ping Identity, SailPoint, and others per Wikipedia's implementation history and interoperability events dating to 2011), with an active IETF working group and numerous open-source client/server libraries. |
| Extensibility | 4 | The protocol has an explicit extension model: custom resource schemas and attributes are added via registered URN-prefixed schema extensions, filters can reference those extension attributes directly, and RFC 7644 explicitly allows service providers to support additional filter operators beyond the ten defined. |
| Transport Compatibility | 5 | The filter is designed from the outset as an HTTP query-string parameter (`GET /Users?filter=...`) with a documented POST-based `/.search` fallback specifically for cases where exposing filter content in a URL would leak sensitive information (§7.5.2) — a deliberate, dual HTTP-native design matching the dataset's top tier. |
| Standardization | 5 | SCIM Filter is defined within RFC 7644, an IETF Internet Standards Track "Proposed Standard" produced by the IETF's own SCIM working group — the same formal governance tier as SQL, JPQL, SPARQL, XPath/XQuery, OData, and JSONPath in this dataset. |
| Security | 3 | RFC 7644 mandates TLS 1.2 for transport and documents OAuth 2.0 bearer-token threat considerations plus a specific safeguard against leaking sensitive filter content in URIs (403 + POST fallback), but like other string-based filter expressions, SCIM filters still depend on the service provider safely translating filter text into a backend query (e.g., SQL or LDAP), and the spec itself defines no language-level injection protection. |
| Performance | 3 | The spec defines no indexing or query-planning semantics and leaves execution entirely to the service provider, but it does build in an explicit performance safety valve: providers MAY reject overly broad filters (e.g., a bare `userName pr`) with a "tooMany" error rather than compute an unbounded result set. |
| Orthogonality | 4 | Every attribute expression follows the same attrPath+operator(+value) shape, logical `and`/`or`/`not` combine any FILTER or complex-attribute sub-expression uniformly, and the bracketed valuePath grouping composes predictably with nested filters — a small, consistent set of composition rules per the ABNF grammar in Figure 1. |

**Overall score (avg, informational only): 3.9**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.8**

## Summary

SCIM Filter is the query/filter expression language defined within RFC 7644, the IETF Proposed Standard protocol for the System for Cross-domain Identity Management (SCIM 2.0), used to request a subset of User/Group resources via a `filter` query parameter (or POST body) on a SCIM REST API. It combines ten simple attribute operators (eq, ne, co, sw, ew, pr, gt, ge, lt, le) with logical and/or/not, parenthesized grouping, and a distinctive bracketed complex-attribute filter for scoping predicates to a single value of a multi-valued attribute. As part of a mature, IETF-standardized, HTTP-native identity-provisioning protocol with broad industry adoption (Okta, Microsoft, Salesforce, and others), it scores strongly on standardization, transport compatibility, and community/ecosystem, while remaining schema-bound to the SCIM resource model rather than a general-purpose query language.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page.

```
filter=category eq "electronics" and price gt 100
```

SCIM Filter's grammar (RFC 7644 §3.4.2.2) is filter-only — sorting and pagination are separate protocol-level query parameters defined by RFC 7644 (`sortBy`/`sortOrder` and `startIndex`/`count`), not part of the filter expression language itself.

## Sources

- Hunt, P. (Ed.), Grizzle, K., Ansari, M., Wahlstroem, E., & Mortimore, C. (2015, September). [*System for Cross-domain Identity Management: Protocol (RFC 7644), Section 3.4.2.2 "Filtering"*](https://datatracker.ietf.org/doc/html/rfc7644#section-3.4.2.2). IETF.
- Wikipedia contributors. (n.d.). [*System for Cross-domain Identity Management*](https://en.wikipedia.org/wiki/System_for_Cross-domain_Identity_Management). Wikipedia.
