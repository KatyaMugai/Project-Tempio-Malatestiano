---
layout: default
title: Conclusion
---

  <h3 style="text-align: center;">Sections:</h3>
<div style="text-align: center; margin: 30px 0 25px 0; line-height: 1.8;">
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

<h1>Conclusion</h1>

<p>
  This project explored the RDF description of 
  <a href="https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046" target="_blank">
    Tempio Malatestiano
  </a> 
  in the ArCo Knowledge Graph in order to identify information that could benefit from enrichment.
</p>

<p>
  The analysis showed that Tempio Malatestiano is well documented in ArCo, especially through related photographic resources. However, some important information is represented only indirectly, mainly inside textual labels, rather than as direct structured RDF relations of the main architectural resource.
</p>

<hr>

<h2>Main findings</h2>

<p>
  The project identified two main gaps.
</p>

<h3>Gap 1: Internal architectural components</h3>

<p>
  The direct RDF description of Tempio Malatestiano includes only limited information about its construction elements. The SPARQL results showed that the facade is directly connected to the monument, while several internal chapels appear mainly in the labels of related photographic resources.
</p>

<p>
  These chapels include the Cappella delle Virtù, the Cappella dello Zodiaco, the Cappella degli Angeli and the Cappella degli Antenati.
</p>

<p>
  To address this gap, the proposed enrichment represents these chapels as construction elements using the existing ArCo property <code>cdesc:hasConstructionElement</code>.
</p>

<h3>Gap 2: Historical and artistic entities</h3>

<p>
  The second gap concerns historical and artistic entities associated with Tempio Malatestiano. The SPARQL analysis showed that entities such as Sigismondo Pandolfo Malatesta, Isotta degli Atti, the Crocifisso giottesco and the Stemma Malatesta appear in photographic resource labels, but are not directly connected to the main resource through structured RDF properties.
</p>

<p>
  To address this gap, the final enrichment reuses existing ArCo and ArCo Core properties instead of introducing new local properties.
</p>

<ul>
  <li><code>core:involvesAgent</code> is used for historical figures.</li>
  <li><code>a-dd:hasAssociatedObject</code> is used for the Crocifisso giottesco.</li>
  <li><code>a-dd:hasElementAffixedToCulturalProperty</code> is used for the Stemma Malatesta.</li>
</ul>

<hr>

<h2>RDF enrichment strategy</h2>

<p>
  The proposed enrichment transforms information that was previously implicit in textual labels into explicit RDF triples.
</p>

<p>
  The final modelling strategy follows a reuse-first approach. At an earlier stage of the project, a small local vocabulary extension was considered. However, after checking the existing ArCo ontology modules, we decided that suitable properties were already available.
</p>

<p>
  For this reason, the final version of the project does not introduce new local properties. The <code>ex:</code> namespace is used only for local resources representing the specific entities identified during the analysis, such as chapels, historical figures, artistic objects and heraldic elements.
</p>

<p>
  This decision made the enrichment less artificial and more consistent with the existing ArCo ontology.
</p>

<hr>

<h2>Role of SPARQL and LLMs</h2>

<p>
  SPARQL queries were the main tool used to explore the knowledge graph and identify the gaps. They made it possible to compare the direct RDF description of the monument with the information contained in related photographic resources.
</p>

<p>
  Large Language Models were used as supporting tools. Different prompting techniques were tested, including zero-shot prompting, chain-of-thought prompting and few-shot chain-of-thought prompting. However, the LLM outputs were not accepted automatically.
</p>

<p>
  The answers produced by the models were compared with the SPARQL results, and only information supported by the RDF data was used in the final interpretation and modelling.
</p>

<hr>

<h2>Final result</h2>

<p>
  The final enrichment proposal makes the representation of Tempio Malatestiano more explicit, structured and directly queryable.
</p>

<p>
  After the proposed enrichment, it would be possible to query the monument directly for its internal chapels, associated historical agents, related artistic object and affixed heraldic element.
</p>

<p>
  This is more effective than searching for these entities only inside photographic resource labels.
</p>

<p>
  Overall, the project shows that knowledge graph enrichment is not only about adding more data. It is also about deciding how to represent information correctly, how to reuse existing ontology properties and how to avoid unnecessary vocabulary extension.
</p>

<p>
  In this project, the most important result was the transformation of implicit information into explicit RDF triples while remaining aligned with the modelling principles already available in ArCo.
</p>

<hr>

<div style="display: flex; justify-content: space-between; margin-top: 2em;">
  <a href="challenges.html">Previous</a>
  <a href="index.html">Back to Home</a>
</div>
