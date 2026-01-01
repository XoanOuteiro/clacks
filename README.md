# clacks

This tool is meant to allow VASS analysts and triagers to categorize vulnerabilities across many different metrics at once, while keeping ambiguity, uncertainty, and nuance explicit rather than hidden.

## Slugs (hierarchical tags)

The tool’s primary utility is producing "slugs": hierarchical tags (when a hierarchy exists) that describe a vulnerability across multiple metrics in a consistent, queryable form.

Example: searching `sqli` may emit slugs such as:

- Clacks slug:
  - `clacks/weakness/injection/sql-injection`
- CWE slug (hierarchical where available):
  - `cwe/view-699/CWE-74/CWE-89`
- VRT slug (always hierarchical):
  - `vrt/server-side-injection/sql-injection`
- OWASP Top 10 slug (bucket-level):
  - `owasp/top10/2021/A03`

If a metric has a hierarchy, the full hierarchy is emitted (not only the clacks hierarchy). If a metric has no meaningful hierarchy for the concept, only the leaf slug is emitted.

## Components

The project consists of three main parts:

### Authority
Upstream, read-only JSON exports of authoritative sources such as MITRE ATT&CK, OWASP Top 10, Bugcrowd VRT, and CWE.

These datasets are treated as reference material and are not modified beyond format normalization and indexing.

### Crosswalk
An opinionated, human-curated layer that correlates authority metrics and expresses a practical vulnerability taxonomy.

The crosswalk:
- Allows many-to-many mappings between taxonomies
- Supports multiple parents and competing interpretations
- Explicitly records confidence and notes for ambiguous mappings
- May include heuristic baseline ranges for CVSS 3.1 and CVSS 4.0 to aid triage (not as authoritative scoring)

This layer is expected to evolve continuously.

### clacks.rs
A CLI tool that consumes the local Authority and Crosswalk data to allow analysts to browse, search, and extract hierarchical tags and mappings without relying on a browser.

All queries are performed locally against the checked-out repository.

## Generated indexes

Some folders contain generated index files used by the CLI to provide fast and deterministic lookups (for example, alias resolution).

These files are derived artifacts and are not intended to be edited manually. Human contributions should focus on the Crosswalk concept files.

## Disclaimer

Initial crosswalk coverage for a given domain (for example, Web Security) is generated using an LLM and then continuously reviewed and corrected during real-world triage work.

Mappings are not absolute, may change over time, and can be wrong. Ambiguity is preserved intentionally rather than forced into a single “correct” classification.

Contributions and corrections are welcome.