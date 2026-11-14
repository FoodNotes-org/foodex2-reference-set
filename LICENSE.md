# Licence

Every row in `data/*.csv` has two parts: what the source published, and what
this project adds. Each part has its own licence.

| Columns | Owner | Licence |
|---|---|---|
| `source`, `source_food_id`, `description`, `published_code` | the source named in `source` | the source's licence, below |
| `proposed_code`, `free_text`, `country`, `language`, `mtx_release`, `coded_by`, `status`, `reviewed_by`, `notes` | the contributors to this set | [CC BY 4.0](LICENSES/CC-BY-4.0.txt) |

The source's columns are copied unchanged and are never edited here. A
`proposed_code` is a contributor's alternative to the published code, set
beside it.

Everything else in this repository (README, contributing guide, templates) is
CC BY 4.0 as well.


## Sources

Each data file holds a selection of foods from one edition of a source, never
the full source. `sources.csv` gives the full citation and how the foods were
selected.

### USDA FoodData Central: Foundation Foods

- **File:** `data/usda-fdc-foundation.csv`
- **Owner:** U.S. Department of Agriculture, Agricultural Research Service
- **Licence:** public domain, under [CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/)
- **Taken:** the FDC ID and the food description
- **Cite as:** U.S. Department of Agriculture, Agricultural Research Service.
  FoodData Central: Foundation Foods. fdc.nal.usda.gov

### NEVO online 2025/9.0

- **File:** `data/nevo-online-2025.csv`
- **Owner:** National Institute for Public Health and the Environment (RIVM),
  the Netherlands
- **Licence:** RIVM's [conditions of use](https://www.rivm.nl/sites/default/files/2025-11/Conditions-of-use-NEVO-online-2025-dataset.pdf).
  The data may be used unchanged, with the source and version stated.
  Additions must be clearly additional to the original data, the original
  data may not be amended, and end users may not be charged for the NEVO
  data. Read the conditions themselves; this summary is not a substitute.
- **Taken:** the NEVO-code, the Dutch food name and the FoodEx2 code RIVM
  published for it, from the table "NEVO 2025 with LanguaL and FoodEx2"
- **Cite as:** NEVO online, version 2025/9.0, RIVM, Bilthoven

### McCance and Widdowson's The Composition of Foods Integrated Dataset 2021 (CoFID)

- **File:** `data/cofid-2021.csv`
- **Owner:** Public Health England; Crown copyright
- **Licence:** [Open Government Licence v3.0](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/).
  Attribute with: "Contains public sector information licensed under the
  Open Government Licence v3.0."
- **Taken:** the food code and the food name, from the Factors worksheet
- **Cite as:** Public Health England. McCance and Widdowson's The Composition
  of Foods Integrated Dataset 2021.

### The food classification and description system FoodEx2 (revision 2)

- **File:** `data/efsa-foodex2-guidance-2015.csv`
- **Owner:** European Food Safety Authority (EFSA)
- **Licence:** reproduction is authorised provided the source is acknowledged
- **Taken:** the worked encoding examples in chapter 5: each food the
  guidance codes, and the code it assigns
- **Cite as:** European Food Safety Authority, 2015. The food classification
  and description system FoodEx2 (revision 2). EFSA supporting publication
  2015:EN-804. 90 pp.


## Using the set

Using rows from a source means meeting that source's conditions, at least by
citing it as above. Using the project's columns means crediting this set
under CC BY 4.0; `CITATION.cff` says how.

FoodEx2 and its catalogue are © EFSA. This project is independent and not
endorsed by EFSA, RIVM, Public Health England or the USDA.
