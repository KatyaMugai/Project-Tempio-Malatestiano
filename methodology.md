---
layout: default
title: Methodology
---

  <h3 style="text-align: center;">Sections:</h3>
<div style="text-align: center; margin-bottom: 20px;">
  <a href="index.html">Home</a> |
  <a href="topic.html">Topic</a> |
  <a href="methodology.html">Methodology</a> |
  <a href="sparql.html">SPARQL Results</a> |
  <a href="gaps.html">Identifying Gaps</a> |
  <a href="llms.html">LLM Prompts</a> |
  <a href="rdf-enrichment.html">RDF Triples</a> |
  <a href="challenges.html">Challenges</a> |
  <a href="conclusion.html">Conclusion</a>
</div>

# Methodology

This section explains the methodology followed in our project to explore and enrich the RDF description of [**Tempio Malatestiano**](https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046.html) in the [**ArCo**](http://wit.istc.cnr.it/arco/) knowledge graph.

The project was based on a step-by-step process that combined <strong>SPARQL exploration</strong>, <strong>gap identification</strong>, <strong>RDF modeling</strong> and the use of <strong>Large Language Models</strong>.

---

## Step-by-step process

### 1. Selecting the topic

We selected [**Tempio Malatestiano**](https://en.wikipedia.org/wiki/Tempio_Malatestiano), an architectural heritage resource located in Rimini, Italy.

This resource was chosen because it is a complex cultural heritage object. It is connected not only to architecture, but also to historical figures and artistic objects.

---

### 2. Exploring the ArCo knowledge graph

The first step of the analysis was to explore the [ArCo](http://wit.istc.cnr.it/arco/) knowledge graph through the official [SPARQL endpoint](https://dati.cultura.gov.it/sparql). We searched for the [main resource](https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046.html) describing Tempio Malatestiano and analysed its RDF description.

The initial queries were used to retrieve:

- the label of the resource;
- its RDF types;
- its direct properties;
- its related resources;
- its documentation and photographic resources.

---

### 3. Analysing the direct RDF description

After identifying the main resource, we analysed which information was directly connected to it through RDF properties.
This step was important because the goal of the project was not only to find information about <strong>Tempio Malatestiano</strong>, but also to understand how this information is structured in the knowledge graph.

---

### 4. Exploring related photographic resources

The next step was to analyse the resources linked to <strong>Tempio Malatestiano</strong> through <code>rdfs:seeAlso</code>.

These related resources were especially important because many of them are photographic documentation resources, and their labels contained relevant information that was not directly represented as structured RDF relations of the main resource.

---

### 5. Identifying information gaps

By comparing the direct [RDF description](https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046.html) of the main resource with the information found in related photographic resources, we identified two main information gaps.

#### Gap 1: Internal architectural components

The first gap concerns the internal architectural structure of <strong>Tempio Malatestiano</strong>.

In the direct RDF description, only the facade is explicitly modeled as a construction element. However, the photographic resources repeatedly mention several internal chapels. This suggests that these internal architectural components exist in the documentation, but they are not directly represented as construction elements of the main architectural resource.

#### Gap 2: Historical and artistic entities

The second gap concerns historical and artistic entities associated with <strong>Tempio Malatestiano</strong>.

The photographic resources mention several important figures and elements, including:

- <strong>Sigismondo Pandolfo Malatesta</strong>;
- <strong>Isotta degli Atti</strong>;
- <strong>Crocifisso giottesco</strong>;
- <strong>Stemma Malatesta</strong>.

However, these entities are not directly connected to the main architectural resource through explicit RDF properties.

---

### 6. Using Large Language Models

Large Language Models were used as support tools during the project.

We tested models such as [**ChatGPT**](https://chat.openai.com/) and [**Gemini**](https://gemini.google.com/?hl=it) in order to see whether they could answer some questions concerning Tempio, help interpret the identified gaps and suggest possible enrichment strategies.

Different prompting techniques were used, including:

- zero-shot prompting;
- chain-of-thought prompting;
- few-shot chain-of-thought prompting.

The answers produced by the models were compared with the evidence obtained through SPARQL queries.

---

### 7. Proposing RDF triples

After identifying the gaps, **we proposed new RDF triples** to enrich the knowledge graph. The goal was not to create new properties, but to make implicit information explicit by reusing existing vocabulary from ArCo and related RDF vocabularies whenever possible.

For the **first gap**, we proposed adding direct links between **Tempio Malatestiano** and its internal chapels using the [existing ArCo property](http://wit.istc.cnr.it/arco/lode/extract?url=https://raw.githubusercontent.com/ICCD-MiBACT/ArCo/master/ArCo-release/ontologie/construction-description/construction-description.owl) <code>cdesc:hasConstructionElement</code>. For the **second gap**, we initially considered creating local properties to connect the monument with historical and artistic entities. However, after checking the existing ArCo ontology modules, we decided to reuse already available properties instead.

In the final RDF enrichment, historical figures are linked through the [existing ArCo Core property](http://wit.istc.cnr.it/arco/lode/extract?url=https://raw.githubusercontent.com/ICCD-MiBACT/ArCo/master/ArCo-release/ontologie/core/core.owl) <code>core:involvesAgent</code>. The Crocifisso giottesco is represented through <code>a-dd:hasAssociatedObject</code>, and the Stemma Malatesta is represented through <code>a-dd:hasElementAffixedToCulturalProperty</code>.

The enrichment aims to transform information that was previously implicit in photographic resource labels into explicit, structured and directly queryable RDF triples.

---

### 8. Publishing the project website

The final step was to publish the project as a website using [**GitHub Pages**](https://docs.github.com/en/pages).
The website presents the main parts of the project to present our project in an accessible and visually structured format.

---

## Tools used

### ArCo

[**ArCo**](http://wit.istc.cnr.it/arco/) was used as the main knowledge graph for the project. It provides RDF descriptions of Italian cultural heritage resources.

### SPARQL

[**SPARQL endpoint**](https://dati.cultura.gov.it/sparql) was used to query the ArCo knowledge graph.

We used <code>SELECT</code> queries to retrieve and analyse existing information, and <code>CONSTRUCT</code> queries to generate proposed RDF triples.

### RDF and RDFS

<strong>RDF</strong> was used to represent the proposed enrichment in the form of triples.

<strong>RDFS</strong> was used to define new classes, labels, comments, domains and ranges in the vocabulary extension.

### Large Language Models

<strong>Large Language Models</strong> were used to support the interpretation of the gaps and to compare different prompting strategies.

### GitHub Pages

[**GitHub Pages**](https://docs.github.com/en/pages) was used to publish the project website and organize the work into clear sections.

<div style="display: flex; justify-content: space-between; margin-top: 2em;">
  <a href="topic.html">Previous</a>
  <a href="sparql.html">Next</a>
</div>
