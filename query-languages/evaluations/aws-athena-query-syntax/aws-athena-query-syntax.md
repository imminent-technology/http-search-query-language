# AWS Athena Query Syntax

[↑ Full comparison table](../summary.md)

- **Category**: Relational/SQL-family
- **Official docs**: [SQL reference for Athena](https://docs.aws.amazon.com/athena/latest/ug/ddl-sql-reference.html)
- **Media type**: None known — requests use AWS's generic JSON RPC protocol (`application/x-amz-json-1.1`) for the whole Athena API action, not a dedicated media type for the SQL text.
- **Evaluated**: 2026-09-04

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | DML is based on Trino/Presto SQL (joins, aggregation, window functions, subqueries) while DDL is based on HiveQL, giving broad expressiveness for querying data in S3. |
| Simplicity | 4 | Familiar ANSI-SQL-like syntax for anyone who knows SQL, though mixing HiveQL-derived DDL with Trino-derived DML introduces minor inconsistencies. |
| Flexibility | 3 | Schema-on-read over S3 files (Parquet, JSON, CSV, ORC) via the Glue Data Catalog is more flexible than a fixed RDBMS schema, but tables must still be defined before querying. |
| Community and Ecosystem | 3 | Backed by AWS with solid official documentation and inherits Trino/Presto tooling, though the AWS-specific service itself has a smaller dedicated community than core SQL. |
| Extensibility | 3 | Supports user-defined functions via AWS Lambda, but extension points are narrower than in a general-purpose database engine. |
| Transport Compatibility | 2 | Primarily invoked through the AWS SDK/CLI/console or JDBC/ODBC drivers via StartQueryExecution, not designed for embedding directly in a URL query string. |
| Standardization | 2 | No formal standards body governs Athena itself; it layers AWS-specific service semantics on top of the open-source Trino SQL and HiveQL dialects. |
| Security | 3 | AWS IAM-based access control and parameterized execution via SDKs reduce risk, but ad hoc query strings built by string concatenation remain possible. |
| Performance | 4 | Serverless, distributed engine (Trino-based) that benefits from columnar formats, partitioning, and partition pruning for large-scale S3 datasets. |
| Orthogonality | 3 | Inherits reasonable SQL orthogonality, but sourcing DDL from HiveQL and DML from Trino/Presto creates some inconsistency between the two halves of the language. |

**Overall score (avg, informational only): 3.1**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.3**

## Summary

AWS Athena's query syntax is a serverless SQL dialect over S3 data, combining Trino/Presto's expressive DML with HiveQL-derived DDL for a familiar, reasonably performant analytics experience, but it remains an AWS-specific service rather than a standardized query language and is used through SDKs/APIs rather than as a URL-embeddable string.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page.

```sql
SELECT *
FROM products
WHERE category = 'electronics' AND price > 100
ORDER BY price DESC
OFFSET 10
LIMIT 10
```

Athena's DML follows Trino syntax, which evaluates `ORDER BY` before `OFFSET`/`LIMIT`, both natively supported.

## Sources

- Amazon Web Services (AWS). (n.d.). [*SQL reference for Athena*](https://docs.aws.amazon.com/athena/latest/ug/ddl-sql-reference.html).
