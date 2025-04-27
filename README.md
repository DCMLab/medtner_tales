![Version](https://img.shields.io/github/v/release/DCMLab/medtner_tales?display_name=tag)
[![DOI](https://zenodo.org/badge/383821270.svg)](https://doi.org/10.5281/zenodo.7473528)
![GitHub repo size](https://img.shields.io/github/repo-size/DCMLab/medtner_tales)
![License](https://img.shields.io/badge/license-CC%20BY--NC--SA%204.0-9cf)


This is a README file for a data repository originating from the [DCML corpus initiative](https://github.com/DCMLab/dcml_corpora)
and serves as welcome page for both 

* the GitHub repo [https://github.com/DCMLab/medtner_tales](https://github.com/DCMLab/medtner_tales) and the corresponding
* documentation page [https://dcmlab.github.io/medtner_tales](https://dcmlab.github.io/medtner_tales)

For information on how to obtain and use the dataset, please refer to [this documentation page](https://dcmlab.github.io/medtner_tales/introduction).

When you use (parts of) this dataset in your work, please read and cite the accompanying data report:

_Hentschel, J., Rammos, Y., Neuwirth, M., Moss, F. C., & Rohrmeier, M. (2024). An annotated corpus of tonal piano music 
from the long 19th century. Empirical Musicology Review, 18(1), 84–95. https://doi.org/10.18061/emr.v18i1.8903_

This corpus forms part of the larger [Distant Listening Corpus](https://github.com/DCMLab/distant_listening_corpus)
which constitutes a data infrastructure the data report of which has implications for the present corpus, too:

_Hentschel, J., Rammos, Y., Neuwirth, M., & Rohrmeier, M. (2025). A corpus and a modular infrastructure for the 
empirical study of (an)notated music. Scientific Data, 12(1), 685. https://doi.org/10.1038/s41597-025-04976-z_

# Nikolai Medtner – Tales (A corpus of annotated scores)


## Getting the data

* download repository as a [ZIP file](https://github.com/DCMLab/medtner_tales/archive/main.zip)
* download a [Frictionless Datapackage](https://specs.frictionlessdata.io/data-package/) that includes concatenations
  of the TSV files in the four folders (`measures`, `notes`, `chords`, and `harmonies`) and a JSON descriptor:
  * [medtner_tales.zip](https://github.com/DCMLab/medtner_tales/releases/latest/download/medtner_tales.zip)
  * [medtner_tales.datapackage.json](https://github.com/DCMLab/medtner_tales/releases/latest/download/medtner_tales.datapackage.json)
* clone the repo: `git clone https://github.com/DCMLab/medtner_tales.git` 


## Data Formats

Each piece in this corpus is represented by five files with identical name prefixes, each in its own folder. 
For example, the first tale has the following files:

* `MS3/op08n01.mscx`: Uncompressed MuseScore 3.6.2 file including the music and annotation labels.
* `notes/op08n01.notes.tsv`: A table of all note heads contained in the score and their relevant features (not each of them represents an onset, some are tied together)
* `measures/op08n01.measures.tsv`: A table with relevant information about the measures in the score.
* `chords/op08n01.chords.tsv`: A table containing layer-wise unique onset positions with the musical markup (such as dynamics, articulation, lyrics, figured bass, etc.).
* `harmonies/op08n01.harmonies.tsv`: A table of the included harmony labels (including cadences and phrases) with their positions in the score.

Each TSV file comes with its own JSON descriptor that describes the meanings and datatypes of the columns ("fields") it contains,
follows the [Frictionless specification](https://specs.frictionlessdata.io/tabular-data-resource/),
and can be used to validate and correctly load the described file. 

### Opening Scores

After navigating to your local copy, you can open the scores in the folder `MS3` with the free and open source score
editor [MuseScore](https://musescore.org). Please note that the scores have been edited, annotated and tested with
[MuseScore 3.6.2](https://github.com/musescore/MuseScore/releases/tag/v3.6.2). 
MuseScore 4 has since been released which renders them correctly but cannot store them back in the same format.

### Opening TSV files in a spreadsheet

Tab-separated value (TSV) files are like Comma-separated value (CSV) files and can be opened with most modern text
editors. However, for correctly displaying the columns, you might want to use a spreadsheet or an addon for your
favourite text editor. When you use a spreadsheet such as Excel, it might annoy you by interpreting fractions as
dates. This can be circumvented by using `Data --> From Text/CSV` or the free alternative
[LibreOffice Calc](https://www.libreoffice.org/download/download/). Other than that, TSV data can be loaded with
every modern programming language.

### Loading TSV files in Python

Since the TSV files contain null values, lists, fractions, and numbers that are to be treated as strings, you may want
to use this code to load any TSV files related to this repository (provided you're doing it in Python). After a quick
`pip install -U ms3` (requires Python 3.10 or later) you'll be able to load any TSV like this:

```python
import ms3

labels = ms3.load_tsv("harmonies/op08n01.harmonies.tsv")
notes = ms3.load_tsv("notes/op08n01.notes.tsv")
```


## Version history

See the [GitHub releases](https://github.com/DCMLab/medtner_tales/releases).

## Questions, Suggestions, Corrections, Bug Reports

Please [create an issue](https://github.com/DCMLab/medtner_tales/issues) and/or feel free to fork and submit pull requests.

## Cite as

> Hentschel, J., Rammos, Y., Neuwirth, M., Moss, F. C., & Rohrmeier, M. (2024). An annotated corpus of tonal piano music from the long 19th century. Empirical Musicology Review, 18(1), 84–95. https://doi.org/10.18061/emr.v18i1.8903

## License

Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License ([CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)).

![cc-by-nc-sa-image](https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png)

## File naming convention

The file names listed in the [Overview](#overview) below refer to the following pieces:

| Opus  |No.| Key           | Title                | Included |
|-------|---|---------------|----------------------|----------|
| 8     | 1 | C minor       |                      | yes      |
| 8     | 2 | C minor       |                      | no       |
| 9     | 1 | F minor       |                      | no       |
| 9     | 2 | C major       |                      | no       |
| 9     | 3 | G major       |                      | no       |
| 14    | 1 | F minor       | Ophelia's Song       | yes      |
| 14    | 2 | E minor       | March of the Paladin | no       |
| 20    | 1 | B flat minor  |                      | no       |
| 20    | 2 | B minor       | Campanella           | no       |
| 26    | 1 | E flat major  |                      | yes      |
| 26    | 2 | E flat major  |                      | yes      |
| 26    | 3 | F minor       |                      | yes      |
| 26    | 4 | F sharp minor |                      | yes      |
| 31    | 3 | G sharp minor |                      | no       |
| 34    | 1 | B minor       | Magic Violin         | yes      |
| 34    | 2 | E minor       |                      | yes      |
| 34    | 3 | A minor       | Wood Spirit          | yes      |
| 34    | 4 | D minor       |                      | yes      |
| 35    | 1 | C major       |                      | yes      |
| 35    | 2 | G major       |                      | yes      |
| 35    | 2 | A minor       |                      | yes      |
| 35    | 4 | C sharp minor |                      | yes      |
| 42    | 1 | F minor       | Russian Tale         | yes      |
| 42    | 2 | C minor       | Phrygian             | yes      |
| 42    | 3 | G sharp minor |                      | yes      |
| 48    | 1 | C major       | Dance Tale           | yes      |
| 48    | 2 | G minor       | Tale of the Elves    | yes      |
| 51    | 1 | D minor       |                      | no       |
| 51    | 2 | A minor       |                      | no       |
| 51    | 3 | A major       |                      | no       |
| 51    | 4 | F sharp minor |                      | no       |
| 51    | 5 | F sharp minor |                      | no       |
| 51    | 6 | G major       |                      | no       |
| 54    | 2 | C minor       | Bird's Tale          | no       |
| 54    | 4 | E minor       | Scherzo              | no       |
| 54    | 6 | D minor       | The Organ Grinder    | no       |
| 54    | 8 | E minor       | The Beggar           | no       |
| deest |   | D minor       |                      | no       |

## Overview
|file_name|measures|labels|standard|                 annotators                 |   reviewers    |
|---------|-------:|-----:|--------|--------------------------------------------|----------------|
|op08n01  |      81|   213|2.3.0   |Wendelin Bitzan (2.2.0), John Heilig (2.3.0)|Adrian Nagel, DK|
|op14n01  |      85|   265|2.3.0   |Wendelin Bitzan (2.2.0), John Heilig (2.3.0)|Adrian Nagel, DK|
|op26n01  |      47|   180|2.3.0   |Wendelin Bitzan (2.2.0), John Heilig (2.3.0)|Adrian Nagel, DK|
|op26n02  |      65|   166|2.3.0   |Wendelin Bitzan (2.2.0), John Heilig (2.3.0)|Adrian Nagel, DK|
|op26n03  |      81|   116|2.3.0   |Wendelin Bitzan (2.2.0), John Heilig (2.3.0)|Adrian Nagel, DK|
|op26n04  |      77|   300|2.3.0   |Wendelin Bitzan (2.2.0), John Heilig (2.3.0)|Adrian Nagel, DK|
|op34n01  |     237|   669|2.3.0   |Wendelin Bitzan (2.2.0), John Heilig (2.3.0)|Adrian Nagel, DK|
|op34n02  |      48|   195|2.3.0   |Wendelin Bitzan (2.2.0), John Heilig (2.3.0)|Adrian Nagel, DK|
|op34n03  |     144|   408|2.3.0   |Wendelin Bitzan (2.2.0), John Heilig (2.3.0)|Adrian Nagel, DK|
|op34n04  |      61|   323|2.3.0   |Wendelin Bitzan (2.2.0), John Heilig (2.3.0)|Adrian Nagel, DK|
|op35n01  |      75|   272|2.3.0   |Wendelin Bitzan (2.2.0), John Heilig (2.3.0)|Adrian Nagel, DK|
|op35n02  |     139|   422|2.3.0   |Wendelin Bitzan (2.2.0), John Heilig (2.3.0)|AN, JH, AB      |
|op35n03  |      80|   320|2.3.0   |Wendelin Bitzan (2.2.0), John Heilig (2.3.0)|AN, AB          |
|op35n04  |     122|   345|2.3.0   |Wendelin Bitzan (2.2.0), John Heilig (2.3.0)|AN, AB          |
|op42n01  |     134|   479|2.3.0   |Wendelin Bitzan (2.2.0), John Heilig (2.3.0)|AN, AB          |
|op42n02  |      67|   178|2.3.0   |Wendelin Bitzan (2.2.0), John Heilig (2.3.0)|AN, AB          |
|op42n03  |     182|   504|2.3.0   |Wendelin Bitzan (2.2.0), John heilig (2.3.0)|Adrian Nagel    |
|op48n01  |     553|   871|2.3.0   |Wendelin Bitzan, John Heilig (2.3.0)        |Adrian Nagel, VZ|
|op48n02  |     186|   282|2.3.0   |Wendelin Bitzan (2.2.0), John Heilig (2.3.0)|Adrian Nagel, VZ|


*Overview table automatically updated using [ms3](https://ms3.readthedocs.io/).*
