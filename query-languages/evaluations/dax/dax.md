# DAX

[↑ Full comparison table](../summary.md)

- Category: Analytics/Observability
- Official docs: [Data Analysis Expressions (DAX) Reference](https://learn.microsoft.com/en-us/dax/)
- Media type: None known — DAX queries are submitted inside a generic `application/json` body via the Power BI/Analysis Services REST APIs.
- Evaluated: 2026-09-04

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | A formula language with around 340 functions for calculated columns, measures, calculated tables, calculation groups, custom format strings, and row-level security filters, plus dedicated time-intelligence functions. |
| Simplicity | 3 | Designed to feel familiar to Excel formula authors and "be simple and easy to learn", but its row-context vs. filter-context evaluation model is a well-documented conceptual hurdle distinct from ordinary spreadsheet or SQL thinking. |
| Flexibility | 2 | DAX expressions are evaluated against a predefined Tabular/Power Pivot data model (tables and relationships) rather than arbitrary or schema-free data, so a data model must be designed and loaded first. |
| Community and Ecosystem | 4 | Powers Power BI, Excel Power Pivot, and SQL Server Analysis Services Tabular models — one of the most widely used BI toolchains — with a mature ecosystem of dedicated books, the DAX Patterns methodology, and community reference sites like dax.guide. |
| Extensibility | 2 | The function library is fixed and versioned entirely by Microsoft (with periodic additions of "new DAX functions"); there is no user-defined function mechanism for extending the core language. |
| Transport Compatibility | 2 | Evaluated inside BI client tools (Power BI, Excel, SSAS) or via XMLA-based query endpoints rather than being designed for direct URL/query-string embedding. |
| Standardization | 1 | A Microsoft-proprietary formula/query language with no independent standards body governing its syntax or semantics. |
| Security | 3 | Primarily used to define calculations evaluated inside a trusted BI model rather than as raw user-supplied query strings sent over a network, reducing typical injection exposure, though DAX queries issued via XMLA/REST endpoints still lack documented parameterization protections. |
| Performance | 4 | Runs against the in-memory VertiPaq columnar storage engine used by Analysis Services Tabular models, purpose-built for fast analytical aggregations over large BI datasets. |
| Orthogonality | 3 | Blends Excel-like formula syntax with relational filter/row-context semantics inherited in part from MDX, resulting in two coexisting evaluation models that can behave inconsistently for the same-looking expression depending on context. |

**Overall score (avg, informational only): 2.8**

## Summary

DAX is a mature, Excel-formula-inspired analytical expression language deeply embedded in Microsoft's Power BI/Analysis Services BI ecosystem, offering strong expressiveness for calculations over a fast in-memory columnar engine, but it requires a predefined Tabular data model, has no user-extensible function mechanism, and its dual row-context/filter-context evaluation model remains a genuine learning curve despite its Excel-like surface syntax.

## Sources

- Microsoft. (n.d.). [*Data Analysis Expressions (DAX) Reference*](https://learn.microsoft.com/en-us/dax/).
- Wikipedia. (2026, May 31). [*Data Analysis Expressions*](https://en.wikipedia.org/wiki/Data_Analysis_Expressions).
