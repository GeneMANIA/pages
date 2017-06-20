---
id: 103
title: Cytoscape plugin tools
date: 2011-06-08T16:15:22+00:00
author: max
layout: page
guid: http://pages.genemania.org/?page_id=103
---
# Command line tools reference documentation

## Installation

First, you need to download the [GeneMANIA JAR file](http://www.genemania.org/plugin/release/genemania-cytoscape-plugin-3.3.1.jar). If you already installed the plugin through Cytoscape, you can find it in one of the following places:

  * **Unix/Mac**: `~/.cytoscape/<em>Cytoscape Version</em>/plugins/GeneMANIA-<em>Version</em>/`
  * **Windows**: `My Documents\.cytoscape\<em>Cytoscape Version</em>\plugins\GeneMANIA-<em>Version</em>\`

Second, you need a data set. If you&#8217;ve used the Cytoscape plugin to perform predictions, you&#8217;ll already have one installed in one of these locations:

  * **Unix/Mac**: `~/genemania_plugin/gmdata-<em>id</em>/`
  * **Windows**: `My Documents\genemania_plugin\gmdata-<em>id</em>\`

Otherwise, you can use [Data Admin](#data=admin) to install one of the available data sets from `genemania.org`.

## Available Tools

<table class="options">
  <tr>
    <th colspan="2">
      Data Import & Management
    </th>
  </tr>
  
  <tr>
    <th>
      <a href="#data-admin">Data Admin</a>
    </th>
    
    <td>
      Downloads and manages GeneMANIA data sets from <code>genemania.org</code>.
    </td>
  </tr>
  
  <tr>
    <th>
      <a href="#gene-sanitizer">Gene Sanitizer</a>
    </th>
    
    <td>
      Prints out the mappings between the given gene list and GeneMANIA&#8217;s preferred identifiers.
    </td>
  </tr>
  
  <tr>
    <th>
      <a href="#id-importer">Id Importer</a>
    </th>
    
    <td>
      Creates a new data set from a set of identifiers and aliases. The identifiers correspond to node labels.
    </td>
  </tr>
  
  <tr>
    <th>
      <a href="#network-importer">Network Importer</a>
    </th>
    
    <td>
      Imports network/profile data from a file into a GeneMANIA data set.
    </td>
  </tr>
  
  <tr>
    <th colspan="2">
      Prediction
    </th>
  </tr>
  
  <tr>
    <th>
      <a href="#query-runner">Query Runner</a>
    </th>
    
    <td>
      Runs one or more predictions and writes the results to disk. Each prediction needs to be provided in the form of a query file. One prediction report is generated for each query file.
    </td>
  </tr>
  
  <tr>
    <th colspan="2">
      Validation
    </th>
  </tr>
  
  <tr>
    <th>
      <a href="#cross-validator">Cross Validator</a>
    </th>
    
    <td>
      Performs k-fold cross validation on the prediction algorithm for a given set of pre-classified genes. Cross Validator reports on the following evaluation measures: area under the ROC curve (AUC-ROC), area under the precision-recall curve (AUC-PR), and precision at fixed recall.
    </td>
  </tr>
  
  <tr>
    <th>
      <a href="#network-assessor">Network Assessor</a>
    </th>
    
    <td>
      Assesses the value of a set of networks by performing k-fold cross validation against a baseline network set, as well as the networks to assess. The percentage error of each validation measure is computed for each query in the validation set and reported.
    </td>
  </tr>
  
  <tr>
    <th>
      <a href="#validation-set-maker">Validation Set Maker</a>
    </th>
    
    <td>
      Produces sets of genes based on Gene Ontology (GO) annotations for use in cross validation. One gene set is created for each GO category in the ontology. More specific annotations are propagated up to all genes associated with any of the parent annotations.
    </td>
  </tr>
</table>

<a name="data-admin"></a>

## Data Admin

<div class="section">
  <p>
    Downloads and manages GeneMANIA data sets from <code>genemania.org</code>. Each data set consists of multiple organisms which are identified by their <code>data-id</code>. Organisms can be installed and removed individually as needed.
  </p>
  
  <h3>
    Commands:
  </h3>
  
  <ul>
    <li>
      <strong><code>list</code></strong>: Lists available data sets.<br /> <h4>
        Usage:
      </h4>
      
      <pre>list</pre>
      
      <h4>
        Example:
      </h4>
      
      <pre style="overflow: auto;">$ java -jar GeneMania.jar DataAdmin <strong>list</strong>
<span style="color: #202080;">Data Set ID	Total Size	Database Version
2013-10-15	9351.08 MB	15 October 2013
2013-10-15-core	2059.38 MB	15 October 2013
2013-10-15-open_license	9324.49 MB	15 October 2013
2012-08-02	5994.14 MB	19 July 2012
2012-08-02-core	1764.09 MB	19 July 2012
2012-08-02-open_license	5963.38 MB	19 July 2012
...</span></pre>
    </li>
    
    <li>
      <strong><code>install</code></strong>: Installs the infrastructure for the given data set ID without actually installing any organism data.<br /> <h4>
        Usage:
      </h4>
      
      <pre>install <em>data-set-id</em></pre>
      
      <p>
        &#8230;where <code>data-set-id</code> is one of the IDs given by the <code>list</code> command above.
      </p>
      
      <h4>
        Example:
      </h4>
      
      <pre style="overflow: auto;">$ java -jar GeneMania.jar DataAdmin <strong>install 2013-10-15-core</strong></pre>
      
      <p>
        This example will download the data set into the directory <code>gmdata-2013-10-15-core</code> in the current directory.</li> 
        
        <li>
          <strong><code>list-data</code></strong>: Lists the data available for download for a particular data set.<br /> <h4>
            Usage:
          </h4>
          
          <pre>list <em>path/to/data/set</em></pre>
          
          <p>
            &#8230;where <code>path/to/data/set</code> is the path to a data set downloaded by the Cytoscape plugin, or the <code>install</code> command above.
          </p>
          
          <h4>
            Example:
          </h4>
          
          <pre style="overflow: auto;">$ java -jar GeneMania.jar DataAdmin <strong>list-data gmdata-2013-10-15-core</strong>
<span style="color: #202080;">Data ID	Description	Status
1	A. thaliana Arabidopsis (424 MB)	
2	C. elegans Worm (141 MB)	
3	D. melanogaster Fly (237 MB)	
4	H. sapiens Human (413 MB)	
5	M. musculus Mouse (412 MB)	
6	S. cerevisiae Baker's yeast (148 MB)	
7	R. norvegicus Rat (154 MB)	
8	D. rerio Zebrafish (126 MB)	
</span></pre>
        </li>
        
        <li>
          <strong><code>install-data</code></strong>: Downloads and installs data with the given ID from <code>genemania.org</code>.<br /> <h4>
            Usage:
          </h4>
          
          <pre>install-data <em>path/to/data/set</em> <em>data-id [data-id ...]</em></pre>
          
          <p>
            &#8230;where <code>path/to/data/set</code> is the path to a data set downloaded by the Cytoscape plugin, or the <code>install</code> command above; and <em>data-id</em> is one of the IDs given by the <code>list-data</code> command, or <code>all</code>, which is an alias for all available data for the given data set.
          </p>
          
          <h4>
            Example: Installing yeast data
          </h4>
          
          <pre style="overflow: auto;">$ java -jar GeneMania.jar DataAdmin <strong>install-data gmdata-2013-10-15-core 6</strong></pre>
        </li>
        
        <h4>
          Example: Installing all data for 2013-10-15-core
        </h4>
        
        <pre style="overflow: auto;">$ java -jar GeneMania.jar DataAdmin <strong>install-data gmdata-2013-10-15-core all</strong></pre></ul> 
        
        <ul>
          <li>
            <strong><code>uninstall-data</code></strong>: Deletes previously installed data from a data set.<br /> <h4>
              Usage:
            </h4>
            
            <pre>uninstall-data <em>path/to/data/set</em> <em>data-id [data-id ...]</em></pre>
            
            <p>
              &#8230;where <code>path/to/data/set</code> is the path to a data set downloaded by the Cytoscape plugin, or the <code>install</code> command above; and <em>data-id</em> is one of the IDs given by the <code>list-data</code> command.
            </p>
            
            <h4>
              Example: Uninstalling human data
            </h4>
            
            <pre style="overflow: auto;">$ java -jar GeneMania.jar DataAdmin <strong>uninstall-data gmdata-2013-10-15-core 4</strong></pre>
          </li>
        </ul></div> 
        
        <p>
          <a name="gene-sanitizer"></a>
        </p>
        
        <h2>
          Gene Sanitizer
        </h2>
        
        <div class="section">
          <p>
            Prints out the mappings between the given gene list and GeneMANIA&#8217;s preferred identifiers. This tool is useful for checking which of your genes are recognized by GeneMANIA. The output is a tab-delimited text file containing one mapping per line. The first item is GeneMANIA&#8217;s preferred identifier, or nothing, if the identifier that follows isn&#8217;t recognized.
          </p>
          
          <h3>
            Usage:
          </h3>
          
          <pre style="overflow: auto;">java -Xmx900M -jar GeneMANIA.jar GeneSanitizer <em>options gene-list-file</em></pre>
          
          <h3>
            Example Gene List:
          </h3>
          
          <pre style="overflow: auto;">YMR043W
YPR113W
YCL067C
YIL015W
YNOT?
YCR084C
YFL026W
YHR084W
YGL008C
YNL145W</pre>
          
          <h3>
            Example Output:
          </h3>
          
          <pre style="overflow: auto;">YMR043W	MCM1
YPR113W	PIS1
YCL067C	HMLALPHA2
YIL015W	BAR1
YNOT?	
YCR084C	TUP1
YFL026W	STE2
YHR084W	STE12
YGL008C	PMA1
YNL145W	MFA2</pre>
          
          <h3>
            Options:
          </h3>
          
          <table class="options">
            <tr>
              <th>
                Name
              </th>
              
              <th>
                Description
              </th>
            </tr>
            
            <tr>
              <th style="white-space: nowrap; font-family: monospace;">
                &#8211;data <em class="parameter">directory</em>
              </th>
              
              <td>
                Path to a GeneMANIA data set (e.g. <code>/Users/username/genemania_plugin/gmdata-2013-10-15</code>).
              </td>
            </tr>
            
            <tr>
              <th style="white-space: nowrap; font-family: monospace;">
                &#8211;organism <em class="parameter">name</em>
              </th>
              
              <td>
                The name or taxonomy id of an <a href="#available-organisms">organism</a> whose genes should be considered.
              </td>
            </tr>
          </table>
        </div>
        
        <p>
          <a name="id-importer"></a>
        </p>
        
        <h2>
          Id Importer
        </h2>
        
        <div class="section">
          <p>
            Creates a new data set from a set of identifiers and aliases. The identifiers correspond to node labels. Although the resulting data set is generally treated like an organism, where the given ids denote its genome, it does not have to be an organism. The identifiers can be anything, as long as they&#8217;re unique within the data set.
          </p>
          
          <h3>
            Usage:
          </h3>
          
          <pre style="overflow: auto;">java -Xmx900M -jar GeneMANIA.jar IdImporter <em>options</em></pre>
          
          <h3>
            Options:
          </h3>
          
          <table class="options">
            <tr>
              <th>
                Name
              </th>
              
              <th>
                Description
              </th>
            </tr>
            
            <tr>
              <th style="white-space: nowrap; font-family: monospace;">
                &#8211;data <em class="parameter">directory</em>
              </th>
              
              <td>
                Path to a GeneMANIA data set (e.g. <code>/Users/username/genemania_plugin/gmdata-2013-10-15</code>).
              </td>
            </tr>
            
            <tr>
              <th style="white-space: nowrap; font-family: monospace;">
                &#8211;filename <em class="parameter">file-name</em>
              </th>
              
              <td>
                The path to a file that contains a complete set of identifiers that will serve as the basis of a new data set. Each line in the file should follow this format:</p> 
                
                <pre style="overflow: auto;"><em>primary-id</em> ( \t alias-1 ... )</pre>
              </td>
            </tr>
            
            <tr>
              <th style="white-space: nowrap; font-family: monospace;">
                &#8211;name <em class="parameter">entity-name</em>
              </th>
              
              <td>
                The name of the resulting entity (e.g. organism).
              </td>
            </tr>
            
            <tr>
              <th style="white-space: nowrap; font-family: monospace;">
                &#8211;alias <em class="parameter">entity-name</em>
              </th>
              
              <td>
                Optional. An alias for the resulting entity (e.g. shorter, informal name)
              </td>
            </tr>
            
            <tr>
              <th style="white-space: nowrap; font-family: monospace;">
                &#8211;taxid <em class="parameter">number</em>
              </th>
              
              <td>
                Optional. The taxonomy id of the resulting entity, if applicable.
              </td>
            </tr>
            
            <tr>
              <th style="white-space: nowrap; font-family: monospace;">
                &#8211;description <em class="parameter">description</em>
              </th>
              
              <td>
                Optional. A description of the resulting entity.
              </td>
            </tr>
          </table>
        </div>
        
        <p>
          <a name="network-importer"></a>
        </p>
        
        <h2>
          Network Importer
        </h2>
        
        <div class="section">
          <p>
            Imports network/profile data from a file into a GeneMANIA data set.
          </p>
          
          <h3>
            Usage (32-bit JVM):
          </h3>
          
          <pre style="overflow: auto;">java -Xmx1800M -jar GeneMANIA.jar NetworkImporter <em>options</em></pre>
          
          <h3>
            Usage (64-bit JVM):
          </h3>
          
          <pre style="overflow: auto;">java -d64 -Xmx3G -jar GeneMANIA.jar NetworkImporter <em>options</em></pre>
          
          <h3>
            Options:
          </h3>
          
          <table class="options">
            <tr>
              <th>
                Name
              </th>
              
              <th>
                Description
              </th>
            </tr>
            
            <tr>
              <th style="white-space: nowrap; font-family: monospace;">
                &#8211;data <em class="parameter">directory</em>
              </th>
              
              <td>
                Path to a GeneMANIA data set (e.g. <code>/Users/username/genemania_plugin/gmdata-2013-10-15</code>).
              </td>
            </tr>
            
            <tr>
              <th style="white-space: nowrap; font-family: monospace;">
                &#8211;organism <em class="parameter">name</em>
              </th>
              
              <td>
                The name or taxonomy id of an <a href="#available-organisms">organism</a> whose genes should be considered.
              </td>
            </tr>
            
            <tr>
              <th style="white-space: nowrap; font-family: monospace;">
                &#8211;filename <em class="parameter">path</em>
              </th>
              
              <td>
                Path to a file containing either interaction or profile data. Supported types of data include:</p> 
                
                <ul>
                  <li>
                    unweighted networks <pre style="overflow: auto;">GENE1 \t GENE2</pre>
                  </li>
                  
                  <li>
                    weighted networks <pre style="overflow: auto;">GENE1 \t GENE2 \t SCORE</pre>
                  </li>
                  
                  <li>
                    expression profiles <pre style="overflow: auto;">GENE \t EXPR1 ( \t EXPR2 ... )</pre>
                  </li>
                  
                  <li>
                    SOFT-formatted expression profiles (e.g. from <a href="http://www.ncbi.nlm.nih.gov/geo/">GEO</a>)
                  </li>
                </ul>
              </td>
            </tr>
            
            <tr>
              <th style="white-space: nowrap; font-family: monospace;">
                &#8211;name <em class="parameter">network-name</em>
              </th>
              
              <td>
                The name of the new network.
              </td>
            </tr>
            
            <tr>
              <th style="white-space: nowrap; font-family: monospace;">
                &#8211;description <em class="parameter">description</em>
              </th>
              
              <td>
                Optional. A description of the new network.
              </td>
            </tr>
            
            <tr>
              <th style="white-space: nowrap; font-family: monospace;">
                &#8211;group <em class="parameter">network-type</em>
              </th>
              
              <td>
                Optional. The <a href="#available-networks">network group</a> to which the new network will be added. If this group does not exist, it will be created. Defaults to <code>other</code>.
              </td>
            </tr>
            
            <tr>
              <th style="white-space: nowrap; font-family: monospace;">
                &#8211;group-description <em class="parameter">description</em>
              </th>
              
              <td>
                Optional. A short description for a network group being created. Only applicable when the group specified by <code>--group</code> does not already exist.
              </td>
            </tr>
            
            <tr>
              <th style="white-space: nowrap; font-family: monospace;">
                &#8211;color <em class="parameter">RRGGBB</em>
              </th>
              
              <td>
                Optional. The colour of the network group being created. Only applicable when the group specified by <code>--group</code> does not already exist. Defaults to <code>000000</code> (i.e. black).
              </td>
            </tr>
            
            <tr>
              <th style="white-space: nowrap; font-family: monospace;">
                &#8211;verbose
              </th>
              
              <td>
                Optional. Makes NetworkImporter print more details about what&#8217;s happening.
              </td>
            </tr>
          </table>
        </div>
        
        <p>
          <a name="query-runner"></a>
        </p>
        
        <h2>
          Query Runner
        </h2>
        
        <div class="section">
          <div>
            Runs one or more predictions and writes the results to disk. Each prediction needs to be provided in the form of a query file. One prediction report is generated for each query file.
          </div>
          
          <h3>
            Usage (32-bit JVM):
          </h3>
          
          <pre style="overflow: auto;">java -Xmx1800M -jar GeneMANIA.jar QueryRunner <em>options query-file-1 [ query-file-2 ... ]</em></pre>
          
          <h3>
            Usage (64-bit JVM):
          </h3>
          
          <pre style="overflow: auto;">java -d64 -Xmx3G -jar GeneMANIA.jar QueryRunner <em>options query-file-1 [ query-file-2 ... ]</em></pre>
          
          <h3>
            Options:
          </h3>
          
          <table class="options">
            <tr>
              <th>
                Name
              </th>
              
              <th>
                Description
              </th>
            </tr>
            
            <tr>
              <th style="white-space: nowrap; font-family: monospace;">
                &#8211;data <em class="parameter">directory</em>
              </th>
              
              <td>
                Path to a GeneMANIA data set (e.g. <code>/Users/username/genemania_plugin/gmdata-2013-10-15</code>).
              </td>
            </tr>
            
            <tr>
              <th style="white-space: nowrap; font-family: monospace;">
                &#8211;in <em class="parameter">input-format</em>
              </th>
              
              <td>
                Optional. The format of the query files, which can be one of:</p> 
                
                <ul>
                  <li>
                    <code>flat</code> (default): Tab-delimited (<a href="#flat-example">example</a>).
                  </li>
                  <li>
                    <code>xml</code>: Not yet supported.
                  </li>
                </ul>
              </td>
            </tr>
            
            <tr>
              <th style="white-space: nowrap; font-family: monospace;">
                &#8211;out <em class="parameter">output-format</em>
              </th>
              
              <td>
                Optional. The format of the output files, which can be one of:</p> 
                
                <ul>
                  <li>
                    <code>genes</code> (default): List of result genes ordered by score; one per line.
                  </li>
                  <li>
                    <code>flat</code>: Tab-delimited report containing details of prediction results and query parameters.
                  </li>
                  <li>
                    <code>xml</code>: XML-formatted report containing details of prediction results and query parameters.
                  </li>
                  <li>
                    <code>scores</code>: List of result genes with scores ordered by score for the entire genome (ignores related genes limit); one per line.
                  </li>
                </ul>
              </td>
            </tr>
            
            <tr>
              <th style="white-space: nowrap; font-family: monospace;">
                &#8211;scoring-method <em class="parameter">method</em>
              </th>
              
              <td>
                Optional. The method used to compute the gene scores, which can be one of:</p> 
                
                <ul>
                  <li>
                    <code>discriminant</code> (default): GeneMANIA&#8217;s classic scoring method.
                  </li>
                  <li>
                    <code>z</code>: Z-scores.
                  </li>
                </ul>
              </td>
            </tr>
            
            <tr>
              <th style="white-space: nowrap; font-family: monospace;">
                &#8211;ids <em class="parameter">id-types</em>
              </th>
              
              <td>
                Optional. A comma-separated list of identifier types, in descending order of preference, which may be one or more of the following:</p> 
                
                <ul>
                  <li>
                    <code>Ensembl Gene Name</code>
                  </li>
                  <li>
                    <code>Entrez Gene Name</code>
                  </li>
                  <li>
                    <code>Ensembl Gene ID</code>
                  </li>
                  <li>
                    <code>RefSeq mRNA ID</code>
                  </li>
                  <li>
                    <code>TAIR ID</code>
                  </li>
                  <li>
                    <code>Uniprot ID</code>
                  </li>
                  <li>
                    <code>Uniprot AC</code>
                  </li>
                  <li>
                    <code>RefSeq Protein ID</code>
                  </li>
                  <li>
                    <code>Ensembl Protein ID</code>
                  </li>
                  <li>
                    <code>Entrez Gene ID</code>
                  </li>
                </ul>
                
                <p>
                  If the most preferred identifier is not available for a given gene, the next most preferred identifier is selected. The list above reflects the default order of preference.</td> </tr> 
                  
                  <tr>
                    <th style="white-space: nowrap; font-family: monospace;">
                      &#8211;results <em class="parameter">directory</em>
                    </th>
                    
                    <td>
                      Optional. Path to where the prediction result files will be created (one per input query file). Defaults to the current working directory.
                    </td>
                  </tr>
                  
                  <tr>
                    <th style="white-space: nowrap; font-family: monospace;">
                      &#8211;threads <em class="parameter">number</em>
                    </th>
                    
                    <td>
                      Optional. The maximum number of parallel predictions. Ideally this should be set to the number of processing cores. Defaults to 1.
                    </td>
                  </tr>
                  
                  <tr>
                    <th style="white-space: nowrap; font-family: monospace;">
                      &#8211;verbose
                    </th>
                    
                    <td>
                      Optional. Makes QueryRunner print more details about what&#8217;s happening.
                    </td>
                  </tr>
                  
                  <tr>
                    <th style="white-space: nowrap; font-family: monospace;">
                      &#8211;list-networks <em class="parameter">organism-name</em>
                    </th>
                    
                    <td>
                      Optional. Lists the available networks for the given organism. You may need to put quotes around the organism name if invoked from a shell.
                    </td>
                  </tr>
                  
                  <tr>
                    <th style="white-space: nowrap; font-family: monospace;">
                      &#8211;list-genes <em class="parameter">organism-name</em>
                    </th>
                    
                    <td>
                      Optional. Lists the genes that are recognized for the given organism. You may need to put quotes around the organism name if invoked from a shell. Each line in the output contains a gene and all its synonyms, if any.
                    </td>
                  </tr></tbody> </table> 
                  
                  <p>
                    <a name="flat-example"></a>
                  </p>
                  
                  <h3>
                    Example Query (Flat):
                  </h3>
                  
                  <div class="filename">
                    yeast-example.query
                  </div>
                  
                  <pre style="overflow: auto;">S. Cerevisiae
CDC27	APC11	APC4	XRS2	RAD54	APC2	RAD52	RAD10	MRE11	APC5
coexp	pi	gi
150
bp</pre>
                  
                  <h3>
                    Flat Query File Format:
                  </h3>
                  
                  <pre style="overflow: auto;"><a href="#available-organisms">organism-name</a> 
query-gene-1 [ \t query-gene-2 ... ]
<a href="#available-networks">networks</a> 
related-gene-limit
[ <a href="#available-combining-methods">combining-method</a> ]</pre></div> 
                  
                  <p>
                    <a name="cross-validator"></a>
                  </p>
                  
                  <h2>
                    Cross Validator
                  </h2>
                  
                  <div class="section">
                    <p>
                      Performs k-fold cross validation on the prediction algorithm for a given set of pre-classified genes. Cross Validator reports on the following evaluation measures: area under the ROC curve (AUC-ROC), area under the precision-recall curve (AUC-PR), and precision at fixed recall.
                    </p>
                    
                    <h3>
                      Usage (32-bit JVM):
                    </h3>
                    
                    <pre style="overflow: auto;">java -Xmx1800M -jar GeneMANIA.jar CrossValidator <em>options</em></pre>
                    
                    <h3>
                      Usage (64-bit JVM):
                    </h3>
                    
                    <pre style="overflow: auto;">java -d64 -Xmx3G -jar GeneMANIA.jar CrossValidator <em>options</em></pre>
                    
                    <h3>
                      Options:
                    </h3>
                    
                    <table class="options">
                      <tr>
                        <th>
                          Name
                        </th>
                        
                        <th>
                          Description
                        </th>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;data <em class="parameter">directory</em>
                        </th>
                        
                        <td>
                          Path to a GeneMANIA data set (e.g. <code>/Users/username/genemania_plugin/gmdata-2013-10-15</code>).
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;organism <em class="parameter">name</em>
                        </th>
                        
                        <td>
                          The name or taxonomy id of an <a href="#available-organisms">organism</a> whose genes should be considered.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;query <em class="parameter">file-name</em>
                        </th>
                        
                        <td>
                          Perform validation against the gene sets listed in the given file. It must be formatted <a href="#validation-query-format">this way</a>.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;networks <em class="parameter">network-list</em>
                        </th>
                        
                        <td>
                          A comma-separated list of <a href="#available-networks">network types</a> and/or network names. To get a full listing of network names, use the option <code>--list-networks</code> with <a href="#query-runner">Query Runner</a>.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;exclude-networks <em class="parameter">network-list</em>
                        </th>
                        
                        <td>
                          Optional. A comma-separated list of <a href="#available-networks">network types</a> and/or network names to exclude from the <code>--networks</code> list.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;folds <em class="parameter">number</em>
                        </th>
                        
                        <td>
                          Optional. The number of folds to use during cross validation. Defaults to 5.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;min <em class="parameter">number</em>
                        </th>
                        
                        <td>
                          Optional. The minimum number of positive genes for a query. Queries with a fewer number of genes will be skipped. Defaults to 10.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;max <em class="parameter">number</em>
                        </th>
                        
                        <td>
                          Optional. The maximum number of positive genes for a query. Queries with a larger number of genes will be skipped. Defaults to 300.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;use-go-cache
                        </th>
                        
                        <td>
                          Optional. Perform validation against bundled Gene Ontology gene sets. In this case, the query file should contain one GO id per line (e.g. <code>GO:0005786</code>). These gene sets have been pre-filtered so that the smallest has 10 genes and the largest has 300.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;outfile <em class="parameter">file-name</em>
                        </th>
                        
                        <td>
                          Optional. The file where the validation results should be saved. If not provided, the results are sent to standard output (usually the console).
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;auto-negatives
                        </th>
                        
                        <td>
                          Optional. Forces all non-positive genes to be labeled as negative examples during prediction. Otherwise, negative examples must be explicitly listed in the query file.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;method <em class="parameter">weighting-method</em>
                        </th>
                        
                        <td>
                          Optional. The <a href="#available-combining-methods">weighting method</a> to use when combining the individual networks. Defaults to <code>automatic</code>.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;seed <em class="parameter">number</em>
                        </th>
                        
                        <td>
                          Optional. A value used to initialize the pseudo random number generator used for shuffling each gene set during validation. Setting the seed to a constant value will make the validation results deterministic. Defaults to something pseudo-random.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;threads <em class="parameter">number</em>
                        </th>
                        
                        <td>
                          Optional. The maximum number of parallel predictions. Ideally this should be set to the number of processing cores. Defaults to 1.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;verbose
                        </th>
                        
                        <td>
                          Optional. Makes CrossValidator print more details about what&#8217;s happening.
                        </td>
                      </tr>
                    </table>
                    
                    <p>
                      <a name="validation-query-format"></a>
                    </p>
                    
                    <h3>
                      Query File Format:
                    </h3>
                    
                    <p>
                      Multiple gene sets may be used during cross validation. Each gene set should be on its own line using the format below:
                    </p>
                    
                    <pre style="overflow: auto;">GENE_SET_ID \t + \t gene_symbol1 <em>[ \t gene_symbol2 ... ]</em> [ \t - \t neg_gene_symbol1 [ \t neg_gene_symbol2 ... ] ]</pre>
                    
                    <p>
                      &#8230;where <code>GENE_SET_ID</code> is the name of your gene set, <code>gene_symbol</code> is a positive gene example, and <code>neg_gene_symbol</code> is a negative gene example (i.e. definitely not a member of the gene set).
                    </p>
                    
                    <p>
                      If <code>--use-go-cache</code> is also specified, the query file should contain one GO id per line (e.g. <code>GO:0005786</code>).
                    </p>
                    
                    <h3>
                      Example Query File (S. Cerevisiae):
                    </h3>
                    
                    <p>
                      This query file only lists positive examples of genes. Use the option <code>--auto-negatives</code> to automatically label all other genes in each set as negative examples.
                    </p>
                    
                    <pre style="overflow: auto;">GO:0005786      +       SCR1    SRP54   SEC65   SRP14   SRP68   SRP21   SRP72
GO:0022626      +       RPS21A  RPS21B  HEF3    RPS8B   RDN18-2 RDN18-1 RPL9A   RPL9B   RPS11B  RPS11A  RPS29A  RPS29B    RPS14A  RPL1A   RPL1B   YGR054W RPS19B  RPS19A  RPS6B   RDN5-1  RDN5-2  RDN5-3  RDN5-4  RDN5-5  RDN5-6  RPL24B    RPL8B   RPL8A   RPL24A  RPS22A  RPS12   RPS22B  RPL18A  FES1    RPL10   RPS8A   RPL41A  RPL42A  ASC1    RPS18A    RPS18B  SQT1    RPL14A  RPL31A  RPL31B  RPL14B  RPS2    RPL37B  RPL16B  RPL16A  RPL37A  RPS17A  RPS17B  RPS27B    RPL27B  RPL27A  RPL5    RPL3    RPL7B   RPL7A   NMD3    RPL41B  RPL11B  RPL11A  RPP2A   TIF5    RPP2B   RPL20B    RPL20A  RPS16B  RPL17A  RPL17B  RPS16A  RPL26A  RPL26B  RPS7A   RPL6A   RPL6B   RPS28B  RPS28A  RDN25-1 TEF1      SIS1    RRP14   RPS31   REI1    RDN25-2 JJJ1    RPL42B  RPL35A  RPL35B  RPL18B  RPS5    RPS3    RPS25A  RPS25B    RPS15   RPL13A  RPL13B  RDN58-2 RDN58-1 RPS9B   RPL22A  RPL22B  RPS9A   RPL36A  RPS4A   RPS4B   RPL36B  RPS30B    RPS20   RPS30A  RPS26A  NAT1    RPS26B  RPL19B  NAT5    RPL19A  GCN1    GCN2    RPS7B   RPS6A   RPL4B   RPL4A     ARX1    RPL21A  RPL21B  RPS13   RPP1A   RPP1B   RPS23B  RPL23B  RPL23A  RPS23A  RPL40A  RPL40B  RPS14B  ARD1      MAP1    NIP7    RPS10A  RPL29   RPL28   RPL25   GCN20   RPL15B  RPL15A  RPS10B  RPS0A   RPS0B   RLI1    RPL34B    RPL34A  RPL43A  RPL43B  RPS24B  RPS24A  FUN12   RPS27A  RPL2A   RPL2B   PAT1    RPL38   RPL39   STM1    RPL32     RPP0    RPL30   RPS1B   RPS1A   RPL33B  RPL12B  RPL12A  RPL33A</pre>
                  </div>
                  
                  <p>
                    <a name="network-assessor"></a>
                  </p>
                  
                  <h2>
                    Network Assessor
                  </h2>
                  
                  <div class="section">
                    <p>
                      Assesses the value of a set of networks by performing k-fold cross validation against a baseline network set, as well as the networks to assess. The percentage error of each validation measure is computed for each query in the validation set and reported.
                    </p>
                    
                    <h3>
                      Usage (32-bit JVM):
                    </h3>
                    
                    <pre style="overflow: auto;">java -Xmx1800M -jar GeneMANIA.jar NetworkAssessor <em>options</em></pre>
                    
                    <h3>
                      Usage (64-bit JVM):
                    </h3>
                    
                    <pre style="overflow: auto;">java -d64 -Xmx3G -jar GeneMANIA.jar NetworkAssessor <em>options</em></pre>
                    
                    <h3>
                      Options:
                    </h3>
                    
                    <table class="options">
                      <tr>
                        <th>
                          Name
                        </th>
                        
                        <th>
                          Description
                        </th>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;data <em class="parameter">directory</em>
                        </th>
                        
                        <td>
                          Path to a GeneMANIA data set (e.g. <code>/Users/username/genemania_plugin/gmdata-2013-10-15</code>).
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;organism <em class="parameter">name</em>
                        </th>
                        
                        <td>
                          The name or taxonomy id of an <a href="#available-organisms">organism</a> whose genes should be considered.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;query <em class="parameter">file-name</em>
                        </th>
                        
                        <td>
                          Perform validation against the gene sets listed in the given file. It must be formatted <a href="#validation-query-format">this way</a>.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;baseline <em class="parameter">network-list</em>
                        </th>
                        
                        <td>
                          A comma-separated list of <a href="#available-networks">network types</a> and/or network names to use as a baseline for comparison. To get a full listing of network names, use the option <code>--list-networks</code> with <a href="#query-runner">Query Runner</a>.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;exclude-baseline <em class="parameter">network-list</em>
                        </th>
                        
                        <td>
                          Optional. A comma-separated list of <a href="#available-networks">network types</a> and/or network names to exclude from the <code>--baseline</code> list.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;networks <em class="parameter">network-list</em>
                        </th>
                        
                        <td>
                          A comma-separated list of <a href="#available-networks">network types</a> and/or network names representing the networks to assess. To get a full listing of network names, use the option <code>--list-networks</code> with <a href="#query-runner">Query Runner</a>.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;exclude-networks <em class="parameter">network-list</em>
                        </th>
                        
                        <td>
                          Optional. A comma-separated list of <a href="#available-networks">network types</a> and/or network names to exclude from the <code>--networks</code> list.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;folds <em class="parameter">number</em>
                        </th>
                        
                        <td>
                          Optional. The number of folds to use during cross validation. Defaults to 5.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;min <em class="parameter">number</em>
                        </th>
                        
                        <td>
                          Optional. The minimum number of positive genes for a query. Queries with a fewer number of genes will be skipped. Defaults to 10.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;max <em class="parameter">number</em>
                        </th>
                        
                        <td>
                          Optional. The maximum number of positive genes for a query. Queries with a larger number of genes will be skipped. Defaults to 300.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;use-go-cache
                        </th>
                        
                        <td>
                          Optional. Perform validation against bundled Gene Ontology gene sets. In this case, the query file should contain one GO id per line (e.g. <code>GO:0005786</code>). These gene sets have been pre-filtered so that the smallest has 10 genes and the largest has 300.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;outfile <em class="parameter">file-name</em>
                        </th>
                        
                        <td>
                          Optional. The file where the validation results should be saved. If not provided, the results are sent to standard output (usually the console).
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;auto-negatives
                        </th>
                        
                        <td>
                          Optional. Forces all non-positive genes to be labeled as negative examples during prediction. Otherwise, negative examples must be explicitly listed in the query file.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;method <em class="parameter">weighting-method</em>
                        </th>
                        
                        <td>
                          Optional. The <a href="#available-combining-methods">weighting method</a> to use when combining the individual networks. Defaults to <code>automatic</code>.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;seed <em class="parameter">number</em>
                        </th>
                        
                        <td>
                          Optional. A value used to initialize the pseudo random number generator used for shuffling each gene set during validation. Setting the seed to a constant value will make the validation results deterministic. Defaults to something pseudo-random.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;threads <em class="parameter">number</em>
                        </th>
                        
                        <td>
                          Optional. The maximum number of parallel predictions. Ideally this should be set to the number of processing cores. Defaults to 1.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;verbose
                        </th>
                        
                        <td>
                          Optional. Makes NetworkAssessor print more details about what&#8217;s happening.
                        </td>
                      </tr>
                    </table>
                    
                    <h3>
                      Query File Format:
                    </h3>
                    
                    <p>
                      Network Assessor uses the same <a href="#validation-query-format">query file format</a> as Cross Validator.
                    </p>
                  </div>
                  
                  <p>
                    <a name="validation-set-maker"></a>
                  </p>
                  
                  <h2>
                    Validation Set Maker
                  </h2>
                  
                  <div class="section">
                    <p>
                      Produces sets of genes based on Gene Ontology (GO) annotations for use in cross validation. One gene set is created for each GO category in the ontology. More specific annotations are propagated up to all genes associated with any of the parent annotations.
                    </p>
                    
                    <h3>
                      Usage (32-bit JVM):
                    </h3>
                    
                    <pre style="overflow: auto;">java -Xmx900M -jar GeneMANIA.jar ValidationSetMaker <em>options</em></pre>
                    
                    <h3>
                      Usage (64-bit JVM):
                    </h3>
                    
                    <pre style="overflow: auto;">java -d64 -Xmx3G -jar GeneMANIA.jar ValidationSetMaker <em>options</em></pre>
                    
                    <h3>
                      Options:
                    </h3>
                    
                    <table class="options">
                      <tr>
                        <th>
                          Name
                        </th>
                        
                        <th>
                          Description
                        </th>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;organism <em class="parameter">name</em>
                        </th>
                        
                        <td>
                          The name or taxonomy id of an <a href="#available-organisms">organism</a> whose genes should be considered.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;query <em class="parameter">filename</em>
                        </th>
                        
                        <td>
                          The file where the resulting validation set should be saved.
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;db <em class="parameter">JDBC-connection-string</em>
                        </th>
                        
                        <td>
                          Optional. A JDBC connection string for a GO MySQL database. No other database backends are currently supported. Defaults to EBI&#8217;s MySQL instance (i.e. <code>jdbc:mysql://mysql.ebi.ac.uk:4085/go_latest?user=go_select&password=amigo</code>)
                        </td>
                      </tr>
                      
                      <tr>
                        <th style="white-space: nowrap; font-family: monospace;">
                          &#8211;branch <em class="parameter">GO-branch</em>
                        </th>
                        
                        <td>
                          Optional. One of <code>bp</code>, <code>mf</code>, <code>cc</code>, or <code>all</code>, which selects GO categories from the biological process, molecular function, cellular component, or all branches, respectively. Defaults to <code>all</code>.
                        </td>
                      </tr>
                    </table>
                  </div>
                  
                  <h2>
                    Common Options
                  </h2>
                  
                  <div class="section">
                    <a name="available-organisms"></a>
                  </div>
                  
                  <h3>
                    Organisms:
                  </h3>
                  
                  <table class="options">
                    <tr>
                      <th>
                        Name
                      </th>
                      
                      <th>
                        Taxonomy Id
                      </th>
                    </tr>
                    
                    <tr>
                      <td>
                        A. Thaliana
                      </td>
                      
                      <td>
                        3702
                      </td>
                    </tr>
                    
                    <tr>
                      <td>
                        C. Elegans
                      </td>
                      
                      <td>
                        6239
                      </td>
                    </tr>
                    
                    <tr>
                      <td>
                        D. Melanogaster
                      </td>
                      
                      <td>
                        7227
                      </td>
                    </tr>
                    
                    <tr>
                      <td>
                        H. Sapiens
                      </td>
                      
                      <td>
                        9606
                      </td>
                    </tr>
                    
                    <tr>
                      <td>
                        M. Musculus
                      </td>
                      
                      <td>
                        10090
                      </td>
                    </tr>
                    
                    <tr>
                      <td>
                        S. Cerevisiae
                      </td>
                      
                      <td>
                        4932
                      </td>
                    </tr>
                    
                    <tr>
                      <td>
                        R. Norvegicus
                      </td>
                      
                      <td>
                        10116
                      </td>
                    </tr>
                  </table>
                  
                  <p>
                    <a name="available-networks"></a>
                  </p>
                  
                  <h3>
                    Networks
                  </h3>
                  
                  <p>
                    Networks may be specified by type or by name. To get a full listing of network names, use the option <code>--list-networks</code>.
                  </p>
                  
                  <h3>
                    Available Network Types:
                  </h3>
                  
                  <table class="options">
                    <tr>
                      <th style="white-space: nowrap; font-family: monospace;">
                        coexp
                      </th>
                      
                      <td>
                        Co-expression
                      </td>
                    </tr>
                    
                    <tr>
                      <th style="white-space: nowrap; font-family: monospace;">
                        coloc
                      </th>
                      
                      <td>
                        Co-localization
                      </td>
                    </tr>
                    
                    <tr>
                      <th style="white-space: nowrap; font-family: monospace;">
                        gi
                      </th>
                      
                      <td>
                        Genetic interactions
                      </td>
                    </tr>
                    
                    <tr>
                      <th style="white-space: nowrap; font-family: monospace;">
                        path
                      </th>
                      
                      <td>
                        Pathway interactions
                      </td>
                    </tr>
                    
                    <tr>
                      <th style="white-space: nowrap; font-family: monospace;">
                        pi
                      </th>
                      
                      <td>
                        Physical interactions
                      </td>
                    </tr>
                    
                    <tr>
                      <th style="white-space: nowrap; font-family: monospace;">
                        predict
                      </th>
                      
                      <td>
                        Predicted
                      </td>
                    </tr>
                    
                    <tr>
                      <th style="white-space: nowrap; font-family: monospace;">
                        spd
                      </th>
                      
                      <td>
                        Shared protein domains
                      </td>
                    </tr>
                    
                    <tr>
                      <th style="white-space: nowrap; font-family: monospace;">
                        other
                      </th>
                      
                      <td>
                        Networks that don&#8217;t belong to any of the above types.
                      </td>
                    </tr>
                    
                    <tr>
                      <th style="white-space: nowrap; font-family: monospace;">
                        default
                      </th>
                      
                      <td>
                        The default set of networks used by the Cytoscape plugin and <code>genemania.org</code>.
                      </td>
                    </tr>
                    
                    <tr>
                      <th style="white-space: nowrap; font-family: monospace;">
                        all
                      </th>
                      
                      <td>
                        Shorthand for specifying all available networks
                      </td>
                    </tr>
                    
                    <tr>
                      <th style="white-space: nowrap; font-family: monospace;">
                        preferred
                      </th>
                      
                      <td>
                        Shorthand for <code>coexp,pi,gi</code>. Typically used for cross validation.
                      </td>
                    </tr>
                  </table>
                  
                  <p>
                    <a name="available-combining-methods"></a>
                  </p>
                  
                  <h3>
                    Weighting Methods
                  </h3>
                  
                  <table class="options">
                    <tr>
                      <th style="white-space: nowrap; font-family: monospace;">
                        automatic
                      </th>
                      
                      <td>
                        Default — The networks are weighted such that the query genes interact as much as possible.</p> 
                        
                        <p>
                          <strong>Note:</strong> This option corresponds to the <em>query gene-based</em> combining method on the web site. If you want the same behaviour as the web site&#8217;s <em>automatic</em> combining method, use <em>automatic_relevance</em>.</td> </tr> 
                          
                          <tr>
                            <th style="white-space: nowrap; font-family: monospace;">
                              automatic_relevance
                            </th>
                            
                            <td>
                              A weighting method is chosen based on your query. This is the same behaviour as the &#8220;Automatically selected weighting method&#8221; option on the web site.
                            </td>
                          </tr>
                          
                          <tr>
                            <th style="white-space: nowrap; font-family: monospace;">
                              average
                            </th>
                            
                            <td>
                              All networks are weighted equally.
                            </td>
                          </tr>
                          
                          <tr>
                            <th style="white-space: nowrap; font-family: monospace;">
                              average_category
                            </th>
                            
                            <td>
                              Networks are weighted such that each type of network has the same overall weight.
                            </td>
                          </tr>
                          
                          <tr>
                            <th colspan="2">
                              For Organisms With GO Annotations:
                            </th>
                          </tr>
                          
                          <tr>
                            <th style="white-space: nowrap; font-family: monospace;">
                              bp
                            </th>
                            
                            <td>
                              Networks are weighted in an attempt to reproduce Gene Ontology Biological Process co-annotation patterns.
                            </td>
                          </tr>
                          
                          <tr>
                            <th style="white-space: nowrap; font-family: monospace;">
                              mf
                            </th>
                            
                            <td>
                              Networks are weighted in an attempt to reproduce Gene Ontology Molecular Function co-annotation patterns.
                            </td>
                          </tr>
                          
                          <tr>
                            <th style="white-space: nowrap; font-family: monospace;">
                              cc
                            </th>
                            
                            <td>
                              Networks are weighted in an attempt to reproduce Gene Ontology Cellular Component co-annotation patterns.
                            </td>
                          </tr></tbody> </table>