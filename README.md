# HTTP Search Query Language

Research on which query language to use when performing search/query operations over HTTP — specifically in the context of the new **HTTP `QUERY` method**.

Use this research to figure out, for your own API, whether one of the 42 query languages analyzed here already fits the query content of a `QUERY` request — or whether none of them do, and you're better off designing a brand new, purpose-built query language instead.

## What is this?

For years, APIs that need to run a search or a query too complex to fit in a URL have had to misuse HTTP `POST` — a method that is neither safe nor idempotent — just to carry a query in the request body. The HTTP `QUERY` method closes that gap: it's an HTTP method that, like `GET`, is safe, idempotent, and cacheable, but like `POST`, can carry an arbitrary request body (the "query content"). After more than a decade of on-and-off work in the IETF, `QUERY` is now a published Internet Standard: [**RFC 10008**](https://www.rfc-editor.org/info/rfc10008/), *The HTTP QUERY Method*, published in June 2026.

That request body has to be expressed in *some* language. `QUERY` is deliberately media-type agnostic — the body can be SQL, GraphQL, JSONPath, XSLT, a URL-encoded form, or anything else, as long as the server understands it (advertised via the `Accept-Query` response header defined by the same spec). That raises an obvious follow-up question: **out of the many query languages already in use across databases, search engines, and APIs, which ones are actually good fits for the query content of an HTTP `QUERY` request?**

This repository is an attempt to answer that question systematically, by researching and scoring a broad set of existing query languages against a common rubric, so the results can be used as raw material for a future comparison article — not to declare a single "winner," but to give API designers real, sourced data points when they choose (or design) a query language for their own `QUERY`-based API.

## The HTTP QUERY method

