# SHELF Standard Operating Procedures

Standard Operating Procedures (SOPs) for the Spawning Habitat & Early-Life
Linkages to Fisheries (SHELF) program, University of South Florida College
of Marine Science.

**Read the SOPs:** <https://shelf-usf.github.io/SHELF-SOP/>

| SOP | Title |
|-----|-------|
| 1 | Program Overview |
| 2 | Field Collection of Fish Eggs Using CUFES |
| 3 | DNA Barcoding of Fish Eggs |
| 4 | Data Management |

SOPs 2 and 3 are also published on protocols.io (see SOP 1, Section 1.7.1).

## Suggesting a change

Open a [new issue](https://github.com/SHELF-USF/SHELF-SOP/issues/new/choose)
and choose **Suggest a change to an SOP**. Full instructions are in SOP 1,
Section 1.8.4.

## For maintainers

- The SOP text is in `documents/SHELF_SOPn_*.md`; the preface is
  `index.qmd`; book settings are in `_quarto.yml`.
- Each push to `main` rebuilds the website and Word version
  (`.github/workflows/publish.yml`). To check locally first, run
  `quarto render` and open `_book/index.html`.
- Before a release, set the version in `_quarto.yml` (`date`,
  `date-format`, and `output-file`; format `YYYYMMDD.N`).
- Step-by-step editing and release instructions are in SOP 1,
  Section 1.8.6.

## Citation

Stallings C, Breitbart M, Kerr M, Marley A (2026) *SHELF Standard Operating
Procedures.* University of South Florida College of Marine Science.
<https://shelf-usf.github.io/SHELF-SOP/>

Funded by the Florida Institute of Oceanography, Florida RESTORE Act
Centers of Excellence Program (FLRACEP).

## License

The SOP text and SHELF figures are licensed under the
[Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/):
you may share and adapt them with credit to SHELF. Figures credited to
another source (for example, the xkcd cartoon in SOP 4, licensed
CC BY-NC 2.5) are not covered and remain under their owners' terms. Full license text: [LICENSE](LICENSE).
