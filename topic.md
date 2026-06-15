---
layout: default
title: Tempio Malatestiano
---

<div style="text-align: center; margin-bottom: 20px;">
  <a href="index.html">🏠 Home</a> |
  <a href="topic.html">🏛️ Topic</a> |
  <a href="methodology.html">🛠️ Methodology</a> |
  <a href="sparql.html">📊 SPARQL Results</a> |
  <a href="gaps.html">🔍 Identifying Gaps</a> |
  <a href="rdf-enrichment.html">🔗 RDF Enrichment</a> |
  <a href="vocabulary-extension.html">🧩 Vocabulary Extension</a> |
  <a href="llms.html">💬 LLMs</a> |
  <a href="challenges.html">⚠️ Challenges</a> |
  <a href="conclusion.html">✅ Conclusion</a>
</div>

# Tempio Malatestiano

_A Knowledge Graph Enrichment Project based on the ArCo Knowledge Graph_

---

## Selected Resource

For this project, we selected the ArCo resource describing **Tempio Malatestiano**, an architectural heritage object located in Rimini, Italy.

The selected resource is:

```text
https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046
Tempio Malatestiano was selected because it is a complex cultural heritage object. It is not only a church, but also a monument connected to architectural components, historical figures, artistic objects and symbolic elements.

This makes it a suitable case for exploring how cultural heritage information is represented in a knowledge graph and how this representation can be enriched through RDF triples.

⸻

Why Tempio Malatestiano?

Tempio Malatestiano is significant for this project because its ArCo representation contains both explicit and implicit information.

On the one hand, the main resource is already described as an architectural heritage object and is connected to several documentation and photographic resources.

On the other hand, our SPARQL exploration showed that some important information is not directly modeled as structured RDF relations of the main resource.

In particular, relevant information about internal chapels, historical figures and artistic elements appears mainly in the labels of related photographic resources.

This makes Tempio Malatestiano an interesting example of a cultural heritage object that is documented in the knowledge graph, but whose semantic representation can still be improved.

⸻

Project Objectives

The main objectives of this project are:

* to explore the ArCo knowledge graph using SPARQL;
* to analyse the RDF description of Tempio Malatestiano;
* to identify relevant information gaps;
* to propose new RDF triples that could enrich the knowledge graph;
* to suggest a small vocabulary extension when the existing vocabulary is not sufficient;
* to test how Large Language Models can support the interpretation of the identified gaps.

⸻

Focus of the Analysis

The project focuses on two main information gaps.

Gap 1: Internal Architectural Components

The first gap concerns the representation of internal architectural elements.

In the original RDF description, the main resource directly models only the facade as a construction element. However, related photographic resources mention several internal chapels, such as:

* Cappella delle Virtù / S. Sigismondo
* Cappella dello Zodiaco
* Cappella degli Angeli
* Cappella degli Antenati

This suggests that information about the internal structure of the monument exists in the knowledge graph, but it is not represented as direct construction-element relations of the main resource.

Gap 2: Historical and Artistic Entities

The second gap concerns historical and artistic entities associated with Tempio Malatestiano.

The related photographic resources mention several important figures and elements, including:

* Sigismondo Pandolfo Malatesta
* Isotta degli Atti
* Crocifisso giottesco
* Stemma Malatesta

However, these entities are not directly connected to the main architectural resource through explicit RDF properties.

⸻

Expected Enrichment

The proposed enrichment aims to transform implicit information into explicit RDF triples.

The enrichment focuses on:

* adding internal chapels as construction elements of Tempio Malatestiano;
* connecting the monument to associated historical persons;
* representing artistic and heraldic elements connected to the monument;
* introducing new resources and properties where needed.

In this way, the project improves the semantic granularity of the knowledge graph and makes the information more searchable, reusable and machine-readable.
<hr>
<div style="display: flex; justify-content: space-between; margin-top: 2em;">
  <a href="index.html">← Previous</a>
  <a href="methodology.html">Next →</a>
</div>
```
