# Invictus IR — IOCs & TTPs

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-blue.svg)](LICENSE)
[![MITRE ATT&CK](https://img.shields.io/badge/MITRE-ATT%26CK-red.svg)](https://attack.mitre.org/)
![Last commit](https://img.shields.io/github/last-commit/invictus-ir/IOCs)
![Stars](https://img.shields.io/github/stars/invictus-ir/IOCs?style=social)

**Curated Indicators of Compromise (IOCs) and MITRE ATT&CK-mapped Tactics, Techniques & Procedures (TTPs) from real cloud incident-response casework by [Invictus IR](https://www.invictus-ir.com).** Every file here is the machine-readable evidence behind one of our [threat-intelligence blog posts](https://www.invictus-ir.com/news) — reconstructed from audit logs during actual investigations across AWS, Microsoft 365, Azure, and Google Workspace.

> **TL;DR** — 13 CSV datasets. 5 incident IOC sets + 8 ATT&CK-mapped TTP sets, including a **Cloud Threat Landscape** of **168 techniques** observed in the wild. Free to use with attribution (CC BY 4.0). Load straight into ATT&CK Navigator, a SIEM, or pandas.

---

## At a glance

| | |
|---|---|
| **What** | Threat intelligence: IOCs (hashes, domains, IPs) + TTPs (MITRE ATT&CK techniques with procedure context) |
| **Format** | Plain-text CSV — one file per campaign or threat actor |
| **Coverage** | Cloud & identity intrusions: BEC, supply-chain compromise, phishing, cloud espionage, ransomware |
| **Mapped to** | [MITRE ATT&CK](https://attack.mitre.org/) (Enterprise + Cloud matrices), tactic → technique → ID → procedure |
| **Source** | Real incident reconstructions, not surveys — see the linked [Invictus IR research](https://www.invictus-ir.com/news) |
| **License** | [CC BY 4.0](LICENSE) — reuse freely, just credit Invictus IR |
| **Updated** | Continuously, alongside new research |

---

## What's inside

### 🧭 Cloud Threat Landscape (flagship dataset)

`TTPs - Cloud Threat Landscape - Q1-Q3 2025.csv` — **168 attacker technique observations** spanning **76 distinct MITRE ATT&CK techniques** and **all 14 tactics** of the cloud kill chain, each attributed to a threat actor and the cloud service abused. The headline finding: adversaries aren't breaking in, they're **logging in** — *Valid Accounts: Cloud Accounts* is the single most-observed technique.

### 🎯 Threat-actor TTP profiles

ATT&CK-mapped technique sets for named adversaries, each with real procedure context:

| Threat actor | File | Nexus |
|---|---|---|
| **Silk Typhoon** | `TTPs - Profiling Silk Typhoon - Nov 2025.csv` | China · cloud/Commvault |
| **Sea Turtle** | `TTPs - Profiling Sea Turtle - August 2025.csv` | DNS hijacking |
| **Laundry Bear** | `TTPs - Profiling Laundry Bear - June 2025.csv` | Russia |
| **TradeTraitor** | `TTPs - Profiling TradeTraitor - June 2025.csv` | North Korea · crypto |
| **JavaGhost** | `TTPs - Profiling JavaGhost - May2025.csv` | Cloud abuse / phishing |
| **Black Basta** | `TTPs - BlackBasta Chat Leaks.csv` | Ransomware (leaked chats) |

Plus a campaign-level TTP set: `TTPs - Locked Out, Dropboxed In - When BEC threats innovate.csv` — the technique side of the matching IOC file below.

### 🧾 Incident IOC sets

Indicators from specific investigations and campaigns:

- `IOCs - Axios Supply Chain Attack - 31.03.2026.csv` — malware supply-chain compromise
- `IOCs - Anatomy of a BEC in 2025.csv` — business email compromise
- `IOCs - Invisible Architecture of Modern Phishing.csv` — phishing infrastructure
- `IOCs - Locked Out, Dropboxed In - When BEC threats innovate.csv` — BEC innovation
- `IOCs - VendorVandals - How we almost got hacked - Nov 2025.csv` — a first-person near-miss

---

## Data schema

**IOC files**

| Column | Description |
|---|---|
| `Type` | Indicator type (Malware/hash, IP, Domain, URL, …) |
| `Indicator` | The IOC value |
| `Description` | Context / role |
| `Incident` | The campaign it belongs to |

**TTP files**

| Column | Description |
|---|---|
| `MITRE Tactic` | ATT&CK tactic (e.g. Initial Access) |
| `MITRE Technique` | ATT&CK technique name |
| `Technique ID` | ATT&CK ID (e.g. `T1078.004`) |
| `Threat Actor` / `Procedure (Context)` | Attribution and how the technique was used |
| `Services Abused` | Cloud service or tool involved (where present) |

---

## How to use it

**Load into MITRE ATT&CK Navigator** — build a coverage layer from any TTP file's `Technique ID` column to visualize an actor's or campaign's technique spread, or overlay several to compare.

**Analyze in Python**

```python
import pandas as pd
ttps = pd.read_csv("TTPs - Cloud Threat Landscape - Q1-Q3 2025.csv")
print(ttps["MITRE Tactic"].value_counts())          # where activity concentrates
print(ttps["MITRE Technique"].value_counts().head(10))  # the most-used techniques
```

**Feed a SIEM / detection pipeline** — use the IOC files as block-lists and the TTP files to prioritize detection engineering by real-world frequency. Pair with our open-source acquisition and detection tooling:

- [Microsoft-Extractor-Suite](https://github.com/invictus-ir/Microsoft-Extractor-Suite) — acquire M365 & Azure logs
- [Invictus-AWS](https://github.com/invictus-ir/Invictus-AWS) — acquire & analyze AWS CloudTrail
- [Sigma-AWS](https://github.com/invictus-ir/Sigma-AWS) — detection rules for AWS

---

## Threat actors & campaigns covered

Silk Typhoon · Sea Turtle · Laundry Bear · TradeTraitor · JavaGhost · Black Basta · JINX-0126 · Mimo · UNC6040 · MUT-1692 · UTA0304 · UTA0307 — plus business email compromise (BEC), software supply-chain compromise, modern phishing infrastructure, and cloud resource hijacking. Each dataset links back to the full analysis on the [Invictus IR blog](https://www.invictus-ir.com/news).

---

## FAQ

**What is this repository?**
A free, continuously updated collection of indicators of compromise (IOCs) and MITRE ATT&CK-mapped TTPs published by Invictus IR, derived from real cloud incident-response engagements.

**How are the TTPs different from other ATT&CK datasets?**
Each technique carries a **procedure-level narrative** — what the adversary actually did and which cloud service they abused — not just a colored matrix cell.

**Can I use this commercially?**
Yes. It's licensed [CC BY 4.0](LICENSE) — reuse in any context (including commercial) as long as you credit Invictus IR.

**How current is it?**
It's updated alongside our published research; the Cloud Threat Landscape covers Q1–Q3 2025.

**Where does the data come from?**
Cloud and identity intrusions we reconstructed from surviving audit logs (AWS CloudTrail, Microsoft 365 Unified Audit Log, Azure, Google Workspace).

---

## How to cite

If you use this data in research, detection content, or reporting, please cite it (a `CITATION.cff` is included, so GitHub shows a **"Cite this repository"** button):

> Invictus IR. *IOCs & TTPs — Threat Intelligence Datasets.* GitHub, https://github.com/invictus-ir/IOCs

---

## Contributing & disclaimer

Feedback and additional context are welcome via issues. These indicators are shared for **defensive research and detection**. Do not use them to attack the environments, hosts, or infrastructure referenced. ATT&CK® is a registered trademark of The MITRE Corporation; technique names and IDs are used under MITRE's terms.

**License:** [CC BY 4.0](LICENSE) · **Research:** https://www.invictus-ir.com/news · **Company:** https://www.invictus-ir.com
