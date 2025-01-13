# oga_src

## Purpose

This repository contains a simplified version and value-added adaptation of the Opera Graeca Adnotata (hereafter, OGA). The OGA corpus version used here is v0.2.0, released 2024-11-24, containing annotations of 40M+ base tokens and 1999 base documents.

Useability of OGA may pose an issue for  researchers and general users because of:
 - the size of the [corpus on Zenodo](https://doi.org/10.5281/zenodo.14206061) (8.6 GB zipped)
 - the process of unpacking several subdirectory zip files
 - the complexity of navigating the OGA subdirectory structure
 - the large number of files for each document
 - the complex dependency relationships among files in the corpus
 - different document versions for the progressive stages of morphosyntactical processing
 - several layers of resulting [standoff annotation](https://varro.informatik.uni-leipzig.de/oga/en/standoff_annotation.html)

This adaptation of OGA contains just one file per document, all located in a single directory. Each file is in the Universal Dependencies CoNNL-U format. This format and simple repository organization facilitates the broadest possible access and ease of use. 

Embedded in each CoNNL-U file are supplemental fields extracted and built from document-related xml files provided by OGA as described in the next two sections.

## Sentence headers

Sentence headers are newly added. Each header contains three lines: source, text, and sent_id.

 - The first header line represents the document source, including the author (extracted from anno_author.xml), title (extracted from anno.title.xml), and an automatically calculated internal document location or range. The latter derives from the adjusted word token MISC fields. Author names are sometimes shortened or abbreviated. Titles are usually abbreviated. For more details on title abbreviations, see #2 below in the MISC field expansion description.
 - The second header line contains the full text of the sentence, concatenating each sentence's tokens into a single string. All tokens are included, whether words, punctuation marks, or ellipses (syntactically necessary, yet implicit words). The concatenation generates a human-readable sentence, with the caveat that single space padding separates all tokens.
 - The third header line contains the sequential number of each sentence within the document. These numbers derive from an automated count of all sentences and insertion routine.

In the file, the header fields are structured as follows:

\# source = [author], [title]_[internal_location_start]-[internal_location_end]  
\# text = [concatenation of all words and punctuation marks in the sentence]  
\# sent_id = [sentence_number_in_document_sequence]  

A sample sentence header follows:

\# source = Plutarch, Herod.malign._1  
\# text = τοῦ Ἡροδότου πολλοὺς μέν , ὦ Ἀλέξανδρε , καὶ ἡ λέξις ὡς ἀφελὴς καὶ δίχα πόνου καὶ ῥᾳδίως ἐπιτρέχουσα τοῖς πράγμασιν ἐξηπάτηκε ·  
\# sent_id = 1  

## MISC field expansions: parent token id & token reference location

To the last or rightmost field for each word token, which is called the "MISC" field in the CoNNL-U format, two new subfields are added.

1. The parent's document-wide id token id (t_#) or document-wide elliptical id (e_#). The CoNNL-U HEAD field values are internal to the sentence. These supplemental identifiers are mapped based on those HEAD values, while adding clarity and precision to syntactical analysis, particularly at the document level.

2. A document abbreviation and internal document location, which facilitates contextualization, comprehension, and comparisons with other digital editions. For well-known Classical texts, the abbreviations generally correspond to the [Perseus abbreviation list](https://www.perseus.tufts.edu/hopper/abbrevhelp). Document abbreviations for Christian texts are a mix of commonplace scholarly abbreviations (SBL, Lampe) and abbreviations that I've minted for this specific project, particularly for texts that have longer titles or are not cited as commonly in the scholarly literature. The internal document locations/references are pulled from the location codes in the OGA xml files ending in "tok01_cts01". As is evident in the table below, internal location types and depths can vary considerably from document to document.

What follows are several out-of-the-box and adjusted MISC field samples, all representing the third word token (t_3) found in a variety of authors and genres.

| cts_urn | OGA MISC | oga_src MISC |
|------------------|-----------------|-----------------|
| tlg0087.tlg011   | t_3 | t_3\|0\|ref=orthog_1.1.1.1    |
| tlg0013.tlg014   | t_3 | t_3\|t_5\|ref=HH14.Mat._1    |
| tlg0017.tlg012   | t_3 | t_3\|t_4\|ref=Isaeus 12_0    |
| tlg0031.tlg001   | t_3 | t_3\|t_2\|ref=Matt_1.1    |
| tlg0059.tlg029   | t_3 | t_3\|t_8\|ref=Cleit._406    |
| tlg0007.tlg047   | t_3 | t_3\|t_2\|ref=Alex._1.1   |
| tlg0055.tlg001   | t_3 | t_3\|t_1\|ref=ep._1   |

## Other corrections and adjustments

The document-wide token id values--the first substring of each MISC field--are adjusted to separate sequential numbering for ellipses (or elliptical) tokens: e_1, e_2, e_3, etc.

The file for tlg5026.tlg001 was split into two roughly equal halves, following [this Issue conversation](https://github.com/OpenGreekAndLatin/First1KGreek/issues/2808), because the file size exceeded the 100MB threshold permitted by standard Github operations. This brings the total file count of oga_src to 2000 files, one more than the 1999 documents in the OGA corpus.

## Data sources

Version 0.2.0 of the Opera Graeca Adnotata, curated by Giuseppe Celano at the University of Leipzig, was archived at [Zenodo](https://doi.org/10.5281/zenodo.14206061) on 2024-11-24, and is the sole source of the data used in this repository. 

The OGA corpus was in turn derived from several major corpora of digital editions of classical Greek texts, most notably the [Perseus Project](https://github.com/PerseusDL/canonical-greekLit) (Department of Classics, Tufts University) and closely connected [First1KGreek](https://github.com/OpenGreekAndLatin/First1KGreek) project. First1KGreek is funded by the "Harvard Library Arcadia Fund, European Social Fund, and the Alexander-von-Humboldt professorship for Digital Humanities at Leipzig. The data has been produced in an international cooperation with the Center for Hellenic Studies, the Harvard Library, Mount Alison University, Tufts University, the University of Leipzig, and the University of Virginia." Significant contributions, particularly to Patristic and early Christian literature, were made available to OGA through the [Patristic Text Archive](https://github.com/PatristicTextArchive/pta_data) thanks to funding from Academies Programme and housed at the Berlin-Brandenburg Academy of Sciences and Humanities. Contributions of digital editions and most of the canonical text service ontology come by way of the famous [Thesaurus Linguae Graecae](https://stephanus.tlg.uci.edu/index.php#login=true) centered at the University of California, Irvine.

OGA annotation includes morphosyntactical features based on the [Ancient Greek Dependency Treebank, or AGDT](https://github.com/PerseusDL/treebank_data/blob/master/AGDT2/guidelines/Greek_guidelines.md), as well as data (sometimes provisional) pertaining to authorship and likely date or date range of composition.

Elsewhere I have archived a [simple comparison of documents in the OGA and GLAUx corpora](https://doi.org/10.5281/zenodo.14254072), which shows at a glance which documents are unique to OGA, which are unique to GLAUx, and which texts overlap between the two.

## Citation

The OGA corpus was described in this earlier article that corresponds to v0.1.0.

> Giuseppe G. A. Celano, "Opera Graeca Adnotata: Building a 34M+ Token Multilayer Corpus for Ancient Greek", arXiv cs.CL, 2024-03-41, https://doi.org/10.48550/arXiv.2404.00739.
