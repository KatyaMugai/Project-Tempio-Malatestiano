---
layout: default
title: Methodology
---


<div style="text-align: center; margin-bottom: 20px;">
  <a href="index.html">Home</a> |
  <a href="topic.html">Topic</a> |
  <a href="methodology.html">Methodology</a> |
  <a href="sparql.html">SPARQL Results</a> |
  <a href="gaps.html">Identifying Gaps</a> |
  <a href="llms.html">LLM Prompts</a> |
  <a href="rdf-enrichment.html">RDF Triples</a> |
  <a href="vocabulary-extension.html">Vocabulary Extension</a> |
  <a href="challenges.html">Challenges</a> |
  <a href="conclusion.html">Conclusion</a>
</div>

# Methodology

This section explains the methodology followed in our project to explore and enrich the RDF description of <strong>Tempio Malatestiano</strong> in the <strong>ArCo knowledge graph</strong>.

The project was based on a step-by-step process that combined <strong>SPARQL exploration</strong>, <strong>gap identification</strong>, <strong>RDF modeling</strong>, <strong>vocabulary extension</strong> and the use of <strong>Large Language Models</strong>.

---

## Step-by-step process

### 1. Selecting the topic

We selected <strong>Tempio Malatestiano</strong>, an architectural heritage resource located in Rimini, Italy.

This resource was chosen because it is a complex cultural heritage object. It is connected not only to architecture, but also to historical figures, artistic objects, internal chapels and symbolic elements.

For this reason, it is a suitable case for exploring how cultural heritage information is represented in a knowledge graph and how this representation can be enriched.

---

### 2. Exploring the ArCo knowledge graph

The first step of the analysis was to explore the ArCo knowledge graph through the official SPARQL endpoint.

We searched for the main resource describing Tempio Malatestiano and analysed its RDF description.

The selected resource is:

```text
https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046

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

In particular, we checked whether the main resource directly represented:

- internal architectural components;
- historical figures;
- artistic objects;
- heraldic or symbolic elements.

---

### 4. Exploring related photographic resources

The next step was to analyse the resources linked to <strong>Tempio Malatestiano</strong> through <code>rdfs:seeAlso</code>.

These related resources were especially important because many of them are photographic documentation resources.

The labels of these photographic resources contained relevant information about:

- internal chapels;
- tombs;
- sculptures;
- historical figures;
- artistic objects;
- heraldic elements.

This showed that some information was present in the dataset, but only indirectly through textual labels.

---

### 5. Identifying information gaps

By comparing the direct RDF description of the main resource with the information found in related photographic resources, we identified two main information gaps.

#### Gap 1: Internal architectural components

The first gap concerns the internal architectural structure of <strong>Tempio Malatestiano</strong>.

In the direct RDF description, only the facade is explicitly modeled as a construction element. However, the photographic resources repeatedly mention several internal chapels, such as:

- <strong>Cappella delle Virtù / S. Sigismondo</strong>;
- <strong>Cappella dello Zodiaco</strong>;
- <strong>Cappella degli Angeli</strong>;
- <strong>Cappella degli Antenati</strong>.

This suggests that these internal architectural components exist in the documentation, but they are not directly represented as construction elements of the main architectural resource.

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

We tested models such as <strong>ChatGPT</strong> and <strong>Gemini</strong> in order to see whether they could help interpret the identified gaps and suggest possible enrichment strategies.

Different prompting techniques were used, including:

- zero-shot prompting;
- chain-of-thought prompting;
- few-shot chain-of-thought prompting.

The answers produced by the models were compared with the evidence obtained through SPARQL queries.

The LLMs were not used as the only source of knowledge. Their role was to support interpretation and reflection, while the actual evidence came from the RDF data and SPARQL results.

---

### 7. Proposing RDF triples

After identifying the gaps, we proposed new RDF triples to enrich the knowledge graph.

For the first gap, we proposed adding direct links between <strong>Tempio Malatestiano</strong> and its internal chapels using the property <code>cdesc:hasConstructionElement</code>.

For the second gap, we proposed adding new relations between <strong>Tempio Malatestiano</strong> and historical or artistic entities associated with it.

The proposed enrichment aims to transform information that was previously implicit in labels into explicit RDF triples.

---

### 8. Creating a vocabulary extension

Some of the required relations were not sufficiently represented by the existing vocabulary.

For this reason, we proposed a small local vocabulary extension using the namespace:

<p>
  <code>@prefix ex: &lt;https://example.org/tempio-malatestiano/enrichment/&gt; .</code>
</p>

The vocabulary extension introduces:

- new classes;
- new resources;
- new properties;
- labels;
- comments;
- domains;
- ranges.

This makes the proposed enrichment more precise and semantically explicit.

---

### 9. Publishing the project website

The final step was to publish the project as a website using <strong>GitHub Pages</strong>.

The website presents the main parts of the project:

- the selected topic;
- the methodology;
- the SPARQL exploration;
- the identified gaps;
- the RDF enrichment;
- the vocabulary extension;
- the LLM prompts;
- the challenges;
- the conclusion.

---

## Tools used

### ArCo

<strong>ArCo</strong> was used as the main knowledge graph for the project. It provides RDF descriptions of Italian cultural heritage resources.

### SPARQL

<strong>SPARQL</strong> was used to query the ArCo knowledge graph.

We used <code>SELECT</code> queries to retrieve and analyse existing information, and <code>CONSTRUCT</code> queries to generate proposed RDF triples.

### RDF and RDFS

<strong>RDF</strong> was used to represent the proposed enrichment in the form of triples.

<strong>RDFS</strong> was used to define new classes, labels, comments, domains and ranges in the vocabulary extension.

### Large Language Models

<strong>Large Language Models</strong> were used to support the interpretation of the gaps and to compare different prompting strategies.

### GitHub Pages

<strong>GitHub Pages</strong> was used to publish the project website and organize the work into clear sections.

---

## Methodological logic

The central methodological idea of the project was to compare what is explicitly modeled in the RDF graph with what is only implicitly available in textual labels.

In the case of <strong>Tempio Malatestiano</strong>, the ArCo resource already contains many related photographic resources. However, several important pieces of information appear only in the labels of those resources.

The enrichment therefore aims to transform implicit textual information into explicit, structured and machine-readable RDF triples.

This process makes the knowledge graph more precise, more searchable and more useful for cultural heritage research.

<div style="display: flex; justify-content: space-between; margin-top: 2em;">
  <a href="topic.html">Previous</a>
  <a href="sparql.html">Next</a>
</div>
