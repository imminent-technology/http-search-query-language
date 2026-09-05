# Query language comparison

Methodology: each language is scored 1-5 on the 10 criteria defined in [`../evaluation.md`](../evaluation.md), using the rubric in [`rubric.md`](rubric.md). Scores are descriptive snapshots intended as raw research material for a comparison article — not a ranking or a "best language" verdict. Each table below also reports a Design Quality Score (`DQ`), a second, additive average over only 8 of the 10 criteria that excludes Community & Ecosystem and Standardization — see [`rubric.md`](rubric.md) for why.

**Status: 43 of 43 languages evaluated.** (pilot batch + Relational/SQL-family batch + Document/NoSQL batch + Search/full-text & Graph batch + Analytics/Observability & JSON Query Language batch + Language-integrated/Log-security-search/Scripting/Path-document-navigation/Niche-misc/API-data-fetching-remainder batch + JSON Query Language (christosgkoros) name-collision addition + OData addition + JSONPath addition). Note: an earlier miscount stated the project total as 39 languages; a full recount of `list.csv` confirmed the true total is 40, and it has since grown to 43 with the addition of a second, unrelated "JSON Query Language" spec and, subsequently, OData and JSONPath.

Legend: Exp=Expressiveness, Sim=Simplicity, Flex=Flexibility, Comm=Community & Ecosystem, Ext=Extensibility, Trans=Transport Compatibility, Std=Standardization, Sec=Security, Perf=Performance, Orth=Orthogonality, Avg=overall average (informational only), DQ=Design Quality Score (avg of the 8 criteria excluding Community & Ecosystem and Standardization).

## Relational/SQL-family

| Language | Exp | Sim | Flex | Comm | Ext | Trans | Std | Sec | Perf | Orth | Avg | DQ |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| [SQL](sql/sql.md) | 5 | 3 | 2 | 5 | 4 | 2 | 5 | 2 | 5 | 3 | 3.6 | 3.3 |
| [HQL](hql/hql.md) | 4 | 4 | 2 | 4 | 3 | 1 | 3 | 4 | 3 | 3 | 3.1 | 3.0 |
| [JPQL](jpql/jpql.md) | 4 | 4 | 2 | 4 | 3 | 1 | 5 | 4 | 3 | 3 | 3.3 | 3.0 |
| [Criteria API](criteria-api/criteria-api.md) | 4 | 2 | 2 | 4 | 3 | 1 | 5 | 5 | 3 | 3 | 3.2 | 2.9 |
| [SOQL](soql/soql.md) | 3 | 4 | 2 | 3 | 2 | 4 | 1 | 3 | 3 | 3 | 2.8 | 3.0 |
| [SQL++](sql-plus-plus/sql-plus-plus.md) | 4 | 3 | 5 | 2 | 3 | 3 | 2 | 2 | 3 | 3 | 3.0 | 3.3 |
| [Azure Cosmos DB SQL Query Syntax](azure-cosmos-db-sql-query-syntax/azure-cosmos-db-sql-query-syntax.md) | 3 | 4 | 5 | 4 | 4 | 3 | 1 | 3 | 4 | 3 | 3.4 | 3.6 |
| [AWS Athena Query Syntax](aws-athena-query-syntax/aws-athena-query-syntax.md) | 4 | 4 | 3 | 3 | 3 | 2 | 2 | 3 | 4 | 3 | 3.1 | 3.3 |

## Document/NoSQL

