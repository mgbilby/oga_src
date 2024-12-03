# oga_src

## Purpose

This repository contains a simplified version and value-added adaptation the Opera Graeca Adnotata (hereafter, OGA). The OGA corpus used here is version 0.2.0 (released 2024-11-24).

Useability of OGA may pose an issue for  researchers and general users because of:
 - the size of the [corpus on Zenodo](https://doi.org/10.5281/zenodo.14206061) (8.6 GB zipped)
 - the process of unpacking several subdirectory zip files
 - the complexity of navigating the OGA subdirectory structure
 - the large number of files for each document
 - the complex dependency relationships among files in the corpus
 - different document versions for the progressive stages of morphosyntactical processing
 - several layers of resulting [standoff annotation](https://varro.informatik.uni-leipzig.de/oga/en/standoff_annotation.html)

This adaptation of OGA contains just one file per document, all in a single directory. Each file is in the Universal Dependencies CoNNLu format to facilitate the broadest possible access and ease of use. Embedded in each CoNNLu file are supplemental fields pulled from document-related xml files provided by OGA, described in the next two sections.

## Sentence headers

Sentence headers are added in keeping with typical conllu conventions, containing the following information:
 - "# source = [author], [title] [internal_location_start]-[internal_location_end]"
 - "# text = [concatenation of all words and punctuation marks in the sentence]"
 - "sent_id = [sentence_number_in_document_sequence]"

Here is an example:

 - "# source = Plutarch, De Heroditi malignate 1"
 - "# text = τοῦ Ἡροδότου πολλοὺς μέν , ὦ Ἀλέξανδρε , καὶ ἡ λέξις ὡς ἀφελὴς καὶ δίχα πόνου καὶ ῥᾳδίως ἐπιτρέχουσα τοῖς πράγμασιν ἐξηπάτηκε ·"
 - "# sent_id = 1"

## Word locations

To the last or rightmost field for each word token, which is called the "MISC" field in the CoNNLu format, an internal document location description is appended. This location follows immediately after the OGA token id, represented as t_[number]. A vertical bar separates the internal field values. Location types and depths vary based on the document. 

Here are some sample MISC fields from the third word token of various documents.

 - Aelius Herodianus: t_3|ref=Περὶ ὀρθογραφίας_1.1.1.1
 - Homeric Hymns: t_3|ref=Hymn 14 to the Mother of the Gods_1
 - Isaeus: t_3|ref=On The Estate of Apollodorus_0
 - New Testament, Matthew: t_3|ref=Matthew_1.1
 - PLato: t_3|ref=Cleitophon_406
 - Plutarch: t_3|ref=Alexander_1.1
 - Themistocles: t_3|ref=Epistulae_1

## Data source

Version 0.2.0 of the Opera Graeca Adnotata, curated by Giuseppe Celano at the University of Leipzig, was archived on November 24, 2024 on [Zenodo]( https://doi.org/10.5281/zenodo.14206061). 

The corpus annotates 40M+ base tokens and 1999 base texts/files, derived from various major corpora of digital editions of classical Greek texts, such as Perseus, First1KGreek, Thesaurus Linguae Graecae, and the Patristic Text Archive.

OGA annotation includes morphosyntactical features based on the Ancient Greek and Latin Dependency Treebank convention, as well as data (sometimes provisional) pertaining to authorship and likely date or date range of  composition.

Elsewhere I have archived a [simple comparison of OGA documents and GLAUx documents](https://doi.org/10.5281/zenodo.14254072), which shows at a glance which documents are unique to OGA, which are unique to GLAUx, and which texts overlap between the two.

## Citation

The OGA corpus was described in this earlier article that corresponds to v0.1.0.

> Giuseppe G. A. Celano, "Opera Graeca Adnotata: Building a 34M+ Token Multilayer Corpus for Ancient Greek", arXiv cs.CL, 2024-03-41, https://doi.org/10.48550/arXiv.2404.00739.

## License and Reuse

The OGA corpus was archived under a CC BY-SA 4.0 international license. This share-alike license requires that derivatives also be shared on like terms. Thus this oga_src repository of CoNNLu files is also archived under a CC BY-SA 4.0 license.

## Disclaimer

THE DATA ARE PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE AND DATA OR THE USE OF OR OTHER DEALINGS IN THE SOFTWARE OR DATA.

