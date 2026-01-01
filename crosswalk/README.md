# crosswalk

Curated crosswalk layer for clacks.

- One concept = one JSON file.
- Hierarchy is encoded via `parents` (DAG; multiple parents allowed).
- Tools should compute children by building a reverse index at runtime.

Scope: broad and deep coverage for web and API vulnerability concepts.

## Slugs (hierarchical tags)

The primary utility is producing "slugs": hierarchical tags (when a hierarchy exists) that describe a vulnerability across multiple metrics.

Example slugs for a SQL injection finding:

- clacks:
  - `clacks/weakness/injection/sql-injection`
  - `clacks/weakness/web/sql-injection`
- cwe (via CWE views, when available):
  - `cwe/view-699/CWE-74/CWE-89`
- owasp top 10 (bucket-level):
  - `owasp/top10/2021/A03`
- owasp api top 10:
  - `owasp/api10/2023/API1`

If a metric has a hierarchy, tools should emit the full hierarchy, not only the clacks hierarchy.

## Potential subtypes (children)

Many vulnerabilities have useful subtypes (e.g. SQL injection → blind → time-based).
The dataset stores only `parents`. Tools should compute children at runtime and can show likely subtypes with `--children` / `--tree`.

## Generated indexes

`crosswalk/generated/` contains generated lookup indexes (alias lookup shards, etc.).
They are derived artifacts and not intended to be edited manually.
