---
layout: default
title: Conclusion
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

<h1>Conclusion</h1>

<p>
  This project explored the representation of <strong>Tempio Malatestiano</strong> in the <strong>ArCo knowledge graph</strong> and focused on one main question: what relevant information about this monument is already present in the dataset, but not yet represented as explicit RDF relations? At the beginning, the resource seemed quite rich because it was connected to several descriptions and photographic resources. However, the SPARQL exploration showed that richness in documentation does not always mean richness in structured semantic representation.
</p>

<hr>

<h2>Main findings</h2>

<p>
  The first important result concerns the architectural structure of the monument. In the direct RDF description of Tempio Malatestiano, only the facade is explicitly modeled as a construction element. At the same time, many related photographic resources mention internal chapels, including <strong>Cappella delle Virtù / S. Sigismondo</strong>, <strong>Cappella dello Zodiaco</strong>, <strong>Cappella degli Angeli</strong> and <strong>Cappella degli Antenati</strong>. This showed that the information exists in ArCo, but it is hidden inside labels rather than modeled as direct construction-element relations.
</p>

<p>
  The second result concerns the historical and artistic context of the monument. The photographic resources mention important entities such as <strong>Sigismondo Pandolfo Malatesta</strong>, <strong>Isotta degli Atti</strong>, the <strong>Crocifisso giottesco</strong> and the <strong>Stemma Malatesta</strong>. These entities are meaningful for understanding Tempio Malatestiano, but they are not directly connected to the main architectural resource through structured RDF properties. For this reason, they became the basis for the second enrichment proposal.
</p>

<hr>

<h2>What the enrichment adds</h2>

<p>
  The proposed enrichment does not invent completely new information from outside the knowledge graph. Instead, it reorganizes information that was already visible in ArCo, but only indirectly. For the architectural gap, we proposed adding direct <code>cdesc:hasConstructionElement</code> relations between Tempio Malatestiano and the main internal chapels. For the historical and artistic gap, we proposed new relations such as <code>ex:hasAssociatedPerson</code>, <code>ex:containsArtisticObject</code> and <code>ex:hasHeraldicElement</code>.
</p>

<p>
  This makes the knowledge graph more useful. A user or an application would no longer need to search for chapel names, persons or artistic elements inside long photographic labels. Instead, these elements could be retrieved directly through RDF properties. In this sense, the enrichment improves not only the amount of information in the graph, but also the way that information can be found, reused and interpreted.
</p>

<hr>

<h2>Role of the vocabulary extension</h2>

<p>
  The vocabulary extension was necessary because not all the relations we needed were already available in a precise form for our use case. The class <code>ex:Chapel</code> allowed us to represent the internal chapels as architectural components, while <code>ex:ArtisticObject</code> and <code>ex:HeraldicElement</code> helped us distinguish artistic objects from heraldic or symbolic elements. The new properties also made the proposed relations clearer and more readable.
</p>

<p>
  This part of the project was useful because it showed that enrichment is not only about adding triples. Sometimes it also requires thinking about the vocabulary itself: which classes are needed, which properties express the relation more accurately, and how new resources should be described so that they are understandable both for humans and machines.
</p>

<hr>

<h2>Role of LLMs</h2>

<p>
  Large Language Models were useful as support tools, especially for generating hypotheses, rephrasing questions and checking whether some associations made sense from a cultural point of view. However, their answers could not be used as evidence on their own. The most important methodological decision was to compare the LLM outputs with the SPARQL results and to keep the RDF data as the main source of verification.
</p>

<p>
  This comparison made the role of LLMs clearer. They were helpful for interpretation, but the actual enrichment had to remain grounded in the knowledge graph. When the models gave broad historical answers, we checked whether the same information was actually visible in ArCo. When the models suggested entities or relations, we treated them as possible directions rather than final results.
</p>

<hr>

<h2>What we learned</h2>

<p>
  The project showed that a knowledge graph can contain a lot of information and still have gaps at the semantic level. In the case of Tempio Malatestiano, the issue was not simply missing data. The problem was that important information was present in a form that was difficult to reuse computationally: inside textual labels of photographic resources. By transforming this implicit information into explicit RDF triples, the proposed enrichment makes the graph more precise and more searchable.
</p>

<p>
  Another important lesson was that SPARQL exploration is not just a technical step. It is also a way of understanding how knowledge is organized. The queries helped us see the difference between direct RDF relations, related resources and textual descriptions. Without this distinction, it would have been easy to confuse “information mentioned somewhere” with “information modeled in the graph”.
</p>

<hr>

<h2>Final consideration</h2>

<p>
  Overall, the project demonstrates how the combination of SPARQL, RDF modeling and LLM-assisted reflection can support the enrichment of a cultural heritage knowledge graph. Tempio Malatestiano was already well documented in ArCo, but the enrichment proposed here makes some of its architectural, historical and artistic aspects more explicit. The final result is a more structured representation of the monument, where internal chapels, associated persons, artistic objects and heraldic elements can be queried directly instead of being found only through textual labels.
</p>

<p>
  For this reason, the project does not simply add more data to the graph. It improves the quality of the representation by turning hidden or implicit knowledge into clear semantic relations.
</p>

<hr>

<div style="display: flex; justify-content: space-between; margin-top: 2em;">
  <a href="challenges.html">Previous</a>
  <a href="index.html">Back to Home</a>
</div>