| Language | Exp | Sim | Flex | Comm | Ext | Trans | Std | Sec | Perf | Orth | Avg | DQ |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| [MongoDB Query Syntax](mongodb-query-syntax/mongodb-query-syntax.md) | 4 | 4 | 5 | 5 | 3 | 2 | 1 | 3 | 3 | 4 | 3.4 | 3.5 |
| [CouchDB Mango Query Language](couchdb-mango-query-language/couchdb-mango-query-language.md) | 3 | 4 | 4 | 3 | 2 | 5 | 1 | 3 | 3 | 3 | 3.1 | 3.4 |
| [Firebase Cloud Firestore Query Language](firebase-cloud-firestore-query-language/firebase-cloud-firestore-query-language.md) | 3 | 4 | 4 | 4 | 2 | 3 | 1 | 4 | 4 | 3 | 3.2 | 3.4 |
| [Firebase Realtime Database Query Language](firebase-realtime-database-query-language/firebase-realtime-database-query-language.md) | 2 | 4 | 3 | 3 | 1 | 3 | 1 | 3 | 3 | 2 | 2.5 | 2.6 |
| [AWS DynamoDB Query Syntax](aws-dynamodb-query-syntax/aws-dynamodb-query-syntax.md) | 2 | 3 | 2 | 4 | 2 | 3 | 1 | 4 | 4 | 2 | 2.7 | 2.8 |
| [AQL](aql/aql.md) | 4 | 3 | 5 | 2 | 3 | 2 | 1 | 3 | 3 | 3 | 2.9 | 3.3 |
| [CQL](cql/cql.md) | 2 | 4 | 3 | 4 | 3 | 1 | 1 | 3 | 4 | 2 | 2.7 | 2.8 |

## Search/full-text

| Language | Exp | Sim | Flex | Comm | Ext | Trans | Std | Sec | Perf | Orth | Avg | DQ |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| [Lucene Query Syntax](lucene-query-syntax/lucene-query-syntax.md) | 3 | 4 | 3 | 5 | 2 | 5 | 1 | 3 | 5 | 3 | 3.4 | 3.5 |
| [Solr Query Syntax](solr-query-syntax/solr-query-syntax.md) | 4 | 3 | 3 | 4 | 3 | 5 | 1 | 2 | 5 | 3 | 3.3 | 3.5 |
| [ESQL](esql/esql.md) | 4 | 3 | 4 | 5 | 3 | 4 | 1 | 2 | 5 | 3 | 3.4 | 3.5 |
| [AWS CloudSearch Query Syntax](aws-cloudsearch-query-syntax/aws-cloudsearch-query-syntax.md) | 3 | 3 | 2 | 2 | 2 | 5 | 1 | 3 | 3 | 2 | 2.6 | 2.9 |

## Graph

| Language | Exp | Sim | Flex | Comm | Ext | Trans | Std | Sec | Perf | Orth | Avg | DQ |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| [Cypher](cypher/cypher.md) | 5 | 4 | 4 | 4 | 3 | 2 | 4 | 3 | 4 | 4 | 3.7 | 3.6 |
| [Gremlin](gremlin/gremlin.md) | 5 | 3 | 4 | 3 | 4 | 2 | 3 | 2 | 4 | 4 | 3.4 | 3.5 |
| [SPARQL](sparql/sparql.md) | 5 | 2 | 4 | 3 | 3 | 4 | 5 | 2 | 3 | 4 | 3.5 | 3.4 |
| [Datalog](datalog/datalog.md) | 3 | 2 | 4 | 2 | 4 | 1 | 2 | 3 | 3 | 4 | 2.8 | 3.0 |

## Analytics/Observability

| Language | Exp | Sim | Flex | Comm | Ext | Trans | Std | Sec | Perf | Orth | Avg | DQ |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| [PromQL](promql/promql.md) | 4 | 3 | 2 | 5 | 2 | 4 | 2 | 3 | 4 | 3 | 3.2 | 3.1 |
| [KQL](kql/kql.md) | 4 | 4 | 3 | 4 | 3 | 3 | 1 | 4 | 4 | 4 | 3.4 | 3.6 |
| [NRQL](nrql/nrql.md) | 3 | 4 | 3 | 3 | 2 | 4 | 1 | 2 | 3 | 3 | 2.8 | 3.0 |
| [DQL](dql/dql.md) | 4 | 3 | 5 | 3 | 3 | 3 | 1 | 2 | 4 | 4 | 3.2 | 3.5 |
| [DAX](dax/dax.md) | 4 | 3 | 2 | 4 | 2 | 2 | 1 | 3 | 4 | 3 | 2.8 | 2.9 |
| [MDX](mdx/mdx.md) | 4 | 2 | 2 | 3 | 3 | 3 | 3 | 2 | 4 | 3 | 2.9 | 2.9 |

