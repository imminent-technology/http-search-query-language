# CEL (Common Expression Language)

[↑ Full comparison table](../summary.md)

- **Category**: Scripting
- **Official docs**: [CEL Language Definition](https://github.com/cel-expr/cel-spec/blob/master/doc/langdef.md)
- **Media type**: None known — CEL expressions are embedded as a plain string field within a host application's own configuration or API payload (e.g., a Kubernetes `ValidatingAdmissionPolicy` YAML rule, an Envoy proxy config, a Google Cloud IAM Condition, or a Firebase Security Rules file), not transmitted via any dedicated, independently registered media type.
- **Evaluated**: 2026-09-05

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | CEL offers arithmetic/comparison/logical operators, a ternary conditional, string functions (contains/startsWith/endsWith/matches), field selection, and a small set of comprehension macros (has/all/exists/exists_one/map/filter) that give it real power over lists, maps, and protobuf messages — but it is deliberately not Turing-complete (no loops, recursion, or user-defined functions), a conscious trade-off documented in its own guiding philosophy. |
| Simplicity | 4 | CEL's syntax deliberately mirrors expressions in C/C++/Java/JavaScript, and its own spec states the initial design was shaped by usability testing from the Firebase Rules experience — explicitly optimizing for developer approachability over language power. |
| Flexibility | 4 | CEL is designed to be embedded in arbitrary host applications with a pluggable evaluation context (typed variables, often protobuf messages) and is reused across very different domains — Kubernetes policy validation, Envoy proxy configuration, Google Cloud IAM Conditions, and Firebase Security Rules — though its data model remains bound to CEL's own type system (protobuf/JSON-like values) rather than being fully schema-agnostic. |
| Community and Ecosystem | 4 | CEL is used across major, independently-governed infrastructure projects (Kubernetes admission policies and CRD validation rules, Envoy, Google Cloud IAM, Firebase), with its GitHub specification repository reporting roughly 18,000 dependent projects and an active, multi-organization contributor base — broad, but still narrower and more infrastructure-embedded than a directly developer-facing language like GraphQL or SQL. |
| Extensibility | 5 | "Make it extensible" is one of CEL's three explicit guiding design philosophies: host applications can register custom extension functions and abstract types, and the spec itself evolves through a formal, publicly documented process (Feature Request → co-developed design doc → CEL Language Council review) described in its own GOVERNANCE.md. |
| Transport Compatibility | 2 | CEL defines no URL query-string or HTTP-native transport convention; expressions are always embedded as a string field inside a host system's own configuration format (Kubernetes YAML, Envoy config, IAM policy JSON, Firebase Rules files) rather than passed as a network-native query parameter. |
| Standardization | 3 | CEL has a formal, versioned specification, canonical wire-compatible protobuf AST definitions, and a conformance test suite, governed by a named "CEL Language Council" drawing from multiple contributing organizations rather than a single vendor — a more structured, multi-stakeholder governance model than a single-author spec, but still short of ANSI/ISO/IETF/W3C ratification, placing it in the same semi-formal, de-facto tier as HQL, MDX, Gremlin, and LINQ. |
| Security | 5 | Safety for evaluating untrusted, third-party-authored expressions is a first-class design goal, not an afterthought: the spec explicitly requires CEL to be memory-safe, side-effect-free, and terminating, and deliberately excludes Turing-completeness so that "orders of magnitude faster than equivalently sandboxed JavaScript" execution with reliable containment is possible — exactly the property that lets it be embedded directly in security-policy and admission-control systems. |
| Performance | 4 | The specification dedicates an entire formal section to abstract size, time, and space complexity for every operator, macro, and standard function (e.g., proving most constructs are linear and precisely bounding the only sources of exponential blow-up in macros) — an unusually rigorous, implementation-independent performance guarantee, though actual throughput still depends on each host's own evaluator implementation. |
| Orthogonality | 4 | Every operator is defined as sugar for a uniformly-dispatched named function (e.g., `e1 + e2` becomes `_+_(e1, e2)`), field selection behaves consistently across maps and protobuf messages, and the small set of comprehension macros compose predictably — a compact, internally consistent grammar by design. |

**Overall score (avg, informational only): 3.9**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 4.0**

## Summary

CEL (Common Expression Language) is a small, non-Turing-complete expression language originated at Google and now governed by a multi-organization "CEL Language Council," designed to be embedded in host applications for evaluating boolean conditions and expressions over typed (often protobuf) data. It underpins security- and policy-critical systems including Kubernetes admission-control validation rules, Envoy proxy configuration, Google Cloud IAM Conditions, and Firebase Security Rules. Its core design goals — memory safety, termination, and freedom from side effects — make it uniquely well-suited to safely evaluating untrusted, user-supplied expressions, driving standout scores on Security and a formally specified Performance model, alongside a deliberately extensible, orthogonal grammar. It has no HTTP/URL-native transport convention of its own (expressions are always embedded within a host system's configuration) and remains a semi-formally governed, non-standards-body specification.

## Example

**Scenario:** products in category `electronics` priced above 100, sorted by price descending, page 2 of 10 per page.

```cel
resource.category == "electronics" && resource.price > 100
```

CEL is a single-expression evaluation language with no query, sort, or pagination concept at all — it can only express the boolean filter predicate shown above. Sorting and paging a result set are entirely outside CEL's scope by design (it isn't Turing-complete and has no notion of an ordered result set to sort or page through).

## Sources

- CEL project (cel-expr; originated at Google). (n.d.). [*Common Expression Language (cel-spec README)*](https://github.com/cel-expr/cel-spec).
- CEL project (cel-expr). (n.d.). [*CEL Language Definition*](https://github.com/cel-expr/cel-spec/blob/master/doc/langdef.md).
- CEL project (cel-expr). (n.d.). [*CEL Project Governance*](https://github.com/cel-expr/cel-spec/blob/master/GOVERNANCE.md).
