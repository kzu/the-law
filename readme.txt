This repository is an Open Knowledge Format (OKF) knowledge bundle for Frédéric Bastiat's 1850 essay "The Law".

See:
- OKF specification: https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/SPEC.md
- The book: https://mises.org/library/book/law (Mises Institute)

The bundle implements the OKF v0.1 standard: a git-friendly directory tree of UTF-8 markdown files, each with a YAML frontmatter block containing at minimum a "type" field, plus optional title/description/tags/timestamp plus arbitrary metadata. Concepts are cross-linked using standard markdown links (bundle-absolute /path or relative). Reserved index.md files provide progressive disclosure navigation; log.md records history.

Generated artifacts (produced with the `dnx okf` toolchain from https://github.com/devlooped/okf):

- okf.json (also referenced in some contexts as @okf.json): produced by `dnx okf graph`. A complete, self-contained machine-readable graph of the knowledge bundle. Every concept becomes a node; markdown links become directed edges. Nodes include extracted frontmatter plus computed graph analytics.
- index.html: produced by `dnx okf viz` (or `dnx okf viz -o index.html`). An interactive browser-based visualization of the graph (node-link diagram with filtering, search, details pane, and importance-driven layout/sizing).

What is showcased:

The content is a richly cross-referenced knowledge representation of Bastiat's argument: the true nature of law as the organization of collective defense of natural rights (life, liberty, property), how law is perverted into "legal plunder" via false philanthropy and greed, the consequences (demoralization, class conflict, rent-seeking, etc.), critiques of socialism, and the proper negative/limited sphere of law.

The directory structure mirrors the conceptual organization (fundamental-principles/, legal-plunder/ with its manifestations and consequences subtrees, perversion-of-law/, true-law/, modern-relevance/, key-extracts/, etc.). The root the-law.md and index.md serve as entry points. A log.md chronicles the bundle's construction.

Particular value added by the OKF tooling (https://github.com/devlooped/okf, beyond the plain OKF markdown format itself):

- Graph model: Automatically parses all intra-bundle markdown links to produce a directed graph (no manual edge lists required).
- Degree metrics: Each node reports in-degree, out-degree, and total degree — revealing hubs vs. leaves.
- PageRank: A damped PageRank implementation computes a "weight" (0..1) and stable "rank" (competition ranking) for every node, quantifying structural importance/centrality within the corpus. Top-ranked concepts in this bundle include:
  - legal-plunder/definition (rank 1, degree 86)
  - the-law (rank 2, degree 85)
  - true-law/proper-sphere (rank 3, degree 49)
  - fundamental-principles/law-as-organization-of-defense (rank 4, degree 58)
  - fundamental-principles/natural-rights (rank 5, degree 70)
- Spec validation: `dnx okf check` rigorously validates conformance (required frontmatter type on every concept, correct structure of index.md and log.md, etc.) and reports warnings for broken or dangling links. This bundle passes validation with rich connectivity (zero isolated nodes after enhancement).
- Visualization: `dnx okf viz` consumes either a live bundle or a previously generated okf.json and emits a self-contained interactive HTML that uses the precomputed degree/rank/weight values to drive node sizing, coloring by type, and other analytics affordances.

Together these turn a human-authored collection of markdown essays into a validated, queryable, visualizable, and agent-friendly knowledge graph while preserving full readability, editability, and version-control friendliness of the source files.

The bundle was authored/enhanced to demonstrate these capabilities: extensive deliberate cross-referencing makes the core ideas function as high-centrality hubs.