# clacks
This tool is meant to allow VASS analysts and triagers to categorize vulnerabilities in many different metrics at once while keeping ambiguity and nuance explicit.

## Components
The project consists of 3 main parts:

- Authority: Upstream JSON exports of sources like MITTRE ATT&CK matrix, OWASP TOP 10, VRT and CWE.
- Crosswalk: An opinionated layer that matches all authority metrics and allows users to map the taxonomy of covered vulnerabilities, their general effects and average CVSS3.1 & CVSS4.0.
- Clacks.rs: A CLI tool to locally browse and query said JSONs on an intuitive manner, based on matching preset terms.

## Disclaimer
An initial crosswalk for a topic (eg: Web Security) is created by an LLM, and then throughly checked during my work as a triager. Expect constant changes to the JSONs as I detect flaws while working with this model. Matches and mapping are not absolute and can be wrong.

