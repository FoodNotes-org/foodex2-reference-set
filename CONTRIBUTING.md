# Contributing

Useful contributions include:

- new foods from sources people use in reporting
- FoodEx2 codes for foods that are not coded yet
- a second look at codes that are still `draft` or `reviewed`
- corrections when a code is wrong

Every change comes in through a [pull request](https://github.com/FoodNotes-org/foodex2-reference-set/pulls) against `main`, so it is visible to everyone. Fork the repository, edit the CSV files, and open a PR.

Whoever opens the pull request does not need to be the person who coded or reviewed. In `coded_by` and `reviewed_by`, a name is enough, or an organization if you prefer not to be named.

Column meanings and review statuses are in [README.md](README.md). To check a
code, paste it into the [FoodEx2 Atlas](https://foodex2-atlas.foodnotes.org/),
which shows each of its terms.


## The source's columns

`source`, `source_food_id`, `description` and `published_code` are copied
from the source and are never edited. If one of them was copied wrongly, fix
the copy so it matches the source again, and say so in the pull request.


## Add a food

1. Open the matching `data/<source_id>.csv`, or start from `template.csv` for a new source.
2. Add one row. Fill `source` as the other rows in the file do, and `source_food_id` with the food's ID in the source.
3. Copy `description` exactly as the source gives it (trim surrounding spaces only).
4. If the source published a FoodEx2 code, copy it unchanged into `published_code`.
5. Set `country` and `language`.
6. Leave `proposed_code` empty if you are only nominating the food, or propose a code as below.

More foods from the **same edition** of a source go in the same file. A **new edition** is a new source: a new data file and a row in `sources.csv`.


## Propose a code

1. Set `proposed_code`, checked against the current MTX release (see README; today `17.1`). If you agree with the published code, leave `proposed_code` empty and review that code instead.
2. Set `mtx_release` to that release.
3. Set `coded_by` to your name or organization.
4. Set `status` to `draft`.
5. Put details the code cannot express in `free_text` (`; `-separated; a `label=` prefix is optional).

To disagree with a published code, leave `published_code` as it is, put your
code in `proposed_code`, set `status` to `draft`, and explain why in `notes`.


## Review a code

1. Check the row's code against the catalogue and EFSA's guidance: `proposed_code` when it is filled, otherwise `published_code`. You cannot review a code you wrote yourself.
2. Update `status`:
   - `reviewed` — someone other than the coder checked it; a code you only propose stays `draft`
   - `confirmed` — two or more people agree
3. Append your name (or organization) to `reviewed_by`, separated by `;` if someone is already listed.


## Add a new source

1. Check that the source's licence allows its food descriptions to be reused here. If unsure, open an issue first.
2. Add a row to `sources.csv`: citation, edition, and how the foods were selected.
3. Add `data/<source_id>.csv` with the selected foods, never the full source.
4. Add the source to [LICENSE.md](LICENSE.md): owner, licence, what was taken, and how to cite it.


## Licence of contributions

By opening a pull request you license what you add under
[CC BY 4.0](LICENSES/CC-BY-4.0.txt): the codes you write, your reviews,
notes, free text and the other columns this project adds. They may be
republished, for example on Zenodo or Hugging Face.

The source's columns are not yours to license. They stay under the source's
licence, as [LICENSE.md](LICENSE.md) records.