`QUERY` is defined in [**RFC 10008**](https://www.rfc-editor.org/info/rfc10008/), *The HTTP QUERY Method*, an IETF Proposed Standard authored by **Julian Reschke** (greenbytes), **James M. Snell** (Cloudflare), and **Mike Bishop** (Akamai), with early contributions from Ashok Malhotra. It was published in **June 2026** through the IETF's [HTTP working group](https://httpwg.org/), after several years of development as an Internet-Draft.

In short, the spec defines:

- **`QUERY`**: a request method that asks a server to run a query (described by the request content) scoped to the target URI, without altering server state. It's safe and idempotent like `GET`, but — unlike `GET` — the query itself lives in the request body instead of the URL, avoiding URL-length limits and awkward encoding of complex query parameters.
- **`Accept-Query`**: a response header a server can use to advertise which query-content media types (e.g. `application/sql`, `application/jsonpath`, `application/x-www-form-urlencoded`) it supports for a given resource.
- Well-defined semantics for caching (the cache key must incorporate the request content), conditional requests, range requests, and redirection, so that intermediaries and clients can treat `QUERY` as a first-class, cacheable operation instead of an opaque `POST`.

IANA has registered both `QUERY` (in the HTTP Method Registry) and `Accept-Query` (in the HTTP Field Name Registry) as part of the RFC's publication.

For accessible background on why this method exists and what problem it solves, see Bruno Pedro's write-up, [*The HTTP QUERY Method*](https://apichangelog.substack.com/p/the-http-query-method), on The API Changelog — written while the method was still a draft, but still a good introduction to the motivation behind it (it explicitly calls out the open question of *which* query language(s) an API should accept in the `QUERY` body). That article is what originally motivated this research project.

### How HTTP QUERY evolved into an RFC

The idea behind `QUERY` predates its final name by roughly a decade:

1. **2015 — the `SEARCH` precursor.** Julian Reschke, Ashok Malhotra, and James M. Snell authored an early Internet-Draft, [`draft-snell-search-method`](https://datatracker.ietf.org/doc/draft-snell-search-method/00/), proposing a safe, idempotent `SEARCH` method that could carry a request body — the same basic problem `QUERY` would later solve.
   - WebDAV already had three safe/idempotent methods that carry a request body — `PROPFIND`, `REPORT`, and `SEARCH` (the latter from [RFC 5323](https://www.rfc-editor.org/info/rfc5323)) — and reusing one of them was considered, but ultimately rejected: they're tied to a generic, WebDAV-flavored XML media type rather than being media-type agnostic.
2. **2019 — discussion reopens.** The topic was revived by Asbjørn Ulsberg during that year's HTTP Workshop, prompting the HTTP working group to take a fresh, more general look at the problem.
3. **The method gets renamed to `QUERY`.** During the specification's development the method name changed from `SEARCH` to `QUERY`, better reflecting its relationship to a URI's query component and decoupling it from WebDAV associations.
4. **Standards-track development.** The proposal became the IETF Internet-Draft `draft-ietf-httpbis-safe-method-w-body`, iterated on for several years within the [HTTP working group](https://httpwg.org/), accumulating implementation experience and working-group consensus.
5. **June 2026 — publication as RFC 10008.** The draft completed IETF review, was approved for publication by the IESG, and was published by the RFC Editor as [RFC 10008](https://www.rfc-editor.org/info/rfc10008/), *The HTTP QUERY Method* — a Proposed Standard and, with it, an official IANA registration for both the `QUERY` method and the `Accept-Query` header field.

### Further reading

- Reschke, J., Snell, J. M., & Bishop, M. (2026). *The HTTP QUERY method* (RFC 10008). IETF. https://www.rfc-editor.org/info/rfc10008/
- Fielding, R., Nottingham, M., & Reschke, J. (Eds.). (2022). *HTTP semantics* (RFC 9110). IETF. https://www.rfc-editor.org/rfc/rfc9110
- Fielding, R., Nottingham, M., & Reschke, J. (Eds.). (2022). *HTTP caching* (RFC 9111). IETF. https://www.rfc-editor.org/rfc/rfc9111
- Nottingham, M., & Kamp, P. (2024). *Structured field values for HTTP* (RFC 9651). IETF. https://www.rfc-editor.org/info/rfc9651
- IETF HTTP Working Group. (n.d.). *Query-method* [Issue tracker]. GitHub. https://github.com/httpwg/http-extensions/labels/query-method
- Reschke, J., Malhotra, A., & Snell, J. M. (2015). *HTTP SEARCH method* (Internet-Draft draft-snell-search-method-00). IETF. https://datatracker.ietf.org/doc/draft-snell-search-method/00/

## What's in this repository

- [`query-languages/list.md`](query-languages/list.md) (and the machine-readable [`list.csv`](query-languages/list.csv)) — the catalog of query languages under research, each linked to its official documentation.
- [`query-languages/evaluation.md`](query-languages/evaluation.md) — the ten criteria used to evaluate every language (Expressiveness, Simplicity, Flexibility, Community and Ecosystem, Extensibility, Transport Compatibility, Standardization, Security, Performance, Orthogonality), including a detailed breakdown of what "Orthogonality" means for a query language.
- [`query-languages/evaluations/`](query-languages/evaluations/) — one JSON + Markdown file per language with a scored, sourced evaluation against those criteria, plus [`rubric.md`](query-languages/evaluations/rubric.md) (the scoring rubric) and aggregate [`summary.json`](query-languages/evaluations/summary.json) / [`summary.md`](query-languages/evaluations/summary.md) comparison tables grouped by category.

Scores are descriptive snapshots meant as raw research material for a future comparison article, not a ranking of "best" query language — the right choice for a given `QUERY`-based API still depends heavily on its own data model, transport constraints, and audience.

## Contributing a new query language

Want to add a query language that isn't in the catalog yet? This repository ships a [GitHub Copilot skill](.github/skills/add-query-language/SKILL.md), `add-query-language`, that automates the whole process: cataloging the language in `list.csv`/`list.md`, researching and scoring it against the [rubric](query-languages/evaluations/rubric.md), creating its evaluation folder, and updating the aggregate `summary.json`/`summary.md` (including the Media types table and the Observations section).

To use it in VS Code with GitHub Copilot:

1. Open this repository in VS Code with the Copilot Chat extension enabled (the skill lives in `.github/skills/` and is picked up automatically).
2. Open the chat view and either type `/add-query-language` followed by the language name, or just ask in plain language, e.g. *"Add JMESPath to the query languages portfolio."*
3. Copilot will ask any follow-up questions it needs (e.g. the official documentation URL, a short description) before cataloging, researching, scoring, and evaluating the new language, and updating every affected file.
4. Review the changes (new/updated rows in `list.csv`/`list.md`, the new `query-languages/evaluations/<slug>/` folder, and the updated `summary.json`/`summary.md`) before opening a pull request.

## License

This work is licensed under the [Creative Commons Attribution 4.0 International License](LICENSE.md).
