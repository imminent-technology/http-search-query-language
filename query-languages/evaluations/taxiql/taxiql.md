# TaxiQL

[↑ Full comparison table](../summary.md)

- Category: API/data-fetching
- Official docs: [taxilang/taxilang](https://github.com/taxilang/taxilang)
- Media type: None known — no registered or documented media type could be verified.
- Evaluated: 2026-09-04

> Note: No independent secondary source (e.g. Wikipedia) exists for this small open-source project, so this evaluation is single-sourced from its GitHub repository/documentation.

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | Built on Taxi's rich semantic type system (types can "inherit" from primitives and carry meaning, e.g. distinguishing a CustomerId from a generic String), letting TaxiQL describe API operations and cross-system data relationships more richly than typical schema languages. |
| Simplicity | 3 | Readability is an explicit language goal ("A familiar syntax that should be easy to write, and easy to understand"), but semantic-type modeling as a paradigm requires real learning investment beyond typical schema or query languages. |
| Flexibility | 4 | Designed to bridge multiple protocol/schema formats — OpenAPI, RAML, JsonSchema, Protobuf, databases, message queues, and serverless functions — rather than being tied to one data source or format. |
| Community and Ecosystem | 1 | A small open-source project (199 GitHub stars, 7 forks, roughly a dozen contributors) primarily tied to the commercial Orbital product ecosystem, with limited broader adoption. |
| Extensibility | 4 | Extensibility is an explicit language goal: "Taxi allows you to refine and compose API schemas, adding context, annotations, and improving type signatures." |
| Transport Compatibility | 2 | TaxiQL queries are resolved by a separate query engine (such as Orbital) against underlying APIs and data sources, rather than being a native URL/HTTP query format in its own right. |
| Standardization | 1 | A single open-source project's own bespoke language with no independent standards body, competing conceptually with the much more widely adopted OpenAPI specification. |
| Security | 2 | No explicit security-design discussion is documented; as a query/orchestration layer that resolves and stitches together calls to arbitrary underlying APIs, its risk profile depends heavily on the security of those downstream systems. |
| Performance | 2 | No independent performance data is documented; performance is largely inherited from whatever underlying APIs and data sources TaxiQL orchestrates. |
| Orthogonality | 3 | A consistent model-based approach where types inherit from other types and operations reference those types, though as a hybrid schema-and-query language it lacks the small, uniform composition primitives seen in more focused query languages. |

**Overall score (avg, informational only): 2.6**

## Summary

TaxiQL is the query layer of Taxi, a semantic type/schema language designed to bridge OpenAPI, RAML, databases, message queues, and more without requiring GraphQL-style resolvers, offering genuinely rich and extensible cross-system type modeling, but it remains a small open-source project with limited community adoption, no independent standardization, and no native HTTP transport mechanism of its own.

## Sources

- Taxi Lang project (Orbital). (n.d.). [*taxilang/taxilang*](https://github.com/taxilang/taxilang).
