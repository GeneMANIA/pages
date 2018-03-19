---
title: Help
author: admin
layout: page
---

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**

- [GeneMANIA search tips](#genemania-search-tips)
- [GeneMANIA network categories](#genemania-network-categories)
- [Uploading your own network](#uploading-your-own-network)
- [Choosing an appropriate network weighting option](#choosing-an-appropriate-network-weighting-option)
- [Network data sources](#network-data-sources)
- [Functional Enrichment Analysis](#functional-enrichment-analysis)
- [Computer requirements](#computer-requirements)
- [Linking to GeneMANIA](#linking-to-genemania)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


## GeneMANIA search tips

  * GeneMANIA works best if most of the input genes are functionally related. If they are not, a disconnected network will result and the network weighting will not be optimal. It does not matter which function they are related by, as long as that function is captured somehow by some functional association networks in the GeneMANIA system.
  * If your query list consists of 6 or more genes, GeneMANIA will calculate gene list-specific weights. If your query list has less than 6 genes, GeneMANIA will make gene function predictions based on GO annotations patterns.
  * GeneMANIA will be slower with an input gene list of more than 50 genes; if you have such large gene lists, we recommend using a gene list of no more than 100 genes. The GeneMANIA [Cytoscape app](/cytoscape-app) is capable of handling larger gene lists.

## GeneMANIA network categories

GeneMANIA searches many large, publicly available biological datasets to find related genes. These include protein-protein, protein-DNA and genetic interactions, pathways, reactions, gene and protein expression data, protein domains and phenotypic screening profiles. Data is regularly updated.

Networks names describe the data source and are either generated from the PubMed entry associated with the data source (first author-last author-year), or simply the name of the data source (BioGRID, PathwayCommons-(original data source), Pfam)

  * **Co-expression:** Gene expression data. Two genes are linked if their expression levels are similar across conditions in a gene expression study. Most of these data are collected from the Gene Expression Omnibus (GEO); we only collect data associated with a publication.
  * **Physical Interaction:** Protein-protein interaction data. Two gene products are linked if they were found to interact in a protein-protein interaction study. These data are collected from primary studies found in protein interaction databases, including BioGRID and PathwayCommons.
  * **Genetic interaction:** Genetic interaction data. Two genes are functionally associated if the effects of perturbing one gene were found to be modified by perturbations to a second gene. These data are collected from primary studies and BioGRID.
  * **Shared protein domains:** Protein domain data. Two gene products are linked if they have the same protein domain. These data are collected from domain databases, such as InterPro, SMART and Pfam.
  * **Co-localization:** Genes expressed in the same tissue, or proteins found in the same location. Two genes are linked if they are both expressed in the same tissue or if their gene products are both identified in the same cellular location.
  * **Pathway:** Pathway data. Two gene products are linked if they participate in the same reaction within a pathway. These data are collected from various source databases, such as Reactome and BioCyc, via PathwayCommons.
  * **Predicted:** Predicted functional relationships between genes, often protein interactions. A major source of predicted data is mapping known functional relationships from another organism via orthology. For instance, two proteins are predicted to interact if their orthologs are known to interact in another organism. In these cases, network names describe the original data source of experimentally measured interactions and which organism the interactions were mapped from. E.g. A mouse network predicted from a human network: Barrios-Rodiles-Wrana-2005-Human2Mouse. Also, we include predicted functional associations from other groups that combine multiple data sources for a given organism, e.g., the entire YeastNet predicted network: Lee-Marcotte-2007 YeastNet; the genetic interaction data used to generate YeastNet: Lee-Marcotte-2007 Genetic interactions. In these cases, the network name indicates the original publication detailing the predicted network, and (in some cases) lists the individual network that was used to generate the entire predicted network (for latter example above). Some predicted networks include data from other organisms. In these cases, the original organism is mentioned in the network name, e.g., the yeast protein interaction data used to generate WormNet: Lee-Marcotte-2008 Protein interactions yeast2worm.
  * **Other:** Networks that do not fit into any of the above categories. Examples include phenotype correlations from Ensembl, disease information from OMIM and chemical genomics data.
  * **Uploaded:** Networks that have you have uploaded.

## Uploading your own network

You can upload your network to GeneMANIA and analyze it in the context of all publicly available networks that GeneMANIA knows about. Your network is deleted from the GeneMANIA server after your session ends, or within 24 hours. Please see our [privacy policy](/privacy/ "Privacy") for more information.

The upload network button can be found in the advanced options panel. Your network must be for one of the GeneMANIA supported organisms, be tab delimited text, and in the format <tt>GeneID <tab> GeneID <tab> Score</tt>. The score will vary depending on the type of network, but in general is a number ranging from zero (no interaction) to 1 (strong interaction). For an interaction network or a pathway where interactions either exist or don&#8217;t exist, the score is 1 for all links. For a gene expression network, the score could be the Pearson correlation coefficient for the gene pair, representing the expression level simiarity across several experiments.

For a co-expression network, the score could be the Pearson correlation coefficient between the expression profiles of the two genes. Note that networks are normalized to reduce the effect of highly connected nodes, so scores may change slightly once uploaded.

## Choosing an appropriate network weighting option

GeneMANIA can use a few different methods to weight networks when combining all networks to form the final composite network that results from a search. The default settings are usually appropriate, but you can choose a weighting method in the advanced option panel.

### Query-dependent weighting

  * **Automatically selected weighting method (default):** the network weights are chosen based on the size of your input gene list. If your input gene list has less than 5 genes, the default network weighting method is &#8216;Gene-Ontology (GO) based weighting, Biological Process based&#8217;. This weighting method assumes the input gene list is related in terms of biological processes (as defined by GO). If your input gene list has 5 or more genes, GeneMANIA assigns weights based to maximize connectivity between all input genes using the &#8216;assigned based on query gene&#8217; strategy.
  * **Assigned based on query gene:** the weights are chosen automatically using linear regression, to make genes on your list interact as much as possible with each other, and as little as possible with genes not on your list. This is the default method if your input gene list contains more than 5 genes.

### Gene Ontology (GO)-based weighting

These weighting methods are based on GO terms that have between 3 and 300 genes associated with them. Only the most reliable annotations were used (i.e. all annotations with an IEA evidence code were removed, as these are less reliable). There is one weighting method per GO branch.

  * **Biological Process based:** assumes the input gene list is related through GO biological processes. This is the default method if your input gene list contains less than 5 genes.
  * **Molecular Function based:** assumes the input gene list is related through the GO molecular functions.
  * **Cellular Component based:** assumes the input gene list is related through the GO cellular components.

### Equal weighting

  * **Equal by network:** all networks are assigned an equal weight. This is useful if you want to see all networks that connect your input genes.
  * **Equal by data type:** all network categories are assigned an equal weight, with the weighting also evenly distributed among networks within each category.

## Network data sources

Each network data source is represented as a weighted interaction network where each pair of genes is assigned an association weight, which is either zero indicating no interaction, or a positive value that reflects the strength of interaction or the reliability the observation that they interact. For example, the association of a pair of genes in a gene expression dataset is the **Pearson correlation** coefficient of their expression levels across multiple conditions in an experiment. The more the genes are co-expressed, the higher the weight they are linked by, ranging up to 1.0, meaning perfectly correlated expression.

**Direct interactions** are used for networks where binary information is available (like protein interactions). When two proteins interact, their network link has a weight of 1.

**Shared neighbours** were used for networks where the profile of one gene was compared to that of a second gene and the Pearson correlation coefficient was calculated (like protein domain data).

The GeneMANIA database consists of genomics and proteomics data from a variety of sources, including data from gene and protein expression profiling studies and primary and curated molecular interaction networks and pathways. GeneMANIA relies on the following data sources:

- [GEO](http://www.ncbi.nlm.nih.gov/geo)
- [BioGRID](http://www.ncbi.nlm.nih.gov/geo)
- [EMBL-EBI](http://www.ebi.ac.uk/interpro)
- [Pfam](http://pfam.sanger.ac.uk/)
- [Ensembl](http://www.ensembl.org/)
- [NCBI](http://www.ncbi.nlm.nih.gov/)
- [MGI](http://www.informatics.jax.org/)
- [I2D](http://www.informatics.jax.org/)
- [InParanoid](http://inparanoid.sbc.su.se/)
- [Pathway Commons](http://www.pathwaycommons.org/)

We maintain a [complete list of networks currently in the GeneMANIA system](/networks/ "List of networks used in GeneMANIA").

## Functional Enrichment Analysis

The Functions tab of the GeneMANIA results page displays Gene Ontology (GO) terms enriched among the genes in the network displayed by GeneMANIA.

We only consider annotations (direct or up-propagated) in GO terms with between 10 and 300 non-&#8220;IEA&#8221; and non-&#8220;RCA&#8221; annotations in the organism of interest. The GO categories and Q-values from a FDR corrected hypergeometric test for enrichment are reported, along with coverage ratios for the number of annotated genes in the displayed network vs the number of genes with that annotation in the genome. We estimate Q-values using the Benjamini-Hochberg procedure. Categories are displayed up to a Q-value cutoff of 0.1

We test for enrichment using as the foreground set all the genes in either the query list or the related genes discovered by GeneMANIA that have at least one GO annotation and as the background set all genes with GO annotations and at least one interaction in our network database.

Since the functional enrichment is computed on the displayed network, the value selected for number of related genes in the GeneMANIA advanced option&#8217;s panel will influence the results. It may be informative to try other values for this parameter, particularly if the set of functional categories is empty or small for the default value. If you only want to test the query list for enrichment, select &#8220;0&#8221; for the number of returned genes.

## Computer requirements

<strong>Web browser:</strong> GeneMANIA supports the latest versions of Chrome, Firefox, Safari and Edge. For a faster, smoother experience with GeneMANIA, we recommend you use a standards compliant browser, such as <a href="http://google.com/chrome">Chrome</a> or <a href="http://firefox.com">Firefox</a>.

**Internet Connection:** A fast internet connection such as DSL, Cable or T1.

**Computer:** A modern computer with at least a 1GHz CPU, 1GB RAM and a modern video card.

## Linking to GeneMANIA

The linking URL in its simplest form is `http://genemania.org/link?o=<tid>&g=<genes>`, or alternatively

`http://genemania.org/search/<organism>/<genes>`, where:

  * `<organism>` : organism name or common name (e.g. `human` or `homo_sapiens`) without punctuation (e.g. `bakers_yeast` not `baker's_yeast`)
  * `<tid>` : NCBI taxonomy id for organism (A. thaliana=3702, C. elegans=6239, D. melanogaster=7227, H. sapiens=9606, M. musculus=10090, S. cerevisiae=4932)
  * `<genes>` : one or more gene symbols separated by pipes (&#8220;|&#8221;)

**Examples of the simplest form:**

  * one gene : `http://genemania.org/link?o=3702&g=rad50`
  * multiple genes : `http://genemania.org/link?o=3702&g=PHYB|ELF3|COP1|SPA1|FUS9`

**Optional Parameters:**

GeneMANIA linking supports some optional parameters (reference GeneMANIA help section on meaning of the various weighting methods):

  * `m` : network combining method; must be one of the following:
      * `automatic_relevance` : Assigned based on query genes
      * `automatic` : Automatically selected weighting method
      * `bp` : biological process based
      * `mf` : molecular function based
      * `cc` : cellular component based
      * `average` : Equal by data type
      * `average_category` : Equal by network
  * `r` : the number of results generated by GeneMANIA; must be a number in the range 1..100.

If no optional parameters are provided, GeneMANIA assumes the default values:`m=automatic`; `r=10`.

**Examples using optional parameters:**

The following query runs the GeneMANIA algorithm for A. thaliana using 6 genes as input, the &#8220;average&#8221; method and returns 50 more genes:

`http://genemania.org/link?o=3702&g=DET1|HY5|CIP1|CIP8|PHYA|HFR1&m=average&r=50`

The following query runs the GeneMANIA algorithm for A. thaliana&#8217;s CIP1 gene using the &#8220;molecular process based&#8221; method and returns 101 genes:

`http://genemania.org/link?o=3702&g=CIP1&m=bp&r=100`

**Invalid queries:**

  * `http://genemania.org/link?o=3702` : at least one gene must be specified
  * `http://genemania.org/link?o=1000` : invalid taxonomy id
  * `http://genemania.org/link?o=3702&g=PHYA&m=super_smart&R=50` : invalid method
  * `http://genemania.org/link?o=3702&g=det1&r=1000` : results must be less than 100

Happy linking!
