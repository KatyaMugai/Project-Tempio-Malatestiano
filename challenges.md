---
layout: default
title: Challenges
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

<h1>Challenges Faced During the Project</h1>

<p>
  During the development of our KE4H project on 
  <a href="https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046" target="_blank">
    Tempio Malatestiano
  </a>, 
  we encountered several challenges related to SPARQL exploration, gap identification, ontology reuse and RDF modelling.
</p>

<p>
  The main difficulty was not simply to find more information about the monument, but to understand how this information was represented in the ArCo Knowledge Graph and whether it could be made more explicit through RDF triples.
</p>

<hr>

<h3>Understanding the difference between direct RDF data and indirect information</h3>

<p>
  One of the first challenges was distinguishing between information directly represented in RDF triples and information that appeared only indirectly through related resources.
</p>

<p>
  The main RDF description of Tempio Malatestiano contained structured information about the monument, but some important details appeared mainly in the labels of photographic resources linked through <code>rdfs:seeAlso</code>.
</p>

<p>
  This was especially important for the internal chapels and for historical or artistic entities such as Sigismondo Pandolfo Malatesta, Isotta degli Atti, the Crocifisso giottesco and the Stemma Malatesta.
</p>

<p>
  ✅ <strong>Solution:</strong>
</p>

<p>
  We compared the direct RDF description of the monument with the information found in related photographic resources. This allowed us to identify information that was present in the dataset but not directly represented as structured RDF relations of the main resource.
</p>

<hr>

<h3>Extracting useful information from photographic resource labels</h3>

<p>
  Another challenge was that the labels of photographic resources contained useful information, but this information was not already structured into separate entities and relations.
</p>

<p>
  For example, chapel names and historical references appeared inside textual labels. This made the information difficult to query directly unless the labels were searched and analysed with SPARQL.
</p>

<p>
  ✅ <strong>Solution:</strong>
</p>

<p>
  We used SPARQL expressions such as <code>REGEX</code>, <code>FILTER</code>, <code>BIND</code>, <code>VALUES</code> and aggregation to detect recurring names and group them into meaningful entities. This helped us identify which entities were sufficiently supported by the data.
</p>

<hr>

<h3>Avoiding overinterpretation of the data</h3>

<p>
  A major challenge was deciding which entities should be included in the enrichment proposal and which ones should be excluded.
</p>

<p>
  Not every name appearing in a label was strong enough evidence for a new RDF triple. Some entities appeared frequently, while others appeared only once or in potentially ambiguous contexts.
</p>

<p>
  ✅ <strong>Solution:</strong>
</p>

<p>
  We followed a conservative approach. We selected only entities that were clearly relevant to Tempio Malatestiano and sufficiently supported by the SPARQL results. This helped us avoid adding speculative or weakly justified information to the proposed enrichment.
</p>

<hr>

<h3>Choosing existing ontology properties instead of creating new ones</h3>

<p>
  One of the most important challenges concerned RDF modelling. At first, we considered creating local properties such as <code>ex:hasAssociatedPerson</code>, <code>ex:containsArtisticObject</code> and <code>ex:hasHeraldicElement</code>.
</p>

<p>
  However, this solution risked making the enrichment look artificial, because similar modelling options already existed in ArCo and ArCo Core.
</p>

<p>
  ✅ <strong>Solution:</strong>
</p>

<p>
  We revised the modelling strategy and decided to reuse existing properties whenever possible. The final RDF enrichment uses <code>cdesc:hasConstructionElement</code> for internal chapels, <code>core:involvesAgent</code> for historical figures, <code>a-dd:hasAssociatedObject</code> for the Crocifisso giottesco and <code>a-dd:hasElementAffixedToCulturalProperty</code> for the Stemma Malatesta.
</p>

<p>
  As a result, we cancelled the vocabulary extension and kept the <code>ex:</code> namespace only for the new local resources introduced by the project, not for new properties.
</p>

<hr>

<h3>Using LLMs critically</h3>

<p>
  Large Language Models were useful for generating ideas and comparing possible interpretations, but their answers could not be accepted automatically.
</p>

<p>
  Some answers were too general or not directly supported by the RDF data. This was a challenge because the project needed to remain based on evidence from the knowledge graph, not only on external knowledge or general descriptions of the monument.
</p>

<p>
  ✅ <strong>Solution:</strong>
</p>

<p>
  We used different prompting techniques, including zero-shot prompting, chain-of-thought prompting and few-shot chain-of-thought prompting. The outputs were compared with the SPARQL results, and only information supported by the data was used in the final interpretation and RDF modelling.
</p>

<hr>

<h3>Presenting SPARQL and RDF clearly on the website</h3>

<p>
  A practical challenge was presenting SPARQL queries, RDF triples and ontology terms clearly on the GitHub Pages website.
</p>

<p>
  RDF and SPARQL code contain characters such as <code>&lt;</code> and <code>&gt;</code>, which can be interpreted as HTML tags if they are not formatted correctly. This sometimes caused code and links to appear incorrectly on the website.
</p>

<p>
  ✅ <strong>Solution:</strong>
</p>

<p>
  We formatted code blocks using <code>&lt;pre&gt;</code> and <code>&lt;code&gt;</code>, checked the rendered pages after each change, and corrected links and escaped characters when necessary. This made the final website clearer and easier to read.
</p>

<hr>

<h2>Final reflection</h2>

<p>
  These challenges helped us understand that knowledge graph enrichment is not only about adding more data. It also requires careful decisions about evidence, modelling choices and vocabulary reuse.
</p>

<p>
  The most important methodological decision was to avoid unnecessary vocabulary extension. Instead of creating new local properties, we reused existing ArCo properties and proposed new RDF triples that make implicit information more explicit and directly queryable.
</p>

<p>
  This made the final enrichment more consistent with Semantic Web principles and better aligned with the structure of the ArCo ontology.
</p>

<hr>

<div style="display: flex; justify-content: space-between; margin-top: 2em;">
  <a href="rdf-enrichment.html">Previous</a>
  <a href="conclusion.html">Next</a>
</div>
