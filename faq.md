---
title: FAQ
layout: page
---

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**

- [What is GeneMANIA?](#what-is-genemania)
- [What biological questions can GeneMANIA answer?](#what-biological-questions-can-genemania-answer)
- [How do I interpret GeneMANIA&#8217;s results?](#how-do-i-interpret-genemania8217s-results)
- [What makes GeneMANIA unique?](#what-makes-genemania-unique)
- [How does the GeneMANIA algorithm work?](#how-does-the-genemania-algorithm-work)
- [How do I interpret the network weights?](#how-do-i-interpret-the-network-weights)
- [What gene identifiers does GeneMANIA recognize?](#what-gene-identifiers-does-genemania-recognize)
- [How are networks computed?](#how-are-networks-computed)
- [Where can I download GeneMANIA data?](#where-can-i-download-genemania-data)
- [How do I cite GeneMANIA?](#how-do-i-cite-genemania)
- [How do I link to GeneMANIA?](#how-do-i-link-to-genemania)
- [What happened to the old, blue version of GeneMANIA?](#what-happened-to-the-old-blue-version-of-genemania)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


## What is GeneMANIA?

GeneMANIA finds other genes that are related to a set of input genes, using a very large set of functional association data. Association data include protein and genetic interactions, pathways, co-expression, co-localization and protein domain similarity. You can use GeneMANIA to find new members of a pathway or complex, find additional genes you may have missed in your screen or find new genes with a specific function, such as protein kinases. Your question is defined by the set of genes you input.

## What biological questions can GeneMANIA answer?

**Find more genes like these**

  * If members of your gene list make up a protein complex, GeneMANIA will return more potential members of the protein complex.
  * If your gene list consists of kinases, GeneMANIA will return more kinase genes.
  * If members of your gene list are involved in a specific disease, GeneMANIA will return more genes putatively involved in the same disease.
  * You want to perform a genetic screen with a phenotypic readout, for example. Enter the genes that you already know are likely to come out of your screen, for instance, genes known to underlie a specific phenotype. GeneMANIA will predict other genes underlying the phenotype, which can then be screened.

**Tell me about my gene(s)**

  * If you enter a single gene, GeneMANIA will find interactions in which your gene participates, within the selected datasets.
  * If you enter a gene list, GeneMANIA will return connections between your genes, within the selected datasets.
  * If you enter a gene list, GeneMANIA will show you in which datasets your gene list is highly connected.
  * If you enter genes from a protein interaction screen, like a pull down or yeast two-hybrid, and select only physical interaction networks, GeneMANIA will predict true positives (those more highly connected) and false positives (those less well connected).

## How do I interpret GeneMANIA&#8217;s results?

GeneMANIA returns:

  * A list of genes with associated scores, including your input genes and predicted related genes.
  * A network that shows the relationships between genes in the list. This is a composite of all of the networks chosen from the database in a way that best connects related genes. Nodes represent genes and links represent networks. Genes can be linked by more than one type of network.
  * A list of networks weighted by their ability to connect related genes. This weighting is a measure of how &#8216;informative&#8217; the network for the given set of input genes.

Predicted related genes can be, for instance, in the same pathway or complex as your input genes, can be co-expressed or have similar enzymatic function. To determine how predicted genes are related to your input genes, you need to study the links in the network to find out how your input genes are connected to each other and how new genes are related to your input genes.

## What makes GeneMANIA unique?

Other gene function prediction programs are available, including [STRING](http://string.embl.de/), [bioPIXIE](http://pixie.princeton.edu/pixie/),[Funcassociate](http://llama.med.harvard.edu/funcassociate/), and [FunCoup](http://funcoup.sbc.su.se/).

GeneMANIA has the advantage of flexibility, accuracy, and often speed of response over these other systems. In particular, in a competition (on yeast (Mostafavi et al., 2008 [PDF](http://genemania.org/pdf/Mostafavi.pdf), [PubMed](http://www.ncbi.nlm.nih.gov/pubmed/18613948), [journal](http://genomebiology.com/2008/9/S1/S4)) and mouse (Pena-Castillo et al., 2008 [PDF](http://genemania.org/pdf/Pena_Castillo.pdf), [PubMed](http://www.ncbi.nlm.nih.gov/pubmed/18613946), [journal](http://genomebiology.com/2008/9/S1/S2)), GeneMANIA was shown to be more accurate than other gene function prediction methods, and is generally faster, producing predictions within seconds. Because of this speed, GeneMANIA can produce results while you wait. Users can select arbitrary subsets of networks that they want to query and GeneMANIA automatically selects network weights based on the input gene list, generating a network specific to the user&#8217;s gene list. Unlike other systems, GeneMANIA provides users with the ability to upload their own network and also compensates for redundancies in the data, so users don&#8217;t have to worry about double-counting interactions.

## How does the GeneMANIA algorithm work?

GeneMANIA stands for Multiple Association Network Integration Algorithm.

The GeneMANIA algorithm consists of two parts:

  1. A linear regression-based algorithm that calculates a single composite functional association network from multiple data sources.
  2. A label propagation algorithm for predicting gene function given the composite functional association network.

GeneMANIA treats gene function prediction as a binary classification problem. As such, each functional association network derived from the data sources is assigned a positive weight, reflecting the data sources&#8217; usefulness in predicting the function. The weighted average of the association networks is constructed into a function-specific association network. GeneMANIA uses separate objective functions to fit the weights; this simplifies the optimization problem and decreases the run time.

GeneMANIA predicts gene function from the composite network using a variation of the Gaussian field label propagation algorithm that is appropriate for gene function prediction in which there are typically relatively few positive examples. Label propagation algorithms assign a score (the discriminant value) to each node in the network. This score reflects the computed strength of association that the node has to the seed list defining the given function. This value can be thresholded to enable predictions of a given gene function.

**GeneMANIA: a real-time multiple association network integration algorithm for predicting gene function**

Mostafavi S, Ray D, Warde-Farley D, Grouios C, Morris Q (2008)

[Genome Biology 9: S4.

](http://genomebiology.com/2008/9/S1/S4) [PubMed Abstract](http://www.ncbi.nlm.nih.gov/pubmed/18613948) ([PDF](http://genemania.org/pdf/Mostafavi.pdf))

## How do I interpret the network weights?

Coming soon.

## What gene identifiers does GeneMANIA recognize?

GeneMANIA recognizes Entrez, Ensembl, Standard gene symbols, Uniprot/SwissProt and RefSeq identifiers and unique gene names.

## How are networks computed?

The process used to create interaction networks from source data for GeneMANIA is described on the [data processing](/network-data-processing/ "Network data processing") page. This same process is used both to produce the core networks included with GeneMANIA, as well as for networks created from user-uploaded data at the GeneMANIA Website or using the Cytoscape Plugin.

## Where can I download GeneMANIA data?

The interaction networks used in the current GeneMANIA website, as well as archived datasets from previous releases are [available for download](http://genemania.org/data/) as plain text files. The [data archive](/data/ "GeneMANIA data archive") page describes the file formats used.

## How do I cite GeneMANIA?

We recommend citing the NAR webserver issue, as follows.

**The GeneMANIA prediction server: biological network integration for gene prioritization and predicting gene function**

Warde-Farley D, Donaldson SL, Comes O, Zuberi K, Badrawi R, Chao P, Franz M, Grouios C, Kazi F, Lopes CT, Maitland A, Mostafavi S, Montojo J, Shao Q, Wright G, Bader GD, Morris Q

[Nucleic Acids Res. 2010 Jul 1;38 Suppl:W214-20](http://nar.oxfordjournals.org/cgi/content/abstract/38/suppl_2/W214) [PubMed Abstract](http://www.ncbi.nlm.nih.gov/pubmed/20576703) ([PDF](http://genemania.org/pdf/genemania_prediction_server.pdf))

## How do I link to GeneMANIA?

See the [instructions](/help/#linking-to-genemania "Linking to GeneMANIA").

## What happened to the old, blue version of GeneMANIA?

That version has been superseded by an improved interface that does not use Flash. The old version is available at [old.genemania.org](http://old.genemania.org).
