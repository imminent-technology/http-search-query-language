# CQL

[↑ Full comparison table](../summary.md)

- **Category**: Document/NoSQL
- **Official docs**: [The Cassandra Query Language (CQL)](https://cassandra.apache.org/doc/latest/cassandra/cql/)
- **Media type**: None known for Cassandra's CQL — statements are normally sent over Cassandra's native binary protocol, not HTTP. Note: IANA's registered `text/cql` media type belongs to HL7's unrelated Clinical Quality Language, and OGC defines a separate, also-unrelated CQL for geospatial filtering; neither refers to Cassandra Query Language.
- **Evaluated**: 2026-09-04

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 2 | Deliberately SQL-like SELECT/INSERT/UPDATE/DELETE syntax, but Wikipedia explicitly notes Cassandra "does not support advanced query patterns such as multi-table JOINs, ad hoc aggregations, or complex queries" by design. |
| Simplicity | 4 | Close resemblance to familiar SQL syntax (CREATE KEYSPACE/TABLE, SELECT, INSERT) makes it easy to pick up for anyone with relational database experience. |
| Flexibility | 3 | Supports flexible, sparse-column rows and user-defined types, with tables that can be created/altered at runtime without blocking, but query patterns must be designed around the partition/clustering key structure fixed at table-creation time. |
| Community and Ecosystem | 4 | Apache Cassandra is a long-established (2008), Apache Software Foundation top-level project with a large ecosystem, official documentation, and drivers for Java, Python, Node.js, Go, and C++. |
| Extensibility | 3 | Supports user-defined types, functions (UDFs/UDAs), and secondary indexes, but the query language's core capabilities are fixed by the engine's partitioned-row storage model. |
| Transport Compatibility | 1 | Used exclusively via CQL-native binary protocol drivers (cqlsh, language drivers) inside applications, with no notion of URL or HTTP-based transport. |
| Standardization | 1 | A single-project, Apache-governed but not independently standardized language, with no external standards body or competing implementations of the CQL specification itself. |
| Security | 3 | Parameterized statements via drivers are standard practice, giving protection comparable to prepared SQL statements, though this depends on correct client-side usage. |
| Performance | 4 | Purpose-built around an LSM-tree storage engine optimized for very high write throughput and linear scalability by adding nodes, explicitly prioritizing availability/partition tolerance over strict consistency. |
| Orthogonality | 2 | SELECT/INSERT/UPDATE syntax looks SQL-like, but requiring queries to be modeled around a fixed partition/clustering key, and the explicit lack of joins/aggregation, means the language does not compose as freely as SQL across arbitrary query shapes. |

**Overall score (avg, informational only): 2.7**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 2.8**

## Summary

CQL brings a familiar, easy-to-learn SQL-like syntax to Cassandra's wide-column, partition-oriented data model, backed by a mature Apache Software Foundation project and strong write-throughput performance, but it deliberately omits joins, ad hoc aggregation, and any HTTP/URL transport, requiring queries to be designed around a table's fixed key structure.

## Sources

- Apache Software Foundation. (n.d.). [*The Cassandra Query Language (CQL)*](https://cassandra.apache.org/doc/stable/cassandra/developing/cql/index.html).
- Wikipedia. (2026, March 17). [*Apache Cassandra*](https://en.wikipedia.org/wiki/Apache_Cassandra).
