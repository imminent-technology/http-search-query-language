# Azure Cosmos DB SQL Query Syntax

[↑ Full comparison table](../summary.md)

- **Category**: Relational/SQL-family
- **Official docs**: [Query language for Cosmos DB (in Azure and Fabric) documentation](https://learn.microsoft.com/en-us/azure/cosmos-db/nosql/query/getting-started)
- **Media type**: `application/query+json` — required `Content-Type` for SQL API query requests per Microsoft's Cosmos DB REST API documentation. Not registered with IANA, but officially documented by Microsoft.
- **Evaluated**: 2026-09-04

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 3 | Supports filtering, sorting, cross-product joins, subqueries, scalar/vector/full-text functions and aggregates (COUNT/SUM/MIN/MAX/AVG), but Wikipedia notes there is no GROUP BY or cross-container joins, requiring stored procedures for gaps. |
| Simplicity | 4 | Deliberately reuses familiar ANSI SQL keywords over JSON documents, making it easy for SQL-literate developers to pick up. |
| Flexibility | 5 | Containers are schema-agnostic JSON documents with automatic indexing by default, making the language a natural fit for dynamic and evolving data models. |
| Community and Ecosystem | 4 | Backed by Microsoft with extensive official documentation and SDKs across .NET, Node.js, Java and Python, and wide adoption within the Azure ecosystem. |
| Extensibility | 4 | The embedded JavaScript engine enables stored procedures, triggers and user-defined functions, which are explicitly used to work around gaps like missing aggregation support. |
| Transport Compatibility | 3 | Exposed as a REST API that fits naturally as an HTTP request body, though it is not designed to be compactly embedded in a URL query string. |
| Standardization | 1 | A proprietary Microsoft SQL dialect specific to Cosmos DB, with no independent specification or alternate implementations. |
| Security | 3 | SDKs support parameterized queries, but query text is still commonly built as strings, carrying similar injection risk profile to SQL if not parameterized. |
| Performance | 4 | Every field is automatically indexed by default with a tunable indexing policy, and throughput (RU/s) is provisioned specifically to bound query latency. |
| Orthogonality | 3 | Core filtering and projection compose well, but Wikipedia explicitly documents missing GROUP BY and cross-container joins as gaps requiring special-cased stored-procedure workarounds. |

**Overall score (avg, informational only): 3.4**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.6**

## Summary

Azure Cosmos DB's SQL API brings familiar ANSI SQL syntax to schema-agnostic JSON documents, offering strong flexibility and default indexing backed by Microsoft's ecosystem, but it is a single-vendor proprietary dialect with notable expressiveness gaps (no GROUP BY, no cross-container joins) that require JavaScript-based stored procedures to work around.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page.

```sql
SELECT *
FROM products p
WHERE p.category = "electronics" AND p.price > 100
ORDER BY p.price DESC
OFFSET 10 LIMIT 10
```

Cosmos DB's OFFSET/LIMIT clause requires the preceding ORDER BY (and a matching composite index) for stable, deterministic paging.

## Sources

- Microsoft. (2025, December 31). [*Query language for Cosmos DB (in Azure and Fabric) documentation*](https://learn.microsoft.com/en-us/azure/cosmos-db/nosql/query/getting-started).
- Wikipedia. (2026, April 15). [*Cosmos DB*](https://en.wikipedia.org/wiki/Cosmos_DB).
