---
title: "Creating machine redable metadata"
teaching: 10
exercises: 0
questions:
- "?"
- "?"
objectives:
- ""
- ""
keypoints:
- "."
- ""
---

{% include links.md %}

# Creating machine redable metadata using FAIRifier

Use [FAIRifier](https://github.com/FAIRDataTeam/FAIRifier) to build The Resource Description Framework (RDF) of data.

The FAIRifier is a tool based on OpenRefine and shares its the functionalities. The main added functionality is to add the FAIRified data as RDF to a data resource.


## Summary

1.1 Based on Open Refine

1.2 FAIRification of VCF

1.3 FAIRification of FOAF


## Creating Identifiers, Step by Step 

This is a Do-It-Yourself guide to making your data more Findable, Accessible, Interoperable and Reusable using a set of Open Source tools developed at the Dutch TechCenter for Life Sciences. Although this workbook has been designed with the data producer in mind (that is, the non-IT expert), it should also be of use to computer scientists, data scientists and data managers who want to learn more about deploying and developing FAIR tools. 

In this workbook we will demonstrate the step-by-step FAIRification process for an example dataset containing human genetic variants. Note, the example dataset is represented in a standard  format called VCF (format specification here, some hints as to why VCF is not particularly FAIR).  This example dataset assumes some basic understanding of biology (we will work toward building simpler examples).  

The FAIRification process employs two tools: the OpenRefine FAIRifier and the Metadata Editor. You will access both of these tools via links in this workbook. Might be good to have a schematic summary of the tools… key functions (Note: If at any point you are unhappy about any operations, you can undo them by selecting the Undo/Redo tab in the left panel).

You can also use this workbook as a guide to complete the FAIRification of your own dataset. By following the same step-by-step procedure, it should be possible to expose your own data file on a FAIR Data Point going a long way to achieving Findability, Accessibility, and perhaps even automatic interoperation with other FAIR datasets. 

When working with your own data, we encourage you to record your experience at each step, so that your dataset can become an example to others who may wish to FAIRify similar data. We can then build up an Open library of example data FAIRifications for others to use and cite. 

### Steps

1. Make a new “Project” by opening the original VCF file in OpenRefine.
1. Open the OpenRefine FAIRifier here: open FAIRifier    [or shamanou]
1. Select “web addresses” and load this URL: http://fairifier-demo.fair-dtls.surf-hosted.nl/
1. Tell OpenRefine about the formatting of this VCF file using these  parameters: “ignore first 111 lines”, enable “tabs(TSV)”, disable “quotation marks…” can we make recommendations for the student dataset ? 
1. Before you proceed, append the project name with your name (so that it is easy to retrieve your project later). 
1. Click “Continue” to create the Project.


At this point, you are now in the main part of the user interface of OpenRefine. Here you can access all the OpenRefine functions. Let’s first look at some of the basic operations.
Note the display and paging options right above the table headers. Do we have variants for each of the chromosomes?
An easier way to answer this question is to use the built in facet browsing.

1. Select the pull-down menu for the #CHROM (chromosome) column.
1. Select “facet -> text facet”. A view will appear on the left giving a summary of chromosome occurrences. You can use this view to select only certain variants. You can create additional facets and combine them.

By choosing to work with VCF files, the user probably has a variant-centric point of view. In the VCF format each line represents a single variant. So lets create a data model that reflects our point of view. In this case the first step in our semantic model woudl be to assert that our data contains variants:
Look for an existing ontology that defines “variant”. Bioportal is a good place to start. Copy the URL for the class variant. We can make a small tutorial  (registries) on how to find ontologies… and I suppose have the emergency back up plan… how augment or make your own. 

1. Now open the RDF plugin options (top right) and select “Edit RDF skeleton”. A default (empty) skeleton is shown.
1. Select “add RDF type” and paste the “variant” class URL to indicate each row represents a thing of type variant.
1. Next select the “Preview” tab to see which triples we just defined.
Note the automatically generated subject URLs for the variants. In order to make sure our URL is unique (principle F1), use the “edit Base URI” option to change the BaseURI to a domain that you own (e.g. http://mysite.org/mydata/myvariants).
1. Click “ok” to save the skeleton and return to the main screen.

Let’s continue to extend the semantic data model by providing identifiers for the values in the ID column.In the VCF spec it can be found that the rs identifiers originate from DBSNP. However, anyone could define identifiers that are strings and start with rs. So let’s try to find an identifier that is unique and persistent (as required by principle F1). 
Go to http://identifiers.org and search for “dbsnp” in the search box. Open the single search result.
This page explains that identifiers.org maintains URLs for each rs identifier under the prefix “http://identifiers.org/dbsnp/”. Check out for example http://identifiers.org/dbsnp/rs146863629: it resolves to a page with information about variant rs146863629.
Our mission is to transform the ID column in OpenRefine  to use identifier.org URLs. In the ID column drop-down menu select “Edit cells -> Transform”
Select “language -> Jython” and use this expression to build the URL:
return "http://identifiers.org/dbsnp/" + value
Now you should see…. 
However, there is a problem. In the preview we can see URLs are also generated for empty cells !  So let’s fix this. Type… 
if value == ".":
    raise Exception
return "http://identifiers.org/dbsnp/" + value
Select the option “On error: set to blank” and press OK.

Having generated these URLs for our data points, we can now use them to extend our data model Skeleton:
Go back to “Edit skeleton”
First use the option “add prefix” and add “dc”. The URL for the Dublin Core ontology will be automatically filled in.
Next select the “property?” that links the row URI to ID, or (if it’s not visible), just select “add property”.
Start typing “identifier” and the autocomplete will suggest dc:identifier
Complete the triple by clicking on the object. Select “Use content from cell.. ID” “The cell's content is used.. as URI”
Go to the preview and see the newly generated triples.
Save the skeleton and return to the main screen.

Finally, we’ll add an identifier for #CHROM column
Look for an existing ontology that defines “chromosome”. A search in Bioportal for “chromosome 1” finds (among others) the NCIT. Open the NCIT result.
We can see that NCIT defines concepts for each human chromosome. However, note that the Chromosome URLs end with some code, so this time,  prepending a URL as we did  in the case of ID will not work.
We need to use the OpenRefine  function called “Reconciliation” to map column values to ontological terms. However, the #CHROM column contains too little information at this point,  for the reconciliation function to work.
Therefore we have to prepend the cells of #CHROM with the string “Chromosome ” using the “Edit cells -> Transform” option.
Now use the “Reconcile” function on the #CHROM column and select the service called “NCIT small”. Accept the defaults and proceed through the reconciliation steps.
In each #CHROM cell, OpenRefine will show the best matching concepts. Accept the using the single or double check-marks. Or accept all with the option “Reconcile -> Action -> Match each cell to best candidate”

Now that the #CHROM column has been reconciled, we can use the Chromosome URLs in our data model Skeleton
Go back to “Edit skeleton”
Add a triple to express “the variant is located on chromosome ...” . Find an existing predicate (Bioportal, OLS) or define your own URL.
For the object of the triple select “Use custom expression..” and add the expression that returns the reconciled URL:
Cell.recon.match.id
Finally check the triples in Preview and save the skeleton.

In the main screen use the “Export” button to export RDF data model where?  for all the variants.

## Now What ? 
In the previous steps we have taken the first steps to make the variant data FAIR. But what did we gain by this? Well, for example, the use of a globally unique and well-known identifier for the rs values in the ID column, we can now ask the question:
“Which variants potentially will cause a disease?”
We can do this by querying across our own variant resource and the DisGeNet dataset of known gene-disease associations. Here we use a federated SPARQL query over 1) the variant RDF we just generated (and loaded in a triple store) and 2) the SPARQL endpoint offered by DisGeNet. Execute the following query on this endpoint. Follow the links in the result to see which diseases association are known: should the person with these variants be worried?

