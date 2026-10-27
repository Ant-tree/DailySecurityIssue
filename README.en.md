# DailySecurityIssue

[한국어](README.md)

An archive of security research papers, collected every day and summarized in a fixed format. The focus is on mobile security, AI security, and obfuscation, with other noteworthy papers included as well.

## Layout

Every entry is written twice, once in Korean and once in English. Korean is the primary language; the English version covers the same papers in the same order.

```
ko/                Korean
  Mobile/
  AI/
  Obfuscation/
  Etc/
eng/               English (same layout as ko/)
```

- Files are named after the date of collection in Korea Standard Time, for example `eng/Mobile/2026-10-27.md`.
- If a category has no papers on a given day, no file is created for it.
- Figures are drawn as SVG and stored under `pics/` in each category directory.

## Categories

| Directory | Scope |
| --- | --- |
| `Mobile` | Mobile security in general. Each file is further divided into malware and analysis, moving target defense and deception, on-device LLMs, privacy, TEEs and side channels, and other topics. |
| `AI` | Security problems in AI models and AI-based systems |
| `Obfuscation` | Code obfuscation and deobfuscation |
| `Etc` | Notable papers that do not fit the categories above |

## Entry format

```markdown
# Paper title
> Venue (journal, conference, or preprint)
> Year
Abstract, summary, and link to the paper
### Contribution
What the paper contributes and where it is strong
### Evaluation
Metrics actually measured, datasets and baselines, and how far the numbers can be trusted
#### Comment
What sets the paper apart, its limitations, and how reputable the venue is
```

## Selection criteria

- The main sources are top security conferences and journals (IEEE S&P, USENIX Security, ACM CCS, NDSS, IEEE TDSC, IEEE TIFS, and others), mobile systems conferences, arXiv cs.CR, and the IACR ePrint archive.
- Papers from predatory journals or venues with unclear review processes are left out.
- Preprints that have not been peer reviewed may be included, but this is always stated in the venue line.
- Papers from Chinese institutions get an extra round of checks: whether the venue is actually indexed, whether the authors and affiliations are real, whether the work can be reproduced, and whether the evaluation holds up. The findings are noted in the Comment section, and papers that cannot be adequately verified are excluded.
- Papers already covered on an earlier date are not repeated.

## Update schedule

New papers are added every morning (Korea Standard Time). Each commit message includes the collection date.

## Disclaimer

Summaries and assessments are written after reading the papers themselves, but they may still contain errors of interpretation. Please check the original paper before citing it or relying on it.
