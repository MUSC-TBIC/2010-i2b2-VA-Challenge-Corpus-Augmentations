
This repository provides documentation to explain our augmentations of
a subset of the 2010 i2b2/VA Challenge corpus to include any
laboratory test values associated with an already annotated laboratory test
name.  These laboratory test values are also linked through annotation
relations with their respective laboratory test name.

Due to the conditions of the data use agreement (DUA) of the original
corpus, you are accessing these annotations via Harvard Medical
School's Department of Biomedical Informatics (DBMI) `data portal
<https://portal.dbmi.hms.harvard.edu/data-sets/>`_. This documentation
for these annotations (but not the annotations themselves) is
replicated in the following repository:
https://github.com/MUSC-TBIC/2010-i2b2-VA-Challenge-Corpus-Augmentations

Annotation Process
==================

Heider et al. [1] present further details on the annotation process.
We began with the normalized concept annotations available in the 2019
n2c2 NLP challenge corpus [2]. These annotations included problems,
test, and treatments. We wanted only those annotations related to
laboratory test names. As such, we filtered to include any annotations
with a concept unique identifier (CUI) with the following semantic types:

- Laboratory Procedure (T059)
- Laboratory or Test Result (T034)

These annotations were automatically added to the laboratory test name
list. We then used a second filter to find all annotations with a
semantic type from the following list:

- Antibiotic (T195)
- Bacterium (T007)
- Biologically Active Substance (T123)
- Fungus (T004)
- Immunologic Factor (T129)
- Pharmacologic Substance (T121)
- Virus (T005)
- Vitamin (T127)

This second set of annotations was manually reviewed for inclusion (or
exclusion).

Between these two lists, we had a subset of all original annotations
that related to laboratory test names (and their CUIs). The text
surrounding all of these annotations was automatically searched for
potential laboratory test values. The first search criteria to succeed
was treated as the primary laboratory test value to associate with a
given laboratory test name. The three search criteria were:

1. the nearest numeric expression (e.g., '10,000', '30%') up to fifty
   characters after a concept
2. the nearest numeric expression up to 10 characters before the
   concept
3. the closest categorical value (e.g., 'positive' or 'normal') up to
   fifty characters away

These automatically discovered laboratory test values (and their
relation arches back to laboratory test names) were manually verified
using WebAnno. Any missed laboratory test values were added. Any
incorrectly linked laboratory test values were removed.

A single individual did all of the manual verification. As such, there
is no inter annotator agreement.

Directory Structure
===================

The abstract for Heider et al. [1] is included in the ``docs`` folder.
(The two other publications, which document the corpus creation
process of the antecedent versions, can be retrieved via the provided
links.)

The notes (and annotations) have been split into a 50/50 train/test
split as per Luo et al.'s [2] corpus. The original notes (in plain
text format) are under the ``*_note`` folders. The brat ``.ann``
formatted annotation files are in the ``*_ann`` folders.

The configuration files using for manual verification in WebAnno are
provided in the ``webanno`` directory.

::

  . 
  |-- docs 
  |-- test
  |  |-- test_ann
  |   `-- test_note
  |-- train
  |   |-- train_ann
  |   `-- train_note
  `-- webanno


Links
=====

- This documentation for these annotations (but not the annotations themselves) is replicated in the following repository:  https://github.com/MUSC-TBIC/2010-i2b2-VA-Challenge-Corpus-Augmentations
- Supplemental script repository (within the ``n2c2`` subdirectory):  https://github.com/MUSC-TBIC/corpus-utils 
- Original challenge overview page:  `2019 n2c2 Shared-Task and Workshop Track 3: n2c2/UMass Track on Clinical Concept Normalization <https://n2c2.dbmi.hms.harvard.edu/track3>`_
- Data page: `n2c2 2019 - Track 3: Clinical Concept Normalization <https://portal.dbmi.hms.harvard.edu/projects/n2c2-2019-t3/>`_


References
==========

1. Heider PM, Kim Y, Meystre SM. Semi-Automated Corpus Augmentation
Methods for Enriching Laboratory Test Names with Value Annotations.
AMIA Informatics Summit. 2021.

2. Luo YF, Sun W, Rumshisky A. `MCN: A Comprehensive Corpus for
Medical Concept Normalization
<https://www.ncbi.nlm.nih.gov/pubmed/30802545>`_. Journal of
Biomedical Informatics. 2019 Feb 22:103132.

3. Uzuner O, South BR, Shen S, DuVall SL, `2010 i2b2/VA challenge on
concepts, assertions, and relations in clinical text
<https://doi.org/10.1136/amiajnl-2011-000203>`_, Journal of the
American Medical Informatics Association, Volume 18, Issue 5,
September 2011, Pages 552-556.
