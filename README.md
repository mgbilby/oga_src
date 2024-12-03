# oga_src

## Purpose

This repository contains a simplified version and value-added adaptation of the Opera Graeca Adnotata (hereafter, OGA). The OGA corpus used here is version 0.2.0 (released 2024-11-24).

Useability of OGA may pose an issue for  researchers and general users because of:
 - the size of the [corpus on Zenodo](https://doi.org/10.5281/zenodo.14206061) (8.6 GB zipped)
 - the process of unpacking several subdirectory zip files
 - the complexity of navigating the OGA subdirectory structure
 - the large number of files for each document
 - the complex dependency relationships among files in the corpus
 - different document versions for the progressive stages of morphosyntactical processing
 - several layers of resulting [standoff annotation](https://varro.informatik.uni-leipzig.de/oga/en/standoff_annotation.html)

This adaptation of OGA contains just one file per document, all located in a single directory. Each file is in the Universal Dependencies CoNNLu format. This format and simple repository organization facilitates the broadest possible access and ease of use. 

Embedded in each CoNNLu file are supplemental fields extracted and built from document-related xml files provided by OGA as described in the next two sections.

## Sentence headers

Sentence headers are newly added. Each header contains three lines: source, text, and sent_id.

 - The first header line represents the document source, including the author (extracted from anno_author.xml), title (extracted from anno.title.xml), and an automatically calculated internal document location or range. The latter derives from the adjusted word token MISC fields.
 - The second header line contains the full text of the sentence, concatenating each sentence's tokens into a single string. All tokens are included, whether words, punctuation marks, or ellipses (syntactically necessary, yet implicit words). The concatenation generates a human-readable sentence, with the caveat that single space padding separates all tokens.
 - The third header line contains the sequential number of each sentence within the document. These numbers derive from an automated count of all sentences and insertion routine.

In the file, the header fields 

"# source = [author], [title] [internal_location_start]-[internal_location_end]"
"# text = [concatenation of all words and punctuation marks in the sentence]"
"# sent_id = [sentence_number_in_document_sequence]"

A sample sentence header follows:

 - "# source = Plutarch, De Heroditi malignate 1"
 - "# text = τοῦ Ἡροδότου πολλοὺς μέν , ὦ Ἀλέξανδρε , καὶ ἡ λέξις ὡς ἀφελὴς καὶ δίχα πόνου καὶ ῥᾳδίως ἐπιτρέχουσα τοῖς πράγμασιν ἐξηπάτηκε ·"
 - "# sent_id = 1"

## Word locations

To the last or rightmost field for each word token, which is called the "MISC" field in the CoNNLu format, an internal document location description is appended. This location follows immediately after the OGA token id, represented as t_[number]. A vertical bar separates the internal field values. The information is pulled from the internal document annotations found in the OGA xml files ending in "tok01_cts01". Internal location types and depths vary based on the document.

What follows are several out-of-the-box and adjusted MISC field samples, all representing the third word token (t_3) found in a variety of authors and genres.

| Author | OGA MISC | oga_src MISC |
|------------------|-----------------|-----------------|
| Aelius Herodianus   | t_3 | t_3\|ref=Περὶ ὀρθογραφίας_1.1.1.1    |
| Homeric Hymns   | t_3 | t_3\|ref=Hymn 14 to the Mother of the Gods_1    |
| Isaeus   | t_3 | t_3\|ref=On The Estate of Apollodorus_0    |
| New Testament   | t_3 | t_3\|ref=Matthew_1.1    |
| Plato   | t_3 | t_3\|ref=Cleitophon_406    |
| Plutarch   | t_3 | t_3\|ref=Alexander_1.1    |
| Themistocles   | t_3 | t_3\|ref=Epistulae_1    |


## Data sources

Version 0.2.0 of the Opera Graeca Adnotata, curated by Giuseppe Celano at the University of Leipzig, was archived at [Zenodo]( https://doi.org/10.5281/zenodo.14206061) on 2024-11-24, and is the sole source of the data used in this repository. 

The OGA corpus v0.2.0 contains annotations of 40M+ base tokens and 1999 base texts/files. These files were in turn derived from several major corpora of digital editions of classical Greek texts, especially the Perseus Project (Tufts University) and closely connected First1KGreek project (Mount Allison University, Tufts University, University of Leipzig, University of Virginia), along with the Thesaurus Linguae Graecae (University of California, Irvine) and the Patristic Text Archive (Berlin-Brandenburg Academy of Sciences and Humanities).

OGA annotation includes morphosyntactical features based on the [Ancient Greek Dependency Treebank, or AGDT](https://github.com/PerseusDL/treebank_data/blob/master/AGDT2/guidelines/Greek_guidelines.md), as well as data (sometimes provisional) pertaining to authorship and likely date or date range of composition.

Elsewhere I have archived a [simple comparison of documents in the OGA and GLAUx coropra](https://doi.org/10.5281/zenodo.14254072), which shows at a glance which documents are unique to OGA, which are unique to GLAUx, and which texts overlap between the two.

## Citation

The OGA corpus was described in this earlier article that corresponds to v0.1.0.

> Giuseppe G. A. Celano, "Opera Graeca Adnotata: Building a 34M+ Token Multilayer Corpus for Ancient Greek", arXiv cs.CL, 2024-03-41, https://doi.org/10.48550/arXiv.2404.00739.