## API/data-fetching

| Language | Exp | Sim | Flex | Comm | Ext | Trans | Std | Sec | Perf | Orth | Avg | DQ |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| [GraphQL](graphql/graphql.md) | 4 | 4 | 4 | 5 | 4 | 4 | 4 | 4 | 3 | 4 | 4.0 | 3.9 |
| [JSON Query Language](json-query-language/json-query-language.md) | 3 | 4 | 5 | 1 | 4 | 2 | 1 | 4 | 3 | 4 | 3.1 | 3.6 |
| [JSON Query Language (christosgkoros)](json-query-language-christosgkoros/json-query-language-christosgkoros.md) | 4 | 3 | 4 | 1 | 4 | 3 | 1 | 4 | 3 | 3 | 3.0 | 3.5 |
| [FQL](fql/fql.md) | 2 | 4 | 1 | 1 | 1 | 4 | 1 | 2 | 2 | 3 | 2.1 | 2.4 |
| [TaxiQL](taxiql/taxiql.md) | 4 | 3 | 4 | 1 | 4 | 2 | 1 | 2 | 2 | 3 | 2.6 | 3.0 |
| [OData](odata/odata.md) | 4 | 3 | 2 | 4 | 4 | 5 | 5 | 3 | 3 | 4 | 3.7 | 3.5 |

## Language-integrated

| Language | Exp | Sim | Flex | Comm | Ext | Trans | Std | Sec | Perf | Orth | Avg | DQ |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| [LINQ](linq/linq.md) | 5 | 4 | 5 | 4 | 5 | 1 | 3 | 3 | 2 | 4 | 3.6 | 3.6 |

## Log/security search

| Language | Exp | Sim | Flex | Comm | Ext | Trans | Std | Sec | Perf | Orth | Avg | DQ |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| [SPL](spl/spl.md) | 5 | 3 | 4 | 5 | 4 | 3 | 1 | 2 | 4 | 3 | 3.4 | 3.5 |

## Scripting

| Language | Exp | Sim | Flex | Comm | Ext | Trans | Std | Sec | Perf | Orth | Avg | DQ |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| [Flux](flux/flux.md) | 4 | 3 | 4 | 3 | 3 | 3 | 1 | 2 | 3 | 4 | 3.0 | 3.3 |

## Path/document navigation

| Language | Exp | Sim | Flex | Comm | Ext | Trans | Std | Sec | Perf | Orth | Avg | DQ |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| [XPath](xpath/xpath.md) | 4 | 4 | 3 | 5 | 3 | 2 | 5 | 2 | 3 | 4 | 3.5 | 3.1 |
| [XQuery](xquery/xquery.md) | 5 | 3 | 4 | 3 | 4 | 2 | 5 | 2 | 3 | 4 | 3.5 | 3.4 |
| [JSONPath](jsonpath/jsonpath.md) | 4 | 4 | 5 | 3 | 4 | 3 | 5 | 3 | 3 | 4 | 3.8 | 3.8 |

## Niche/misc

| Language | Exp | Sim | Flex | Comm | Ext | Trans | Std | Sec | Perf | Orth | Avg | DQ |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| [Crul Queries](crul-queries/crul-queries.md) | 2 | 4 | 3 | 1 | 2 | 2 | 1 | 2 | 2 | 4 | 2.3 | 2.6 |
| [OQL](oql/oql.md) | 2 | 3 | 2 | 1 | 1 | 2 | 2 | 2 | 2 | 3 | 2.0 | 2.1 |

## Observations so far (partial data, not yet conclusive)

