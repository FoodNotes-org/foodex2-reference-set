# FoodEx2 reference set

This is a collaborative reference of food descriptions and FoodEx2 codes from published sources for benchmarking or testing.

This reference set is not endorsed by EFSA. It is here to help developers in the absence of an authorized gold dataset.

Use at your own discretion.

Contributions and feedback are welcome.

- [How to contribute](CONTRIBUTING.md)
- [Licence](LICENSE.md)


## What is in it

| Source | Country | Foods | Codes published by the source |
|---|---|---|---|
| [USDA FoodData Central: Foundation Foods](data/usda-fdc-foundation.csv) | US | 30 | none; all codes are drafts written here |
| [NEVO online 2025/9.0](data/nevo-online-2025.csv) (RIVM) | NL | 30 | all 30; for 15 this set proposes a different code |
| [CoFID 2021](data/cofid-2021.csv) (Public Health England) | GB | 30 | none; all codes are drafts written here |
| [FoodEx2 guidance, revision 2](data/efsa-foodex2-guidance-2015.csv) (EFSA, 2015) | — | 17 | all 17; for 6 this set proposes a different code |

The food descriptions belong to their sources. This set adds FoodEx2 codes,
and reviews of them, beside the descriptions. Codes target EFSA catalogue
release **MTX 17.1**.


## Using the data

Each tagged release is a frozen snapshot. Pin a tag so that your results stay
comparable:

```sh
git clone --branch v0.1.0 https://github.com/FoodNotes-org/foodex2-reference-set.git
```

The data files are plain CSV (UTF-8) with the same columns, so they can be
read together. In Python:

```python
import csv, glob

rows = []
for path in sorted(glob.glob("foodex2-reference-set/data/*.csv")):
    with open(path, encoding="utf-8", newline="") as f:
        rows += csv.DictReader(f)

coded = [r for r in rows if r["status"]]
print(len(coded), "foods with a code")

def expected_code(row):
    return row["proposed_code"] or row["published_code"]
```

Use `description` as the input to your coder, together with `country`, which
tells you how to read the name: "chorizo" from the US is a fresh sausage, not a
cured Spanish one. Compare the result with the expected code: the proposed
code when there is one, otherwise the code the source published.

A FoodEx2 code is a base term, then optional facets after `#`, separated by
`$`. Facets have no fixed order, so compare them as a set:

```python
def parse(code):
    base, _, facets = code.partition("#")
    return base, frozenset(facets.split("$")) if facets else frozenset()

def score(predicted, expected):
    p, e = parse(predicted), parse(expected)
    return {"base": p[0] == e[0], "full": p == e}
```

Some starting points:

- **Weight by status.** `confirmed` codes have two or more people behind them;
  `draft` codes have one. Report results for each status separately, or use
  only `confirmed` rows when you need the firmest answers.
- **Score the base term and the full code separately.** Most disagreement
  between careful coders is in the facets.
- **Read the notes when you disagree.** Hard cases say why they are coded the
  way they are. Where a row has both a `published_code` and a
  `proposed_code`, the note says why this set departs from the source.
- **Use `published_code` to measure against the source itself**, for NEVO and
  the EFSA guidance examples.
- **Look up codes** in the [FoodEx2 Atlas](https://foodex2-atlas.foodnotes.org/),
  which decodes a code into its terms. The catalogue itself is available from
  [EFSA](https://www.efsa.europa.eu/en/data/data-standardisation).
- **Cite the sources of the rows you use.** Each source has its own
  conditions; see [LICENSE.md](LICENSE.md).


## Files

| File | Meaning |
|---|---|
| `data/<source_id>.csv` | one row per food, one file per source edition |
| `sources.csv` | the full citation, edition and selection method of each source |
| `LICENSE.md` | who owns which columns, and each source's licence |
| `LICENSES/CC-BY-4.0.txt` | full text of CC BY 4.0, the licence of this project's additions |
| `CITATION.cff` | how to cite this set |
| `template.csv` | empty file with the column headers, for new contributions |

A data file holds selected foods from one edition of a source, never the full
source. `sources.csv` says how the foods were selected. More foods from the same
edition go into the same file; a new edition is a new source.


## Columns in `data/*.csv`

The first four columns are the source's, copied unchanged and never edited:

| Column | Meaning |
|---|---|
| `source` | the source that published the food, as it asks to be cited |
| `source_food_id` | the food's ID in that source (for FoodData Central: the FDC ID) |
| `description` | the food description exactly as the source gives it (surrounding spaces trimmed) |
| `published_code` | the FoodEx2 code exactly as the source published it; empty when the source published none |

The other columns are added by this project:

| Column | Meaning |
|---|---|
| `proposed_code` | a contributor's FoodEx2 code for the description; empty when the published code stands |
| `free_text` | details from the description the code cannot express, separated by `; `; a `label=` prefix naming the kind of detail is optional, e.g. `source=Granny Smith apple` |
| `country` | country of the source data, as an ISO 3166-1 two-letter code (`US`); empty for EFSA's EU-wide examples |
| `language` | language of the description, as an ISO 639-1 code (`en`) |
| `mtx_release` | the EFSA catalogue (MTX) release the code was checked against, e.g. `17.1` |
| `coded_by` | who wrote `proposed_code`: a name or organization; empty when there is no proposal |
| `status` | how far the row's code has been checked; see below |
| `reviewed_by` | who checked the row's code, other than its coder: names or organizations, separated by `;` |
| `notes` | reasoning for hard cases; required when a row has both a `published_code` and a `proposed_code` |

A row is identified by its file plus `source_food_id`.

When a contributor would code a food differently from its source,
`published_code` keeps the source's code, `proposed_code` holds the proposal,
and `notes` says why. The proposal sits beside the source's code; it never
replaces it.


## Review status

| Status | Meaning |
|---|---|
| *(empty)* | not coded yet |
| `draft` | a code has been proposed; nobody has checked it |
| `reviewed` | someone other than the coder checked it against the catalogue (the version specified by the dataset) and EFSA's guidance |
| `confirmed` | two or more people agree on it |

The row's code is `proposed_code` when it is filled, otherwise
`published_code`. Status applies to that code.

For benchmarking or testing, use the row's code. Prefer rows with status
`reviewed` or `confirmed`, treat `draft` as provisional, and skip rows with an
empty status (no code yet).


## Catalogue releases

A FoodEx2 code is valid against a particular release of EFSA's catalogue
(MTX). The data files target one release at a time, currently **MTX 17.1**;
each row's `mtx_release` says which release its code was checked against.

Every tagged release of this dataset is frozen and states the MTX release it
targets. Codes are never thrown away: when EFSA publishes a new catalogue
release, codes it invalidates are re-coded in the data files, while the
previous dataset release keeps the codes that were valid before. Use the
dataset release that matches the catalogue release of your data.


## Licence

The source's columns stay under the source's licence. Everything this project
adds is [CC BY 4.0](LICENSES/CC-BY-4.0.txt). [LICENSE.md](LICENSE.md) lists
each source, its owner, its licence and how to cite it.

FoodEx2 and its catalogue are © EFSA (European Food Safety Authority). This
project is independent and not endorsed by EFSA.
