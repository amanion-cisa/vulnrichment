# Flowcharts

Maybe offer rendered .svg or .png? If so, here's how:

```
npm install -g @mermaid-js/mermaid-cli
mmdc -i vulnrichment_new_cve.mermaid -o vulnrichment_new_cve.svg -b transparent -t neutral
mmdc -i vulnrichment_new_cve.mermaid -o vulnrichment_new_cve.svg
mmdc -i vulnrichment_new_cve.mermaid -o vulnrichment_new_cve.png
```

This is the flowchart for processing new CVE Records. 

```mermaid
---
title: "CISA Vulnrichment: New CVE Record (2024-12-29)"
---
flowchart TD
    new_CVE@{ shape: stadium, label: "New CVE"}
    add_SSVC@{ shape: rect, label: "Add SSVC" }
    fork@{ shape: fork }
    on_KEV@{ shape: diamond, label: "On KEV?" }
    add_KEV@{ shape: rectangle, label: "Add KEV \n SSVC E:A" }
    cna_CVSS@{ shape: diamond, label: "CNA \n provides \n CVSS?" }
    add_CVSS@{ shape: rectangle, label: "Add CVSS" }
    cna_CWE@{ shape: diamond, label: "CNA \n provides \n CWE?" }
    add_CWE@{ shape: rectangle, label: "Add CWE" }
    new_refs@{ shape: diamond, label: "Additional \n references?" }
    add_refs@{ shape: rectangle, label: "Add \n references"}
    join@{ shape: join }
    publish@{ shape: rectangle, label: "Publish" }
    adp@{ shape: rectangle, label: "CVE ADP" }
    github@{ shape: rectangle, label: "GitHub" }
    done@{ shape: stadium, label: "Done"}
    new_CVE --> add_SSVC
    add_SSVC --> fork
    fork --> on_KEV
    fork --> cna_CVSS
    fork --> cna_CWE
    fork --> new_refs
    on_KEV --> | Yes | add_KEV
    add_KEV --> join
    on_KEV --> | No | join
    cna_CVSS --> | Yes | join
    cna_CVSS --> | No | add_CVSS
    add_CVSS --> join
    cna_CWE --> | Yes | join
    cna_CWE --> | No | add_CWE
    add_CWE --> join
    new_refs --> | Yes | add_refs
    add_refs --> join
    new_refs --> | No | join
    join --> publish
    publish --> adp
    publish --> github
    adp --> done
    github --> done
```

This is the flowchart for processing updated CVE Records.

```mermaid
---
title: "CISA Vulnrichment: Updated CVE Record (2024-12-29)"
---
flowchart TD
    new_CVE@{ shape: stadium, label: "Updated CVE"}
```
