---
title: "Building Semantic (Meta)data Models"
teaching: 0
exercises: 0
questions:
- "Key question (FIXME)"
objectives:
- "First learning objective. (FIXME)"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---
FIXME

{% include links.md %}

# Building Semantic (Meta)data Models

To make data and metadata machine-readable, we need semantic (meta)data models. Existing models can be used, however, unfortunately, currently these need to be constructed in most cases. Section 4A and 4B below describe these processes in detail.
Below are best practices...

## Building the Semantic Data Model

### Introduction

Building a semantic data model requires high expertise in the data domain and data modelling. Therefore, a semantic data model is generally constructed by more than one person. Currently, the initial modelling work is done by two persons, a data modeller and a domain expert. The data modeller and the domain expert initially discuss the data (step 1) until the data modeller gets comfortable with the data. The data modeller then constructs an initial model and discusses this with the domain expert. In this way, the data modelling is an ​iterative process.

Questions the ontology expert would ask the domain expert in the iterative process:

- The ontology expert wants to check with the domain expert if his interpretation of the
data, the context of the data, the metadata is correct.
- The Ontologies for the data at hand are chosen/identified by the ontology expert (not by
the domain expert)
- This consists of general guidelines together with community guidelines
([Unpublished manuscript​](https://docs.google.com/document/d/1J47Nb8pqg2idt4xUK2ouklPNZoTpCeWX6ZuSgjDfBQE/edit#heading=h.kt4o5k2ux5a3)).

Expertise / Skills of the Ontology Expert in the domain (the ​ROLODEX​):

- Ideally you would have ontology experts for the specific field. But this may not always be
feasible. It is not feasible if you are not in the domain. It is by definition an interdisciplinary skill. ​Basic domain knowledge and/or the capability to extract this information from the domain experts (sit next to each other)
- Is there a way to assess the domain knowledge of a person regarding semantic data modeling? ​GO FAIR templates or the GO FAIR Open Data Model Registry

Early on it is a good idea to check if there is a data model that you can reuse. Need to know where to look for existing models. Needs to know about places where the models are registered/published: ​[http://datahub.io](http://datahub.io).

Starting with your sketch, find/select the best ​ontologies:

- Read the “What is an ontology” tutorial
- Know the ​principles​ for selecting a good ontology (​Hunter, 2017​; ​Malone e​ t al.​ 2016​)
- Have skill with Ontology Search Tools
- If you didn't find a suitable ontology. If there is not ontology available: ​skill needed to
assess if it is needed to make a new ontology
  - Make a placeholder
  - Submit a request to an Ontology moderator, for augmentation: To be able to
submit a new ontology, several check items have to be checked.
  - Create a new ontology/vocabulary

Build your semantic data model (getting practical)

- Make or Find Globally Unique and Persistent Identifiers (​[F1​](https://www.go-fair.org/fair-principles/f1-meta-data-assigned-globally-unique-persistent-identifiers/)).
- Re-use existing ​[GO FAIR templates or the GO FAIR Open Data Model Registry](https://docs.google.com/document/d/1601htOnncFnYsdiIPtgpyEH9r5b4LiojJNePRa4HqCE/edit)

Identifiers: need domain knowledge (for example, gene ID, protein ID) and community standards (cancer versus rare disease)

- registries
- Choosing from among several identifiers schemes (consensus among domain expert
and data expert)... trying to relieve burden from domain expert
Factors in choosing and building good identifiers
Naming instances (building identifiers , augmenting identifiers from section 3)
- Re-use existing identifiers
- Creating (minting) new identifiers
- When to do one or the other (Instances typically need their own names)
Factors in choosing an building good data models
- Driving question / point of view / considerations of generality
- Capture observations independent of implications
- Choice of ontologies ( ontologies will impact the structure of the model)
- Level of detail
- Experience / skill to decide size / complexity of the model (trade off between simplicity
and complexity)
- Auto xcel to RDF models are usually too trivial (poor model)
- Community forum for discussing models (finding consensus on a model) see wikidata
After making model, then serialize (encapsulate) model (RML, shape expression), EBI RDF Data, then publish model
FAIRsharing is broader, but also has some data models in it
Review of semantic data models (​[current work​](https://drive.google.com/drive/folders/1LDAwLiZ1U4R3WOdIPp90x4H5fZvWSua9)):
For example: F1000 open peer review platform could be used to host (1) publication and (2) review of semantic data models. Such publications may include.....
- See HRB F1000 platform as an example: ​[https://hrbopenresearch.org](https://hrbopenresearch.org/)
- See HRB ​[ToDo​ notes](https://docs.google.com/document/d/1MKsHdgPyuVnAUsC_Gnjcg7amHQjrOS3XPsdvHzOV1aw/edit?userstoinvite=pclarkehome@gmail.com&ts=5a2e4463&actionButton=1) regarding the F1000 platform.


- Text: A4 human readable description of the intent. Purpose of the model, choice of ontology / vocabulary, [stay close to phenomena versus stay close to the experiment].
- Human readable illustration of the model: e.g. in draw.io
- Model: RDF
- The overall structure of the ‘publication’ could look something like this:
[http://nanopub.org/wordpress/?page_id=57](http://nanopub.org/wordpress/?page_id=57)
- Inspiration for how they do it in wikidata: Community of Data Modeling ​(see Andra)
- It’s licensed so people can know if they can reuse it.
- Reviewers can comments on each part of the submission
- See: ​[expressionatlas documentation](https://www.ebi.ac.uk/rdf/documentation/expressionatlas/)

### GO CHANGE (policy that needs to be revised)
### GO TRAIN (skills that need to be learned)
Skills to build a model
Building a model is “subjective”, first level model put together after discussion. Then get confirmation from the expert.
complexity insights to prevent combinatorial explosions

- Scalability of having billions of triples using code (performance, space/time limits)
- Performance awareness of FAIR Data and RDF
- Making processes FAIR (FAIR Services, dynamic FAIR process)
- Data transformation process... semantic annotation of your data
- FAIR Projector

## GO BUILD (tools that need to be developed)

- There is no metrics to assess the usability of the data!
- From draw.io -> rdf
- See HRB F1000 platform as an example: ​[https://hrbopenresearch.org](https://hrbopenresearch.org)
- See HRB ​[ToDo​ notes](https://docs.google.com/document/d/1MKsHdgPyuVnAUsC_Gnjcg7amHQjrOS3XPsdvHzOV1aw/edit?userstoinvite=pclarkehome@gmail.com&ts=5a2e4463&actionButton=1) regarding the F1000 platform

## Building the Semantic Metadata Model
INTRODUCTION
Recommend FDP & RDF , and show how this achieves high levels of FAIRness (this can commented upon for each principle). Then focus on other (community-level) metadata modeling. F3, F4, A1.2, A2, R1.1, R1.3,
Data should be described with rich metadata (​F2​), and this metadata should be assigned a globally unique and persistent identifier (​F1​). F3 and F4 also go here...

1. is there an existing metadata community standard? If so, is it FAIR ?
2. FDP metadata versus Community metadata standards ? Extensions to Kees’s metadata]
editor and possible role for CEDAR

- It should be possible to make your FAIR metadata descriptions, even if you do not know how to FAIRify your actual dataset.
- Moreover, it should be possible to make your FAIR metadata descriptions even before you create any data (for example, as part of your Data Stewardship Plan when you submitted your project proposal).
- Your Metadata is a publication in itself. It will have long-term persistence on the FAIR Data Point, even if your dataset should become no longer sustainable (​A2​). Your Data-Metadata can also be versioned, as needed.
- Defining your metadata is already a big step toward FAIRness (​F2, R1​)!
- Choose a metadata standard! OR Is there a institutional metadata profile?
- Some essential Metadata elements:
- Who are you? Do you have an email, phone number? ​[https://orcid.org]()
- You can retrieve RDF from ORCID, which can be basis for the
metadata!!!
- What is your affiliation? ​[https://www.grid.ac](https://www.grid.ac)
- Who paid for your research? ​[https://www.crossref.org/services/funder-registry/](https://www.crossref.org/services/funder-registry/) - Date-time?
  - Methods? Provenance (​R1.2​)?
  - What licence will you use (​R1.1​)? ​[https://creativecommons.org/licenses](https://creativecommons.org/licenses)
- Re-use metadata descriptions from the GO FAIR metadata templates or the GO FAIR
metadata registry
- Use Kees’s MetaData Editor (see also the ​INSPIRE editor​)
- Review the established model on set intervals, data models are not static and are
subject to constant revision

### GO CHANGE (policy that needs to be revised)

### GO TRAIN (skills that need to be learned)

- Legal skills
- Accessibility framework: Authentication / authorization, sensitive data
- Institutional policy documents -

### GO BUILD (tools that need to be developed)

- Metadata Profiles (people, funding agencies, research institutions)
- MetaData Editor ...
- [Center for Expanded Data Annotation and Retrieval (CEDAR)](https://more.metadatacenter.org/tools-training/cedar-template-tools/#find-template)

# REFERENCES
- [DIY guide​](https://lorentz.fair-dtls.surf-hosted.nl/FAIR_Lorentz.pdf) based in this ​[DIY document](https://docs.google.com/document/d/1jAEKz4yQCh4N6fVx_EXRhZrWcXCcYSvpSNiXaJAjBMY/edit#heading=h.xy88sp7tpl6o)