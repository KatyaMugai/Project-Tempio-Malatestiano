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
  During the development of our project on 
  <a href="https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046" target="_blank">
    Tempio Malatestiano
  </a>, 
  we encountered several challenges related to SPARQL exploration, gap identification, ontology reuse and RDF modelling.
</p>

<p>
  The main difficulty was not simply to find more information about the monument, but to understand how this information was represented in the ArCo Knowledge Graph and whether it could be made more explicit through RDF triples. Moreover, we had some difficulties creating the website since we are not experienced in this field.
</p>

<hr>

<h3>Understanding the difference between direct RDF data and indirect information</h3>

<p>
  One of the first challenges was distinguishing between information directly represented in RDF triples and information that appeared only indirectly through related resources. The main RDF description of Tempio Malatestiano contained structured information about the monument, but some important details appeared mainly in the labels of photographic resources linked through <code>rdfs:seeAlso</code>.
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

<h3>Extracting useful information  from photographic resource labels and creating proper SPARQL queries</h3>

<p>
  Another challenge was that the labels of photographic resources contained useful information, but this information was not already structured into separate entities and relations. Apart from that, it was sometimes hard to fully understand and decide how to create useful query for the search.
</p>

<p>
  For example, chapel names and historical references appeared inside textual labels. This made the information difficult to query directly unless the labels were searched and analysed with SPARQL.
</p>

<p>
  ✅ <strong>Solution:</strong>
</p>

<p>
  We used SPARQL expressions such as <code>REGEX</code>, <code>FILTER</code>, <code>BIND</code>, <code>VALUES</code> and aggregation to detect recurring names and group them into meaningful entities. This helped us identify which entities were sufficiently supported by the data. As for creating queries, we scanned through the websites that were attached as useful examples and figured out what to use. What is more, we asked LLMs to help us create some SPARQL queries.
</p>

<hr>

<h3>Choosing existing ontology properties instead of creating new ones</h3>

<p>
  One of the most important challenges concerned RDF modelling. At first, we considered creating local properties such as <code>ex:hasAssociatedPerson</code>, <code>ex:containsArtisticObject</code> and <code>ex:hasHeraldicElement</code>. However, this solution risked making the enrichment look artificial, because similar modelling options already existed in ArCo and ArCo Core.
</p>

<p>
  ✅ <strong>Solution:</strong>
</p>

<p>
  We revised the modelling strategy and decided to reuse existing properties whenever possible. The final RDF enrichment uses <code>cdesc:hasConstructionElement</code> for internal chapels, <code>core:involvesAgent</code> for historical figures, <code>a-dd:hasAssociatedObject</code> for the Crocifisso giottesco and <code>a-dd:hasElementAffixedToCulturalProperty</code> for the Stemma Malatesta. 
</p>

<hr>

<h3>Presenting SPARQL, RDF and everything clearly on the website</h3>

<p>
  A practical challenge was presenting everything, including SPARQL queries, RDF triples and ontology terms clearly on the GitHub Pages website. RDF and SPARQL code contain characters such as <code>&lt;</code> and <code>&gt;</code>, which can be interpreted as HTML tags if they are not formatted correctly. This sometimes caused code and links to appear incorrectly on the website. Several times the code of the website did not work as expected and we needed to double check whether it was written right or some symbols were missing.
</p>

<p>
  ✅ <strong>Solution:</strong>
</p>

<p>
  We formatted code blocks using <code>&lt;pre&gt;</code> and <code>&lt;code&gt;</code>, checked the rendered pages after each change, and corrected links and escaped characters when necessary. This made the final website clearer and easier to read. We also consulted the example websites codes to check how to make some specific details or how to get the code to work. Moreover, we consulted LLMs and asked them to check our code for mistakes when it was not working as expected.
</p>

<hr>

<h2>Final reflection</h2>

<p>
  These challenges helped us understand that knowledge graph enrichment is not only about adding more data. It also requires careful decisions about evidence, modelling choices and vocabulary reuse. Moreover, we learned how Github and website coding works and how even within Github sometimes it is needed to use different symbols for the same purpose depending on the file extension.
</p>

<p>
  The most important methodological decision was to avoid unnecessary vocabulary extension. Instead of creating new local properties, we reused existing ArCo properties and proposed new RDF triples that make implicit information more explicit and directly queryable. This made the final enrichment more consistent with Semantic Web principles and better aligned with the structure of the ArCo ontology.
</p>

<hr>

<div style="display: flex; justify-content: space-between; margin-top: 2em;">
  <a href="rdf-enrichment.html">Previous</a>
  <a href="conclusion.html">Next</a>
</div>
