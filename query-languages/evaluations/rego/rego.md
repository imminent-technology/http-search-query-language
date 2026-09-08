# Rego

[↑ Full comparison table](../summary.md)

- **Category**: Scripting
- **Official docs**: [Policy Language](https://www.openpolicyagent.org/docs/policy-language)
- **Media type**: application/json (Rego policies are evaluated by the Open Policy Agent (OPA) engine, which is queried over its REST Data/Query APIs using JSON request/response bodies; the Rego source itself is typically loaded as a `.rego` text file rather than transmitted per-request).
- **Evaluated**: 2026-09-15
- **Client Libraries**: Python: partial · JavaScript: partial · Java: partial · Go: mature · Rust: partial · .NET: partial
- **Support Model**: open-source-community

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | A declarative, Datalog-derived logic language with rules, incremental/complete definitions, array/object/set comprehensions, the `every`/`some`/`in` quantifier keywords for universal/existential quantification, user-defined functions, and a large built-in function library — expressive enough to encode arbitrary authorization and validation policy over nested JSON-like data. |
| Simplicity | 2 | Rego's declarative, unification-based semantics (variables are simultaneously inputs and outputs, expressions are joined implicitly, negation has documented safety rules) are a genuine departure from imperative programming, and OPA's own docs devote a full walkthrough plus a dedicated "why FOR ALL is written this way" explanation to help newcomers avoid common correctness pitfalls. |
| Flexibility | 4 | Operates over arbitrary nested JSON-like `input`/`data` documents with no fixed schema required (JSON Schema annotations are optional, type-checking aids rather than a mandatory schema), making it broadly reusable across very different policy domains (Kubernetes admission, API authorization, Terraform, Envoy). |
| Community and Ecosystem | 4 | OPA/Rego is a CNCF Graduated project with broad, cross-vendor adoption (Kubernetes admission control, Envoy, Istio, Terraform, Kafka, many API gateways), an active plugin/ecosystem (e.g., the Regal linter), and multi-organization governance rather than a single vendor. |
| Extensibility | 4 | Supports user-defined functions with incremental/overloaded definitions, custom built-in function registration from host language integrations (e.g., Go), and a documented, versioned metadata/annotation system for schemas, entrypoints, and custom fields. |
| Transport Compatibility | 2 | OPA (the Rego runtime) exposes REST Data and Query APIs over HTTP with JSON request/response bodies, and Rego itself has no URL-embeddable query-string form — policies are loaded as files/bundles and queried via structured JSON input rather than passed as an ad hoc parameter. |
| Standardization | 2 | Governed by OPA's CNCF project process with a documented formal grammar, but Rego remains a single-project specification without ratification by an independent standards body (ISO/IETF/W3C); its CNCF Graduated status gives it stronger multi-stakeholder oversight than a purely single-vendor DSL, placing it above jOOQ/Slick-style proprietary DSLs but still short of a true standards-track language. |
| Security | 4 | Explicitly designed for safely evaluating authorization/admission policy over untrusted request data: negation and variable-safety rules are enforced at compile time, and OPA documents a configurable "strict built-in errors" mode so that runtime errors in built-in calls can be treated as hard failures rather than silently evaluating to undefined, which matters for security-critical policy correctness. |
| Performance | 3 | OPA compiles/evaluates Rego with partial evaluation and (for compatible policies) WebAssembly compilation for embedding in high-throughput paths, and its own docs discuss function-call performance trade-offs, though as with EQL/AQL, real throughput depends on policy complexity and the surrounding OPA deployment rather than a documented formal complexity model like CEL's. |
| Orthogonality | 4 | References, comprehensions, rules (complete/partial/incremental), and the negation/quantifier keywords (`some`, `every`, `in`, `not`) are each independently documented and compose predictably — the same reference and iteration syntax works uniformly whether the underlying data is an array, object, or set. |

**Overall score (avg, informational only): 3.3**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.4**

## Summary

Rego is the CNCF-graduated, Datalog-derived declarative policy language at the heart of Open Policy Agent, purpose-built for expressing authorization and admission-control rules over arbitrary nested JSON with strong compile-time safety guarantees for negation and variable binding — but as a set/object-producing rule language it has no native sort or pagination concept, and its unification-based semantics carry a real learning curve for newcomers.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page.

```rego
package products

matches contains p if {
	some p in input.products
	p.category == "electronics"
	p.price > 100
}
```

Rego produces sets/objects, not ordered sequences — there is no ORDER BY-style sort operator or LIMIT/OFFSET-style pagination construct in the rule language itself. Rego can express the filter predicate shown above (returning the matching products as an unordered set), but sorting the results by price and paging through them is left entirely to the calling application after retrieving OPA's decision document.

## Sources

- Open Policy Agent (OPA) / CNCF. (n.d.). [*Policy Language*](https://www.openpolicyagent.org/docs/policy-language).
- Open Policy Agent (OPA) / CNCF. (n.d.). [*Policy Reference*](https://www.openpolicyagent.org/docs/policy-reference).
