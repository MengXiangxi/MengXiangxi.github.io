---
name: uexplorer-bib
description: This skill generates properly formatted BibTeX citation entries for academic articles. It should be used when the user provides links to academic papers and needs BibTeX entries with specific formatting rules including citekeys, sentence-case titles, full author names, institution mapping, and keyword selection from predefined lists.
---

# uexplorer-bib

Generate BibTeX citation entries for academic articles from provided links or sources.

## Tools

- Use `@browsermcp` to retrieve full citation details from provided links. If the output is too long, truncate from the beginning.
- Use the pubmed tool only if necessary (e.g., to determine PMID). Do not use it to look up PubMed links directly—use browser tool instead

## Process

1. Fetch the article from the provided link
2. Extract: title, authors, journal, year, volume, number, pages, DOI, PMID, institutions, keywords
3. Generate citekey: `<first author last name><year><2-3 keywords from title>`
4. Format title in sentence case with `<sup>` and `<sub>` tags for superscripts/subscripts
5. Ensure full given names for authors (middle names may use initials without periods)
6. Use full journal names in title case (exception: "J. Nucl. Med." for Journal of Nuclear Medicine)
7. Map institutions to the standard list in `references/lists.md`. Include:
   - Institutions of main authors (first author, corresponding authors)
   - The institution that performs the PET scan (usually the hospital equipped with the uExplorer PET)
   - Typically 1-3 institutions, separated by semicolons
8. Select keywords from the predefined list in `references/lists.md`
9. Identify "Just Accepted" articles: Look for "Online ahead of print", "Just Accepted", or missing volume/number/page information
   - For "Just Accepted" papers: set `year={Just Accepted}` and **completely remove** `volume`, `number`, `pages` fields (do not leave empty)
   - Always include `doi`, `pmid`, `institution` fields
10. Append entry to the beginning of `uExplorer.bib`
11. Output a short summary of the paper describing its major ideas

## BibTeX Format

**Standard article:**

```bibtex
@article{citekey,
title={Sentence case title with <sup>18</sup>F tags},
author={Last, First and Last2, First2 M},
journal={Full Journal Name},
volume={X},
number={Y},
pages={123--456},
year={2024},
doi={10.xxxx/xxxxx},
pmid={12345678},
institution={Institution Name},
keywords={keyword1; keyword2; keyword3}
}
```

**Just Accepted article (volume/number/pages fields removed):**

```bibtex
@article{citekey,
title={Sentence case title with <sup>18</sup>F tags},
author={Last, First and Last2, First2 M},
journal={Full Journal Name},
year={Just Accepted},
doi={10.xxxx/xxxxx},
pmid={12345678},
institution={Institution Name},
keywords={keyword1; keyword2; keyword3}
}
```

No leading spaces. Minimal spacing. No tabs.

## Special Rules

- **Institution:** Include 1-3 institutions:
  - Institutions of main authors (first author, corresponding authors)
  - The institution that performs the PET scan (usually the hospital with uExplorer PET)
  - Omit universities if affiliated hospital exists. Keep succinct.
  - Use semicolons to separate multiple institutions (e.g., "SIAT, CAS; Qianfoshan Hospital")
- **Institution replacement:** "The First Affiliated Hospital of Shandong First Medical University" → "Qianfoshan Hospital"
- **Keywords:** Include tracer (except FDG), diseases, specialties. Avoid "total body" or "PET". Use semicolons between keywords. For new tracers, use EANM-recommended names and include tracer family (PSMA, DOTATATE, FAPI, etc.). Use "novel tracer" for uncommon tracers.

## Reference

See `references/lists.md` for institution and keyword lists.