PREFIX dc: <http://purl.org/dc/elements/1.1/> 
PREFIX sio: <http://semanticscience.org/resource/>

```{sql}
SELECT DISTINCT * WHERE {
  SERVICE <http://136.243.4.200:8892/repositories/mark-dtl-demo> {
    ?variant dc:identifier ?dbsnp .
  }
  SERVICE <http://rdf.disgenet.org/sparql/> {
    ?gene_disease sio:SIO_000001 ?dbsnp .
  }

} LIMIT 100
```

### Discussion points
The steps above demonstrate a manual process to make the variant data a little bit more FAIR. In order to increase FAIRness, we should consider to:

Use a better semantic model. In the OpenRefine hands-on we make some ad-hoc decisions about which ontologies, classes and predicates to use. However, to increase Interoperability, we probably should use the emerging standard ontologies for genomic data such as  FALDO or RSA.
Currently we only expose a very small part of the original VCF as FAIR data. By including more fields in our model, we’ll increase opportunities for (automatic) discovery and integration.
To make automatic discovery possible, we should publish our FAIR dataset (using appropriate FAIR metadata) in an online repository, such as for example a FAIR Data Point (FDP). To facilitate this, we are currently extending OpenRefine with an “export to FDP” function (using POST functionality of the FDP).
Using the RDF plugin, OpenRefine can be used to define a mapping (ie. skeleton, model or archetype) from a non-FAIR data representation to a FAIR data representation.
As we have seen, it could take many steps to make a VCF completely FAIR. However, for similar types of data, models and mappings may be reused. To facilitate this, we are considering to extend OpenRefine with access to a public model registry. 
What operations would you like to see in OpenRefine to use such a model registry?
Based on some data imported in OpenRefine, how would we be able to know which models apply to that data?
Do you know if public model registries already exist for Linked Data?
Tell us about your Linked Data generating tools and standard operating procedures (SOPs)
Would OpenRefine also work in your use cases?
Could your tool be used as a data FAIRifier? What steps of your SOP should become part of the FAIRification process?
Could your tool/SOP be connected to export directly to a Fair Data Point (FDP)?
