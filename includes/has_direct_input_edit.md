Back to [Annotation usage examples for each annotation extension relation](http://wiki.geneontology.org/index.php/Annotation_usage_examples_for_each_annotation_extension_relation)

Back to [Annotation usage examples for has input](http://wiki.geneontology.org/index.php/Annotation_Extension_Relation:has_input)

!INCLUDES "has_direct_input_inc.md"

Comment
-------

To use this relationship there must be evidence that the gene product in column 2 is known/predicted to bind the molecular target in column 16.

This can be a co-immunoprecipitation (for example) demonstrated in the paper being annotated, or from evidence available in another paper, or from evidence of protein interactions which have been demonstrated in another paper for orthologous molecules.

Without evidence of a relevant interaction use the relationship has\_input

Synonyms
--------

directly\_localizes (NARROW)

has\_direct\_target (EXACT)

has\_substrate (NARROW)

Child terms
-----------

-   None

Annotation Extension Usage Examples
-----------------------------------

### Enhancing Molecular Function and Biological Process Annotations

#### Specifying the DNA sequence that was bound by a gene product

**Transcription factor binding to potential target sequences in vitro:**

Statement from paper:

*By performing gel electrophoretic mobility shift assays, we could detect efficient binding of Atf-2 to the elements found in the bec-1 and lgg-1 promoters (Fig. 5C).*

(Note that binding to lin-48 is also reported as a positive control).

| Gene Name (col 2)                                     | GO ID (col 5)                                                                                 | Reference (col 6) | Evidence (col 7) | Annotation Extension (col 16)                                                                                                                                                                                                           |
|-------------------------------------------------------|-----------------------------------------------------------------------------------------------|-------------------|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| WBGene00000220 <span style="color:green">Atf-2</span> | <GO:0001012> <span style="color:green">RNA polymerase II regulatory region DNA binding</span> | <PMID:21502138>   | IDA              | has\_direct\_input(WB:WBGene00000247 <span style="color:green">bec-1</span>)|has\_direct\_input(WB:WBGene00002980 <span style="color:green">lgg-1</span>)|has\_direct\_input(WB:WBGene00003033 <span style="color:green">lin-48</span>) |

#### Specifying the target molecule of an enzyme activity

**Targets of protein kinase activity:**

Example 1 Statement from paper:

*A final line of evidence that BAF-1 is a substrate for VRK-1 was obtained with purified recombinant proteins, which demonstrated that BAF-1 was phosphorylated by VRK-1 in vitro (Figure 4H, lower panel). In addition, VRK-1 was autophosphorylated (Figure 4H, upper panel).*

| Gene Name (col 2)                                     | GO ID (col 5)                                                         | Reference (col 6) | Evidence (col 7) | Annotation Extension (col 16)                                                                                                                             |
|-------------------------------------------------------|-----------------------------------------------------------------------|-------------------|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| WBGene00017895 <span style="color:green">Vrk-1</span> | <GO:0004672> <span style="color:green">protein kinase activity</span> | <PMID:17170708>   | IDA              | has\_direct\_input(WB:WBGene00000235 <span style="color:green">baf-1</span>)|has\_direct\_input(WB:WBGene00017895 <span style="color:green">vrk-1</span>) |

Example 2:

*If protein SGD:A phosphorylates protein SGD:B then annotate A to:*

| Gene Name (col 2)                        | GO ID (col 5)                                                         | Reference (col 6) | Evidence (col 7) | Annotation Extension (col 16)                                |
|------------------------------------------|-----------------------------------------------------------------------|-------------------|------------------|--------------------------------------------------------------|
| SGD:A <span style="color:green">A</span> | <GO:0004672> <span style="color:green">protein kinase activity</span> | <PMID:17170708>   | IDA              | has\_direct\_input(SGD:B <span style="color:green">B</span>) |

NOTE we would not include a separate annotation line for B, because we only have annotation lines for active participants

Strictly speaking, the input is SGD:B in the unphosphorylated state and the output is SGD:B in the phosphorylated state. However, currently we do not have IDs for these separate protein forms. Really B is both an input and an output. We standardize on has\_input here.

**Note there is no need to say:**

| Gene Name (col 2)                        | GO ID (col 5)                                                         | Reference (col 6) | Evidence (col 7) | Annotation Extension (col 16)                                                                                                     |
|------------------------------------------|-----------------------------------------------------------------------|-------------------|------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| SGD:A <span style="color:green">A</span> | <GO:0004672> <span style="color:green">protein kinase activity</span> | <PMID:17170708>   | IDA              | has\_direct\_input(SGD:B <span style="color:green">B</span>)|has\_direct\_input(CHEBI:15422 <span style="color:green">ATP</span>) |

**Or even:**

| Gene Name (col 2)                        | GO ID (col 5)                                                         | Reference (col 6) | Evidence (col 7) | Annotation Extension (col 16)                                                                                                                                                                                                                         |
|------------------------------------------|-----------------------------------------------------------------------|-------------------|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SGD:A <span style="color:green">A</span> | <GO:0004672> <span style="color:green">protein kinase activity</span> | <PMID:17170708>   | IDA              | has\_direct\_input(SGD:B <span style="color:green">B</span>)|has\_direct\_input(CHEBI:15422 <span style="color:green">ATP</span>)|has\_output(SGD:B <span style="color:green">B</span>)|has\_output(CHEBI:16761 <span style="color:green">ADP</span>) |

These are correct but this is pointless because the additional info is redundant with what we already know about kinase activity (this is actually made computable in MF x CHEBI)

Inclusion of the C16 information in the Molecular Function *protein kinase* and to the Biological Process *phosphorylation* can be useful, as these annotation extensions will not be created transitively. However, this information can be inferred computationally.

**If protein SGD:A phosphorylates protein SGD:B and SGD:C then annotate A to:**

| Gene Name (col 2)                        | GO ID (col 5)                                                         | Reference (col 6) | Evidence (col 7) | Annotation Extension (col 16)                                                                                             |
|------------------------------------------|-----------------------------------------------------------------------|-------------------|------------------|---------------------------------------------------------------------------------------------------------------------------|
| SGD:A <span style="color:green">A</span> | <GO:0004672> <span style="color:green">protein kinase activity</span> | <PMID:17170708>   | IDA              | has\_direct\_input(SGD:B <span style="color:green">B</span>)|has\_direct\_input(SGD:C <span style="color:green">C</span>) |

There is some redundancy with interaction databases here. Capturing this as GO annotation is more expressive as you can say "A phosphorylates B during pathway C". But if you want to capture this in interaction databases exclusively we have tools for generating GO annotations from these (just as we have tools for capturing GO annotations from pathway databases).

Using examples (from above) to demonstrate [Folding\_and\_Unfolding](Folding_and_Unfolding "wikilink") using the relationship has\_direct\_input
------------------------------------------------------------------------------------------------------------------------------------------------

#### Specifying the DNA sequence that was bound by a gene product

**Transcription factor binding to potential target sequences in vitro:**

Statement from paper:

*By performing gel electrophoretic mobility shift assays, we could detect efficient binding of Atf-2 to the elements found in the bec-1 and lgg-1 promoters (Fig. 5C).*

| Folded/unfolded | Gene Name (col 2)                                     | GO ID (col 5)                                                                                 | Reference (col 6) | Evidence (col 7) | Annotation Extension (col 16)                                                                                                                                                                                                             | Parent terms of new folded GO term                    |
|-----------------|-------------------------------------------------------|-----------------------------------------------------------------------------------------------|-------------------|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------|
| Unfolded        | WBGene00000220 <span style="color:green">atf-2</span> | <GO:0001012> <span style="color:green">RNA polymerase II regulatory region DNA binding</span> | <PMID:21502138>   | IDA              | has\_direct\_input(WB:WBGene00000247 <span style="color:green">bec-1</span>)| has\_direct\_input(WB:WBGene00002980 <span style="color:green">lgg-1</span>)| has\_direct\_input(WB:WBGene00003033 <span style="color:green">lin-48</span>) |                                                       |
| Folded          | WBGene00000220 <span style="color:green">atf-2</span> | <GO:0001012> <span style="color:green">RNA polymerase II regulatory region DNA binding</span> | <PMID:21502138>   | IDA              |                                                                                                                                                                                                                                           | <span style="color:red">No new GO term created</span> |

**OWL class expression:** is\_a <GO:0001012> <span style="color:red">RNA polymerase II regulatory region DNA binding</span> AND has\_direct\_input SOME WBGene00000220 <span style="color:red">atf-2</span>

------------------------------------------------------------------------

Back to [Annotation Extension: Capturing participants](http://wiki.geneontology.org/index.php/Annotation_Extension:_Capturing_participants)

Back to [Annotation usage examples for each annotation extension relation](http://wiki.geneontology.org/index.php/Annotation_usage_examples_for_each_annotation_extension_relation)

<Category:relations> [Category:annotation extension](Category:annotation extension "wikilink") [Category:LEGO examples](Category:LEGO examples "wikilink")
