# JQL

[↑ Full comparison table](../summary.md)

- **Category**: Search/full-text
- **Official docs**: [JQL: Get started with advanced search in Jira](https://www.atlassian.com/software/jira/guides/jql/overview)
- **Media type**: None known — Jira's REST API accepts JQL as a `jql` URL query parameter on `GET` search endpoints, or as a JSON string field in the request body on the equivalent `POST` endpoints, not a dedicated media type.
- **Evaluated**: 2026-09-07

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | A field/operator/value/keyword grammar with comparison operators (=, !=, <, <=, >, >=, ~, IN, IS EMPTY), AND/OR/NOT boolean combination, ORDER BY, and a large built-in function library (currentUser(), now(), membersOf(), WAS, CHANGED, sprint helpers, SLA helpers), but there is no join across issue types beyond linked-issue functions and no user-defined functions within a query. |
| Simplicity | 3 | Basic clauses (`priority = High AND assignee = currentUser()`) read naturally, but the function library is large and some functions restrict which operators they can pair with (e.g. cascadeOption() only supports IN/NOT IN), which is easy to get wrong without the editor's autocomplete. |
| Flexibility | 3 | JQL queries can reference any of Jira's per-project custom fields by quoted name, adapting well to Jira's configurable issue-type/field schema, but it remains scoped entirely to Jira's own issue data model rather than arbitrary data. |
| Community and Ecosystem | 4 | Jira is one of the most widely deployed enterprise issue trackers, and JQL is extensively documented with a dedicated cheat sheet, tutorials, and community-shared saved filters, plus an in-product AI assistant (Rovo) that translates natural language into JQL. |
| Extensibility | 3 | The query-writer cannot define new functions inline, but Atlassian's own docs note that "additional JQL functions may also be available through installed apps," meaning the language's function library is genuinely extensible at the Jira Marketplace/plugin layer. |
| Transport Compatibility | 4 | Passed as a `jql` URL query parameter on Jira Cloud's REST search endpoints (or a JSON body field on the POST variant for longer queries), fitting naturally into both URL query strings and request bodies. |
| Standardization | 1 | A closed, single-vendor (Atlassian) proprietary query language embedded in the Jira SaaS product, with no published formal grammar specification or independent governance body. |
| Security | 3 | Structured field/operator/value clauses avoid raw string concatenation for most queries, but the `~` text-contains operator runs against a Lucene-backed index with no documented query-complexity ceiling comparable to parameterized statements. |
| Performance | 3 | Backed by Jira's Lucene-based issue index for indexed fields, but Atlassian's own documentation and community guidance repeatedly warn that certain function-heavy or unbounded queries (e.g. broad membersOf()/organizationMembers() lookups capped at 10,000 users) can be slow or fail outright on large instances. |
| Orthogonality | 3 | The field/operator/value/keyword model is consistent, but individual functions each declare their own supported/unsupported operator subsets (clearly enumerated per-function in the docs), so the same operator does not behave uniformly across all functions and field types. |

**Overall score (avg, informational only): 3.1**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.3**

## Summary

JQL (Jira Query Language) is Atlassian's field/operator/value/keyword query language for searching and filtering issues in Jira, combining comparison operators, boolean keywords, ORDER BY, and a large built-in function library covering dates, sprints, approvals, and SLAs. It is a closed, single-vendor language with no formal specification, but its function library can be extended by installed Jira apps, and its per-project custom-field model gives it real flexibility within Jira's own issue-tracking domain.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page (adapted to JQL's issue-tracking domain via custom fields, since Jira has no built-in product catalog).

```jql
"Category" = "electronics" AND "Price" > 100 ORDER BY "Price" DESC
```

JQL itself has no LIMIT/OFFSET or paging syntax; pagination (page 2 of 10) is controlled entirely by the surrounding REST API's request parameters (e.g. `startAt`/`maxResults` or a cursor token), not by the JQL query string itself.

## Sources

- Atlassian. (n.d.). [*The Jira Query Language (JQL) cheat sheet*](https://www.atlassian.com/software/jira/guides/jql/cheat-sheet).
- Atlassian. (n.d.). [*JQL functions*](https://support.atlassian.com/jira-software-cloud/docs/jql-functions/).
