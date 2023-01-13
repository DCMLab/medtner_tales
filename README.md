<!-- TOC -->
* [Nikolai Medtner - Tales](#nikolai-medtner---tales)
  * [Getting the data](#getting-the-data)
    * [With full version history](#with-full-version-history)
    * [Without full version history](#without-full-version-history)
  * [Data Formats](#data-formats)
    * [Opening Scores](#opening-scores)
    * [Opening TSV files in a spreadsheet](#opening-tsv-files-in-a-spreadsheet)
    * [Loading TSV files in Python](#loading-tsv-files-in-python)
  * [How to read `metadata.tsv`](#how-to-read-metadatatsv)
    * [File information](#file-information)
    * [Composition information](#composition-information)
    * [Score information](#score-information)
    * [Identifiers](#identifiers)
  * [Generating all TSV files from the scores](#generating-all-tsv-files-from-the-scores)
  * [Questions, Suggestions, Corrections, Bug Reports](#questions-suggestions-corrections-bug-reports)
  * [License](#license)
  * [Naming convention](#naming-convention)
* [Overview](#overview)
<!-- TOC -->

# Nikolai Medtner - Tales

This corpus has been created within the [DCML corpus initiative](https://github.com/DCMLab/dcml_corpora) and employs
the [DCML harmony annotation standard](https://github.com/DCMLab/standards).

It is part of a larger dataset that has been submitted for publication as 
`Hentschel, J., Rammos, Y., Neuwirth, M., Rohrmeier, M. (forthcoming). 
An Annotated Corpus of Tonal Piano Music from the Long 19th Century`.

## Getting the data

### With full version history

The dataset is version-controlled via [git](https://git-scm.com/). In order to download the files with all
revisions they have gone through, git needs to be installed on your machine. Then you can clone this 
repository using the command

```bash
git clone https://github.com/DCMLab/medtner_tales.git
```

### Without full version history

If you are only interested in the current version of the corpus, you can simply download and unpack
[this ZIP file](https://github.com/DCMLab/medtner_tales/archive/refs/heads/main.zip).


## Data Formats

Each piece in this corpus is represented by four files with identical names, each in its own folder. For example, 
the first tale has the following files:

* `MS3/op08n01.mscx`: Uncompressed MuseScore file including the music and annotation labels.
* `notes/op08n01.tsv`: A table of all note heads contained in the score and their relevant features (not each of them represents an onset, some are tied together)
* `measures/op08n01.tsv`: A table with relevant information about the measures in the score.
* `harmonies/op08n01.tsv`: A list of the included harmony labels (including cadences and phrases) with their positions in
  the score.

### Opening Scores

After navigating to your local copy, you can open the scores in the folder `MS3` with the free and open source score
editor [MuseScore](https://musescore.org). Please note that the scores have been edited, annotated and tested with
[MuseScore 3.6.2](https://github.com/musescore/MuseScore/releases/tag/v3.6.2). 
MuseScore 4 has since been released and preliminary tests suggest that it renders them correctly.

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
`pip install -U ms3` (requires Python 3.10) you'll be able to load any TSV like this:

```python
import ms3

labels = ms3.load_tsv('harmonies/op08n01.tsv')
notes = ms3.load_tsv('notes/op08n01.tsv')
```

## How to read `metadata.tsv`

This section explains the meaning of the columns contained in `metadata.tsv`.

### File information

| column                 | content                                                    |
|------------------------|------------------------------------------------------------|
| **fname**              | name without extension (for referencing related files)     |
| **rel_path**           | relative file path of the score, including extension       |
| **subdirectory**       | folder where the score is located                          |    
| **last_mn**            | last measure number                                        |
| **last_mn_unfolded**   | number of measures when playing all repeats                |
| **length_qb**          | length of the piece, measured in quarter notes             |
| **length_qb_unfolded** | length of the piece when playing all repeats               |
| **volta_mcs**          | measure counts of first and second endings                 |
| **all_notes_qb**       | summed up duration of all notes, measured in quarter notes |
| **n_onsets**           | number of note onsets                                      |
| **n_onset_positions**  | number of unique note onsets ("slices")                    |


### Composition information

| column             | content                   |
|--------------------|---------------------------|
| **composer**       | composer name             |
| **workTitle**      | work title                |
| **composed_start** | earliest composition date |
| **composed_end**   | latest composition date   |
| **workNumber**     | Catalogue number(s)       |
| **movementNumber** | 1, 2, or 3                |
| **movementTitle**  | title of the movement     |

### Score information

| column          | content                                                |
|-----------------|--------------------------------------------------------|
| **label_count** | number of chord labels                                 |
| **KeySig**      | key signature(s) (negative = flats, positive = sharps) |
| **TimeSig**     | time signature(s)                                      |
| **musescore**   | MuseScore version                                      |
| **source**      | URL to the first typesetter's file                     |
| **typesetter**  | first typesetter                                       |
| **annotators**  | creator(s) of the chord labels                         |
| **reviewers**   | reviewer(s) of the chord labels                        |

### Identifiers

These columns provide a mapping between multiple identifiers for the sonatas (not for individual movements).

| column          | content                                                                                                 |
|-----------------|---------------------------------------------------------------------------------------------------------|
| **wikidata**    | URL of the [WikiData](https://www.wikidata.org/) item                                                   |
| **viaf**        | URL of the Virtual International Authority File ([VIAF](http://viaf.org/)) entry                        |
| **musicbrainz** | [MusicBrainz](https://musicbrainz.org/) identifier                                                      |
| **imslp**       | URL to the wiki page within the International Music Score Library Project ([IMSLP](https://imslp.org/)) |


## Generating all TSV files from the scores

When you have made changes to the scores and want to update the TSV files accordingly, you can use the following
command (provided you have pip-installed [ms3](https://github.com/johentsch/ms3)):

```python
ms3 extract -M -N -X -D # for measures, notes, expanded annotations, and metadata
```

If, in addition, you want to generate the reviewed scores with out-of-label notes colored in red, you can do

```python
ms3 review -M -N -X -D # for extracting measures, notes, expanded annotations, and metadata
```

By adding the flag `-c` to the review command, it will additionally compare the (potentially modified) annotations in the score
with the ones currently present in the harmonies TSV files and reflect the comparison in the reviewed scores.

## Questions, Suggestions, Corrections, Bug Reports

For questions, remarks etc., please create an issue and feel free to fork and submit pull requests.

## License

Creative Commons Attribution-ShareAlike 4.0 International License ([CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)).

## Naming convention

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

# Overview
|file_name|measures|labels|standard|  annotators   | reviewers  |
|---------|-------:|-----:|--------|---------------|------------|
|op08n01  |      81|   213|2.2.0   |Wendelin Bitzan|Adrian Nagel|
|op14n01  |      85|   265|2.2.0   |Wendelin Bitzan|Adrian Nagel|
|op26n01  |      47|   180|2.2.0   |Wendelin Bitzan|Adrian Nagel|
|op26n02  |      65|   166|2.2.0   |Wendelin Bitzan|Adrian Nagel|
|op26n03  |      81|   116|2.2.0   |Wendelin Bitzan|Adrian Nagel|
|op26n04  |      77|   300|2.2.0   |Wendelin Bitzan|Adrian Nagel|
|op34n01  |     237|   669|2.2.0   |Wendelin Bitzan|Adrian Nagel|
|op34n02  |      48|   195|2.2.0   |Wendelin Bitzan|Adrian Nagel|
|op34n03  |     144|   408|2.2.0   |Wendelin Bitzan|Adrian Nagel|
|op34n04  |      61|   323|2.2.0   |Wendelin Bitzan|Adrian Nagel|
|op35n01  |      75|   272|2.2.0   |Wendelin Bitzan|Adrian Nagel|
|op35n02  |     139|   422|2.2.0   |Wendelin Bitzan|Adrian Nagel|
|op35n03  |      80|   320|2.2.0   |Wendelin Bitzan|Adrian Nagel|
|op35n04  |     122|   345|2.2.0   |Wendelin Bitzan|Adrian Nagel|
|op42n01  |     134|   479|2.2.0   |Wendelin Bitzan|Adrian Nagel|
|op42n02  |      67|   178|2.2.0   |Wendelin Bitzan|Adrian Nagel|
|op42n03  |     182|   552|2.2.0   |Wendelin Bitzan|Adrian Nagel|
|op48n01  |     553|  1020|2.2.0   |Wendelin Bitzan|Adrian Nagel|
|op48n02  |     186|   307|2.2.0   |Wendelin Bitzan|Adrian Nagel|


*Overview table updated using [ms3](https://johentsch.github.io/ms3/) 1.1.1.*
