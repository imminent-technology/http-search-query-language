# AWS DynamoDB Query Syntax

[↑ Full comparison table](../summary.md)

- **Category**: Document/NoSQL
- **Official docs**: [Query - Amazon DynamoDB API Reference](https://docs.aws.amazon.com/amazondynamodb/latest/APIReference/API_Query.html)
- **Media type**: None known — requests use AWS's generic JSON RPC protocol (`application/x-amz-json-1.0`); no dedicated media type for DynamoDB's KeyConditionExpression syntax.
- **Evaluated**: 2026-09-04

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 2 | Query requires an equality condition on the partition key plus an optional single comparison/range/begins_with condition on the sort key, further refinable only by a post-read FilterExpression; there are no joins, aggregation, or arbitrary multi-field key conditions. |
| Simplicity | 3 | KeyConditionExpression/FilterExpression syntax is a simple string mini-language, but correct use requires DynamoDB-specific concepts (partition/sort keys, expression attribute name/value placeholders) not needed in general SQL. |
| Flexibility | 2 | Item attributes themselves are schema-less, but the Query operation is rigid, tied tightly to the table's or index's declared partition/sort key structure decided at table design time. |
| Community and Ecosystem | 4 | A flagship, widely used AWS managed NoSQL service with extensive official documentation, SDKs in most major languages, and a large body of practitioner data-modeling guidance (e.g., single-table design). |
| Extensibility | 2 | The expression language supports only a fixed set of built-in functions (begins_with, size, attribute_exists, etc.) with no user-defined functions. |
| Transport Compatibility | 3 | Invoked via a JSON request body over AWS's HTTP API (or SDKs/CLI wrapping it), so it is HTTP-native but not designed to be compactly embedded in a URL query string. |
| Standardization | 1 | A proprietary, single-vendor AWS API with no independent specification. |
| Security | 4 | ExpressionAttributeNames/Values act as required placeholders/bind parameters rather than raw string concatenation, combined with IAM-based access control, giving strong built-in injection resistance. |
| Performance | 4 | Performance is highly predictable because reads are bounded by the declared partition/sort key structure and provisioned/on-demand capacity, with the engine explicitly bypassing query planning/optimization in favor of direct hash-based partition routing. |
| Orthogonality | 2 | KeyConditionExpression, FilterExpression, and Select/ProjectionExpression each carry distinct, non-overlapping rules (e.g., FilterExpression cannot reference key attributes), reflecting documented special-casing rather than uniform composability. |

**Overall score (avg, informational only): 2.7**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 2.8**

## Summary

DynamoDB's Query API trades expressiveness and flexibility for predictable, low-latency performance at scale, requiring queries to be shaped around a table's fixed partition/sort key design with strong parameterization-based injection resistance, but with no joins, aggregation, or independent standardization.

## Sources

- Amazon Web Services (AWS). (n.d.). [*Query - Amazon DynamoDB API Reference*](https://docs.aws.amazon.com/amazondynamodb/latest/APIReference/API_Query.html).
- Wikipedia. (2026, June 11). [*Amazon DynamoDB*](https://en.wikipedia.org/wiki/Amazon_DynamoDB).
