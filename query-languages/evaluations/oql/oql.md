# OQL

[↑ Full comparison table](../summary.md)

- Category: Niche/misc
- Official docs: [Object Query Language](https://www.ibm.com/docs/en/networkmanager/4.2.0?topic=reference-object-query-language)
- Media type: None known — no registered or documented media type could be verified.
- Evaluated: 2026-09-04

> Note: list.csv's officialDocUrl documents IBM Tivoli Network Manager's proprietary OQL dialect, a tool-specific SQL-like configuration language. This is a different thing from the ODMG's (Object Data Management Group) "Object Query Language" standard for object-oriented databases that Wikipedia primarily describes — evaluated here for context, but the actual scores below reflect the IBM dialect actually linked, per the project's established pattern of evaluating what list.csv links while noting discrepancies.

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 2 | IBM's documented dialect supports basic SQL-style statements (select, insert, update, delete, subqueries, conditional tests) scoped to configuring and querying IBM Network Manager's internal component databases, a narrow tool-specific feature set. |
| Simplicity | 3 | Deliberately SQL-like with simple rules (semicolon-terminated statements, comma-separated lists, quoted strings), though the unrelated ODMG OQL standard that shares this name is separately noted by Wikipedia as complex enough that "the complete OQL standard has not yet been fully implemented in any software". |
| Flexibility | 2 | Tightly scoped to creating, inserting into, and querying IBM Network Manager's own internal configuration databases, not a general-purpose data query mechanism. |
| Community and Ecosystem | 1 | A niche language embedded in one IBM network-management product; the broader ODMG OQL concept it is named after also has very limited practical adoption, per Wikipedia noting the full standard was never fully implemented by any software. |
| Extensibility | 1 | A fixed set of statement types documented for a specific embedded database tool, with no user extension mechanism described. |
| Transport Compatibility | 2 | Issued via a Perl API/scripting interface within IBM Network Manager (the "OQL Service Provider"), rather than being HTTP/URL-native. |
| Standardization | 2 | The name traces to the ODMG (Object Data Management Group) standard for object-oriented database query languages, but the dialect actually documented at list.csv's linked URL is IBM's own proprietary, tool-specific variant unrelated to that standards body's formal specification — a naming discrepancy worth flagging explicitly. |
| Security | 2 | No documented security-specific design; SQL-like statement execution against internal configuration databases carries typical injection-style risk if built from unsanitized input. |
| Performance | 2 | No independent performance data documented; used for a specific network-management embedded database rather than benchmarked for general-purpose or large-scale use. |
| Orthogonality | 3 | A basic SQL-like statement structure (SELECT/INSERT/UPDATE/DELETE-style) that is moderately consistent across the documented statement types. |

**Overall score (avg, informational only): 2.0**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 2.1**

## Summary

The OQL documented at list.csv's linked URL is IBM's own proprietary, SQL-like configuration-database language for its Network Manager product — a naming discrepancy worth noting, since the name "Object Query Language" more commonly refers to the ODMG's much more ambitious (but per Wikipedia, never fully implemented) object-database query standard; either way, this is a narrow, low-adoption, single-vendor tool-specific language with no meaningful extensibility or standardization.

## Sources

- IBM Corporation. (2026, March 30). [*Object Query Language*](https://www.ibm.com/docs/en/networkmanager/4.2.0?topic=reference-object-query-language).
- Wikipedia. (2025, December 27). [*Object Query Language*](https://en.wikipedia.org/wiki/Object_Query_Language).
