---
name: uexplorer-update
description: This skill updates the uexplorer bibliography entry with "Just Accepted" status, when the paper is formally published.
---

# uexplorer-bib

Update the uexplorer bibliography entry with "Just Accepted" status, if the paper is formally published.

## Tools

- Use `@browsermcp` to retrieve full citation details from provided links. If the output is too long, truncate from the beginning.
- Use the pubmed tool only if necessary (e.g., to determine PMID).

## Process

1. Locate the entry in `bibliography/uexplorer.bib` using the provided citekey or other information.
2. Check the current status of the article using its DOI or PMID.
3. If DOI or PMID is missing, try to find it and update if successfully found. Otherwise, if they both present, just go to the next step.
4. If the article is now formally published (i.e., has volume, issue, and page numbers), update the entry:
   - Change the `year` field from "Just Accepted" to the actual publication year.
   - Add `volume`, `number`, and `pages` fields with the correct values.
   - Ensure all other fields are accurate and complete.
5. If the article is still "Just Accepted", ensure the entry reflects that status correctly.
6. Edit the corresponding entry in `bibliography/uexplorer.bib` to match the updated BibTeX format.
7. Return a summary of the changes made.

## BibTeX Format

**Just Accepted article (original):**

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

**Updated article:**

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

No leading spaces. Minimal spacing. No tabs.