- **Transport Compatibility splits cleanly by design era/intent.** Languages built around persistent driver/wire-protocol or in-process connections (Cypher, HQL, JPQL, Criteria API, CQL, MongoDB, Datalog, LINQ) score lowest (1-2) — LINQ's score of 1 is the most extreme case, since it's an in-language construct with no network transport at all — while languages designed for HTTP-native access (Lucene, CouchDB Mango, GraphQL, PromQL, SOQL) score highest (4-5) — a real tradeoff between "designed for a database driver" and "designed for HTTP".
- **Standardization is rare outside SQL's own family, but not unique to it.** SQL and Jakarta Persistence (JPQL, Criteria API) are joined by three W3C recommendations (SPARQL, XPath, XQuery), two industry-consortium specs (Cypher via openCypher/GQL, GraphQL via the GraphQL Foundation), and an OASIS/ISO standard (OData, later approved as ISO/IEC 20802) in scoring above 3 on Standardization — see the full breakdown near the end of this list. Every proprietary single-vendor language evaluated (DynamoDB, Firestore, RTDB, AQL, CQL, Cosmos DB SQL, SOQL, and roughly 20 others) scores 1, regardless of how mature or widely used the underlying database is.
- **Schema flexibility and query expressiveness trade off in the NoSQL/Document group — though not uniformly.** The most flexible, schema-less languages (SQL++, Cosmos DB SQL, AQL, MongoDB — all scoring 5 or 4 on Flexibility) mostly accept real expressiveness limits elsewhere (e.g., Cosmos DB SQL's missing GROUP BY/cross-container joins); MongoDB is the exception, pairing high Flexibility (5) with the category's best Orthogonality (4). At the opposite end, DynamoDB's rigid partition/sort-key-bound Query operation and CQL's explicit lack of joins/aggregation show what happens when a document/wide-column store's query language stays deliberately narrow instead of flexible.
- **Only one language across the entire dataset, the JPA Criteria API, scores a perfect 5 on Security** — by virtue of being structurally immune to injection through typed Java objects rather than string queries. Every other language tops out at 4 (HQL, JPQL, Firestore, DynamoDB, GraphQL, KQL, JSON Query Language, and JSON Query Language (christosgkoros)), reinforcing that weak default injection resistance is a near-universal weak spot across query languages, not specific to any one family.
- **Community/ecosystem strength doesn't require standardization.** MongoDB (5) and DynamoDB (4) are both single-vendor/proprietary (standardization=1) yet have some of the largest developer communities evaluated, and SPL (5, Splunk, standardization=1) reinforces the pattern from a completely different category (Log/security search) — showing market adoption and formal standardization are largely independent axes.
- **Search-engine query dialects (Lucene, Solr, ESQL/Elasticsearch, AWS CloudSearch) cluster tightly on Transport Compatibility (4-5) and Performance (3-5), but bottom out on Standardization (all scoring 1).** Each is HTTP-native by design and built on (or closely derived from) an inverted-index engine, yet every one is a single-vendor or single-project syntax with no independent standards body.
- **Graph query languages show a wide internal spread, though not the widest once the full dataset is in.** Cypher, Gremlin, SPARQL, and Datalog range from 2.8 to 3.7 overall (a 0.9-point spread), split largely by Transport Compatibility (SPARQL's dedicated HTTP protocol scores 4 vs. Datalog's in-process-only evaluation scoring 1) and Standardization (SPARQL's formal W3C recommendation scores 5 vs. proprietary syntaxes scoring 1-3) — showing that within a single problem domain, governance model matters as much as the underlying data model. The API/data-fetching category ends up with the widest spread of any category overall (1.9 points, GraphQL's 4.0 down to FQL's 2.1), since an actively-governed, HTTP-native modern standard and a long-dead, single-vendor relic ended up sharing a category defined only by *what* they query, not *how well* they do it.
- **Orthogonality correlates with a small, uniform set of composition primitives rather than raw expressiveness.** Datalog (facts + Horn-clause rules), Gremlin (map/filter/sideEffect steps), XPath/XQuery (a single axis-and-predicate navigation model), and Flux (a uniform pipe-forward operator) all score 4 on Orthogonality despite Expressiveness scores ranging from 3 to 5, while search-engine query-string dialects (Solr, ESQL, Lucene) consistently score only 3, reflecting their layered, exception-laden grammars built up over many feature additions.
- **Pipe-based observability languages (PromQL, KQL, DQL) generally match or outscore the SQL-style observability language (NRQL) on Orthogonality (3-4 vs. 3) and Flexibility (2-5 vs. 3), though PromQL's own Flexibility (2) actually trails NRQL's (3).** Security tells a similarly mixed story: KQL's documented, explicit anti-injection design (a required `.` prefix on management commands) earns it the cluster's high score (4), but PromQL (3) also clears the cluster's low bar, leaving only DQL and NRQL (2 each) without any documented injection-specific mitigation — suggesting that most observability query languages, despite being newer than SQL, have made only partial, inconsistent progress on SQL's own weak default injection resistance.
- **A language's proprietary, single-vendor status does not by itself predict its Simplicity or Orthogonality.** KQL and DQL (both single-vendor, Standardization=1) score as well or better on Simplicity/Orthogonality than MDX, a decades-old de facto cross-vendor standard (Standardization=3) — showing that governance model and ease-of-use/composability are largely independent axes, echoing the earlier observation that community strength doesn't require standardization.
- **MDX is not alone in occupying an informal middle tier between formal standards-body governance and pure single-vendor proprietary syntax.** Its score of 3 reflects a de facto (not de jure) standard status achieved purely through broad multi-vendor adoption (Microsoft, Hyperion, SAP) and later partial formalization via the XMLA Council's XML for Analysis spec — but Gremlin and LINQ also land at 3 (via Apache TinkerPop's open governance and multi-provider adoption within .NET, respectively), while PromQL and OQL land at 2 (CNCF project governance and vendor-specific product-documentation depth). None of these four reach a globally-recognized standards body's formal recommendation, yet all score above the '1' floor that most fully single-vendor languages sit at — showing this middle tier is a real, if inconsistent, phenomenon rather than an MDX-only curiosity.
- **JSON Query Language is the first language evaluated whose documentation explicitly names "security" as a design motivation**, citing the injection risk of executing arbitrary JavaScript (as in JS+Lodash-based JSON querying) and deliberately blocking access to object methods/class properties — a rare case of a query language's minimal feature set being a direct, stated security tradeoff rather than an accidental byproduct of simplicity.
- **LINQ is one of several languages whose above-average Security score comes from typed, structural query construction rather than from restricting the feature set** — joining the JPA Criteria API (5) and Firestore's SDKs (4), both cited explicitly for building queries from typed objects/method calls instead of string concatenation, and GraphQL (4), whose strongly-typed schema validates queries before execution. LINQ's own compile-time-checked query expressions give it a natural resistance to string-injection attacks (score 3) without sacrificing Expressiveness (5) or Extensibility (5) — notably lower than Criteria API/Firestore/GraphQL despite the shared mechanism, since LINQ providers (e.g., Dynamic LINQ) can still reintroduce string-based query construction that the others don't allow. This typed-construction route is distinct from the grammar-restriction route taken by KQL (a required `.` prefix on management commands) and JSON Query Language (blocking access to object methods/class properties), both also scoring 4.
- **A fully deprecated language can still be meaningfully evaluated, and FQL is the clearest case of a rubric built for comparison, not just endorsement.** FQL's Community/Ecosystem, Extensibility, and Flexibility (1, 1, 1) are frozen at the moment Facebook shut down the API in 2016, while its Transport Compatibility (4, genuinely URL-native via `/fql?q=`) and Simplicity (4, plain SQL-style syntax) remain intact — showing that a language's inherent design qualities and its real-world viability are separate axes that can diverge completely.
- **XPath, XQuery, and JSONPath join SQL, JPQL, the Criteria API, SPARQL, and OData as the only languages in the dataset scoring a full 5 on Standardization** (each via a genuine, formal standards-body recommendation — ANSI/ISO for SQL, Jakarta Persistence for JPQL/Criteria API, W3C for SPARQL/XPath/XQuery, IETF for JSONPath, and OASIS/ISO for OData) **— yet XPath/XQuery's Transport Compatibility remains low (2) despite that maturity.** Unlike SPARQL, which was designed from the outset with a dedicated HTTP protocol (SPARQL Protocol) and scores 4, XPath/XQuery were conceived as embedded/API-invoked languages (for XSLT, database engines, and language bindings) rather than as network-native query mechanisms — showing that formal standardization does not by itself imply HTTP-nativeness. OData reinforces the same point from the opposite direction: it pairs that same top Standardization score with the dataset's highest possible Transport Compatibility (5), since URL query-string conventions were part of its core design brief from the start. JSONPath lands in between (Transport Compatibility 3): it has an IANA-registered media type (`application/jsonpath`) but is mostly consumed as an embedded library/CLI convention rather than a documented URL query-string mechanism, unlike OData's from-the-start HTTP orientation. (MDX's Standardization score of 3 is a lower, de facto tier — see above — and shouldn't be confused with this group's formal W3C/ISO/OASIS/IETF/Jakarta governance.)
- **The OQL and ESQL cases (Batches 3 and 5) both illustrate a recurring risk in this dataset: a query language's common/historical name and its actually-linked, product-specific implementation can refer to genuinely different things.** In both cases, the project chose to evaluate what was actually linked in `list.csv` (a narrower, vendor-specific dialect) while citing the more famous, broader concept's Wikipedia article for historical/standardization context — a pattern worth flagging to readers of any future comparison article so they don't conflate the two.
- **Across all 43 languages, 10 score a 4 or 5 on Standardization: SQL (5), JPQL and the Criteria API (5 each, via Jakarta Persistence), Cypher (4, via openCypher/GQL), GraphQL (4, via the GraphQL Foundation spec), SPARQL/XPath/XQuery (5 each, via W3C), OData (5, via its OASIS Standard status, later approved as ISO/IEC 20802), and JSONPath (5, via its IETF RFC 9535 status as an Internet Standards Track Proposed Standard).** A further 9 (HQL, MDX, Gremlin, LINQ at 3; SQL++, AWS Athena, PromQL, Datalog, OQL at 2) sit in a middle, semi-formal tier. The remaining 24 score a flat 1, meaning 24 of 43 (56%) have no standardization beyond a single vendor's own documentation — reinforcing that formal, vendor-neutral standardization is the exception rather than the norm across the query-language landscape as a whole.
- **The highest overall score in the dataset is GraphQL (4.0)** — the only language to score 4 or above on nine of the ten criteria simultaneously (every criterion except Performance, which sits at 3) — while the lowest is OQL (2.0), whose scores reflect a narrow, single-vendor, low-adoption tool-specific dialect bearing only a name in common with a more ambitious but never-fully-implemented standard.

