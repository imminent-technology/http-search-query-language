# XPath

[↑ Full comparison table](../summary.md)

- Category: Path/document navigation
- Official docs: [XPath](https://developer.mozilla.org/en-US/docs/Web/XPath)
- Media type: None known — no IANA-registered media type exists; XPath expressions are normally embedded within another document (XSLT, XQuery, WebDAV SEARCH request bodies) rather than transmitted standalone.
- Evaluated: 2026-09-04

## Scores

| Criterion | Score | Rationale |
|---|---|---|
| Expressiveness | 4 | A rich set of axes (child, descendant, ancestor, following, preceding, attribute, etc.), node tests, predicates, and a substantial function library (string, boolean, number functions), with XPath 2.0+ adding a much richer type system and XPath 3.0 adding functions as first-class values. |
| Simplicity | 4 | The abbreviated syntax deliberately mimics familiar URI and Unix-style file-path syntax (e.g. /A/B/C), making basic expressions intuitive, though the full unabbreviated axis syntax and predicate rules add real depth for complex cases. |
| Flexibility | 3 | Fundamentally tied to navigating the tree structure of XML (and XML-like) documents via the XQuery and XPath Data Model; XPath 3.1 added maps and arrays to better support JSON, but it remains document-tree-centric rather than data-format-agnostic. |
| Community and Ecosystem | 5 | A foundational W3C technology implemented across nearly every major programming language (Java, Python, JavaScript, PHP, Perl, .NET, C/C++) and embedded natively in web browsers, XSLT, XML Schema, and XForms. |
| Extensibility | 3 | The core language is fixed per W3C specification version, but implementations widely support custom function extensions (e.g. the EXPath community group's extensions), and each major version (1.0 through 3.1) has added substantial new capability. |
| Transport Compatibility | 2 | Typically invoked via an API (e.g. document.evaluate() in browsers, javax.xml.xpath in Java) or embedded within other languages like XSLT, rather than being submitted directly as an HTTP query string. |
| Standardization | 5 | A formal W3C Recommendation since 1999, with stable versioned specifications (1.0, 2.0, 2.0 2nd edition, 3.0, 3.1) each formally ratified by the World Wide Web Consortium. |
| Security | 2 | No distinctive built-in anti-injection design; XPath injection is a well-documented attack class in security literature when expressions are built from unsanitized user input. |
| Performance | 3 | Performance varies significantly by implementation and document size; adequate for typical document-navigation use cases but XPath itself is not designed as a big-data analytics engine. |
| Orthogonality | 4 | Each location step uniformly combines an axis, a node test, and zero or more predicates, and the abbreviated and full-unabbreviated syntaxes are systematically interchangeable, giving a clean, composable model. |

**Overall score (avg, informational only): 3.5**

**Design quality score (avg of Expressiveness/Simplicity/Flexibility/Extensibility/Transport/Security/Performance/Orthogonality — excludes Community & Ecosystem and Standardization): 3.1**

## Summary

XPath is a mature, formally W3C-standardized expression language for navigating XML document trees, with a clean and highly composable axis/node-test/predicate model implemented across nearly every major programming ecosystem, but it remains tied to the XML tree data model, has no native HTTP transport of its own, and (like SQL) has no built-in defense against injection when expressions are built from unsanitized input.

## Sources

- MDN Web Docs (Mozilla). (n.d.). [*XPath*](https://developer.mozilla.org/en-US/docs/Web/XPath).
- Wikipedia. (2025, November 17). [*XPath*](https://en.wikipedia.org/wiki/XPath).