## Media types

Media type for the query/request body when the language is transmitted over HTTP, verified against the [IANA Media Types registry](https://www.iana.org/assignments/media-types/media-types.xhtml) and each vendor's/standard body's own official documentation. Not inferred: languages with no verifiable registered or documented media type are marked "None known".

| Language | Media type |
|---|---|
| [SQL](sql/sql.md) | `application/sql` — IANA-registered, RFC 6922. |
| [HQL](hql/hql.md) | Not applicable — HQL is parsed and translated to SQL inside the JVM by Hibernate; it is not transmitted over HTTP with its own media type. |
| [JPQL](jpql/jpql.md) | Not applicable — like HQL, JPQL is used internally by the JPA provider and is not transmitted over HTTP with a dedicated media type. |
| [Criteria API](criteria-api/criteria-api.md) | Not applicable — the Criteria API is a Java object-graph API for building queries programmatically; it has no serialized wire format. |
| [SOQL](soql/soql.md) | None known — submitted as a URL-encoded `q` query-string parameter on Salesforce's REST API. |
| [SQL++](sql-plus-plus/sql-plus-plus.md) | None known — Couchbase's Query REST API accepts SQL++/N1QL as a `"statement"` field inside a generic `application/json` body. |
| [Azure Cosmos DB SQL Query Syntax](azure-cosmos-db-sql-query-syntax/azure-cosmos-db-sql-query-syntax.md) | `application/query+json` — required `Content-Type` for SQL API query requests per Microsoft's Cosmos DB REST API documentation. Not registered with IANA, but officially documented by Microsoft. |
| [AWS Athena Query Syntax](aws-athena-query-syntax/aws-athena-query-syntax.md) | None known — requests use AWS's generic JSON RPC protocol (`application/x-amz-json-1.1`) for the whole Athena API action, not a dedicated media type for the SQL text. |
| [MongoDB Query Syntax](mongodb-query-syntax/mongodb-query-syntax.md) | None known — MongoDB's wire protocol uses BSON, and the Atlas Data API wraps queries in generic `application/json`. |
| [CouchDB Mango Query Language](couchdb-mango-query-language/couchdb-mango-query-language.md) | None known — Mango selectors are POSTed as a JSON document to `/db/_find` using the generic `application/json` media type. |
| [Firebase Cloud Firestore Query Language](firebase-cloud-firestore-query-language/firebase-cloud-firestore-query-language.md) | None known — Firestore queries are structured protobuf/JSON (`StructuredQuery`) sent via gRPC or the REST API's generic `application/json`. |
| [Firebase Realtime Database Query Language](firebase-realtime-database-query-language/firebase-realtime-database-query-language.md) | None known — query parameters are passed via the URL query string on the REST API; responses use generic `application/json`. |
| [AWS DynamoDB Query Syntax](aws-dynamodb-query-syntax/aws-dynamodb-query-syntax.md) | None known — requests use AWS's generic JSON RPC protocol (`application/x-amz-json-1.0`); no dedicated media type for DynamoDB's KeyConditionExpression syntax. |
| [AQL](aql/aql.md) | None known — ArangoDB's HTTP API wraps AQL queries in a generic `application/json` request body; no dedicated media type exists. |
| [CQL](cql/cql.md) | None known for Cassandra's CQL — statements are normally sent over Cassandra's native binary protocol, not HTTP. Note: IANA's registered `text/cql` media type belongs to HL7's unrelated Clinical Quality Language, and OGC defines a separate, also-unrelated CQL for geospatial filtering; neither refers to Cassandra Query Language. |
| [GraphQL](graphql/graphql.md) | `application/graphql-response+json` (responses) and `application/json` (requests) per the GraphQL-over-HTTP specification (graphql.github.io/graphql-over-http). Not registered with IANA. (A legacy, non-standard `application/graphql` convention for raw request bodies exists in some older server implementations but is not part of any official spec.) |
| [PromQL](promql/promql.md) | None known — Prometheus's HTTP API accepts PromQL as a URL query parameter or `application/x-www-form-urlencoded` field, not a dedicated media type. |
| [KQL](kql/kql.md) | None known — KQL text is submitted as a JSON field inside a generic `application/json` body via the Azure Data Explorer/Log Analytics REST APIs. |
| [NRQL](nrql/nrql.md) | None known — NRQL strings are submitted as a field inside a GraphQL request (`application/json`) to New Relic's NerdGraph API. |
| [DQL](dql/dql.md) | None known — Dynatrace's Grail Query REST API accepts DQL as a JSON field within a generic `application/json` body. |
| [DAX](dax/dax.md) | None known — DAX queries are submitted inside a generic `application/json` body via the Power BI/Analysis Services REST APIs. |
| [MDX](mdx/mdx.md) | None known — MDX statements are typically embedded in a SOAP/XML request (`text/xml`/`application/soap+xml`) to an XMLA endpoint; no dedicated MDX media type. |
| [JSON Query Language](json-query-language/json-query-language.md) | None known — no registered or documented media type found for this specification (jsonquerylang.org). |
| [JSON Query Language (christosgkoros)](json-query-language-christosgkoros/json-query-language-christosgkoros.md) | None known — filter objects are embedded as a JSON Schema-validated field within a generic `application/json` request body; no dedicated media type is registered or documented for the predicate language itself. |
| [Lucene Query Syntax](lucene-query-syntax/lucene-query-syntax.md) | None known — Lucene query strings are embedded as plain text inside the `q` parameter of systems (Solr, Elasticsearch) that wrap it in their own generic JSON APIs. |
| [Solr Query Syntax](solr-query-syntax/solr-query-syntax.md) | None known — Solr accepts query strings as URL parameters or within the JSON Request API's generic `application/json`. |
| [ESQL](esql/esql.md) | None known — Elasticsearch's Query DSL/ES\|QL requests use the generic `application/json` content type. |
| [AWS CloudSearch Query Syntax](aws-cloudsearch-query-syntax/aws-cloudsearch-query-syntax.md) | None known — queries are passed as URL query-string parameters (`q`, `q.parser`) on the CloudSearch search endpoint; no dedicated media type. |
| [Cypher](cypher/cypher.md) | None known — openCypher/Neo4j statements travel over the Bolt protocol or are wrapped in generic `application/json` via Neo4j's HTTP query API; no dedicated Cypher media type. |
| [Gremlin](gremlin/gremlin.md) | None known — no documented or registered media type for Gremlin scripts could be verified. |
| [SPARQL](sparql/sparql.md) | `application/sparql-query` — IANA-registered per the W3C SPARQL 1.1 Protocol. Query results use the related, also IANA-registered `application/sparql-results+xml` / `application/sparql-results+json`. |
| [Datalog](datalog/datalog.md) | `application/vnd.datalog` — registered in the IANA Media Types registry (registrant: Simon Johnston). |
| [Crul Queries](crul-queries/crul-queries.md) | None known — no verifiable, actively documented standard or registered media type could be found for this query language. |
| [Flux](flux/flux.md) | `application/vnd.flux` — documented `Content-Type` for Flux query requests to InfluxDB's `/api/v2/query` endpoint (InfluxData documentation). Not registered with IANA. |
| [FQL](fql/fql.md) | None known — the (now-deprecated) Facebook Query Language was submitted as a `q` parameter of Facebook's Graph API using generic form/JSON encoding; the feature has been retired. |
| [LINQ](linq/linq.md) | Not applicable — LINQ is a .NET language-integrated query syntax compiled into expression trees at compile time; it has no independent wire format. |
| [OQL](oql/oql.md) | None known — no registered or documented media type could be verified. |
| [SPL](spl/spl.md) | None known — submitted as a `search` form field via Splunk's REST API (`application/x-www-form-urlencoded`). |
| [TaxiQL](taxiql/taxiql.md) | None known — no registered or documented media type could be verified. |
| [OData](odata/odata.md) | `application/json` with OData-specific parameters (e.g. `odata.metadata=minimal\|full\|none`) per the OData JSON Format v4.01 spec. No dedicated `application/odata+json` (or similar) media type is registered with IANA. |
| [XPath](xpath/xpath.md) | None known — no IANA-registered media type exists; XPath expressions are normally embedded within another document (XSLT, XQuery, WebDAV SEARCH request bodies) rather than transmitted standalone. |
| [XQuery](xquery/xquery.md) | None known / not registered — despite XQuery being a mature W3C Recommendation, no `application/xquery` (or similar) media type is registered with IANA. |
| [JSONPath](jsonpath/jsonpath.md) | `application/jsonpath` — IANA-registered, RFC 9535 §3.1 (intended usage: COMMON). |
