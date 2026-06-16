---
layout: default
title: Challenges
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

<h1>Challenges</h1>

<p>
  This section describes the main difficulties we faced while working on the project and how we addressed them. Most of the challenges were not caused by the absence of data, but by the way the information was represented in the knowledge graph.
</p>

<hr>

<h2>1. Finding a suitable resource for enrichment</h2>

<p>
  At the beginning of the project, one of the first challenges was to choose a cultural heritage resource that was rich enough to analyse, but also suitable for RDF enrichment. Some resources were either too poor in structured data, too difficult to query, or not clearly connected to the kind of information we wanted to investigate.
</p>

<p>
  We eventually selected <strong>Tempio Malatestiano</strong> because it offered a good balance. It was clearly present in ArCo, it had a stable resource IRI, and it was connected to many related photographic resources. At the same time, its direct RDF description did not fully represent some important architectural, historical and artistic aspects of the monument.
</p>

<p>
  This made it a good case for Project 1: the resource was already documented, but it still contained information gaps that could be meaningfully addressed through RDF enrichment.
</p>

<hr>

<h2>2. Distinguishing direct RDF relations from indirect textual information</h2>

<p>
  The most important challenge was understanding the difference between information that is explicitly modeled in RDF and information that only appears inside textual labels.
</p>

<p>
  In the case of Tempio Malatestiano, ArCo contains many photographic resources linked to the main monument through <code>rdfs:seeAlso</code>. These photographic resources mention internal chapels, historical figures, artistic objects and heraldic elements. However, those elements are not necessarily modeled as direct RDF relations of the main architectural resource.
</p>

<p>
  This distinction was essential for the project. If we had only looked at the labels, we could have wrongly assumed that the knowledge graph already contained all the relevant information. Instead, we checked whether the same entities were directly connected to the main resource through structured properties.
</p>

<p>
  To address this challenge, we compared two levels of information: direct RDF properties of Tempio Malatestiano and labels of related photographic resources. This comparison allowed us to identify the actual gaps.
</p>

<hr>

<h2>3. Working with photographic resources</h2>

<p>
  Another difficulty was that many relevant details were hidden in the labels of photographic resources. These labels were useful because they mentioned specific parts of the monument, such as <strong>Cappella delle Virtù / S. Sigismondo</strong>, <strong>Cappella dello Zodiaco</strong>, <strong>Cappella degli Angeli</strong> and <strong>Cappella degli Antenati</strong>.
</p>

<p>
  However, labels are not the same as structured RDF descriptions. They are human-readable, but they are harder to query reliably. For example, the same entity can appear with slightly different wording, and some labels contain long descriptive strings with many details inside one text value.
</p>

<p>
  We addressed this by using <code>FILTER</code> and <code>REGEX</code> in SPARQL queries. This allowed us to search for recurring names in the labels and count how often they appeared. The results helped us understand which elements were important enough to become part of the proposed enrichment.
</p>

<hr>

<h2>4. Avoiding overinterpretation</h2>

<p>
  One risk in this project was to go beyond what the data actually supported. Some historical and artistic entities are clearly associated with Tempio Malatestiano from a cultural point of view, but the goal of the project was not simply to write a historical description of the monument. The goal was to identify what is present or missing in the RDF representation.
</p>

<p>
  For this reason, we tried to separate historical knowledge from graph-based evidence. When we found names such as <strong>Sigismondo Pandolfo Malatesta</strong>, <strong>Isotta degli Atti</strong>, <strong>Crocifisso giottesco</strong> and <strong>Stemma Malatesta</strong>, we checked whether they were directly linked to the main resource or only appeared in photographic labels.
</p>

<p>
  This helped us keep the enrichment grounded in the data. The proposed triples are not random additions: they are based on information that already appears in ArCo, but only indirectly.
</p>

<hr>

<h2>5. Choosing the right vocabulary</h2>

<p>
  Another challenge was deciding whether to use existing ArCo properties or create a small vocabulary extension.
</p>

<p>
  For the first gap, the solution was relatively clear. The property <code>cdesc:hasConstructionElement</code> was appropriate because the internal chapels can be modeled as construction elements of the monument. This allowed us to connect Tempio Malatestiano to resources such as <code>ex:CappellaDelleVirtu</code>, <code>ex:CappellaDelloZodiaco</code>, <code>ex:CappellaDegliAngeli</code> and <code>ex:CappellaDegliAntenati</code>.
</p>

<p>
  The second gap was more difficult. We needed to represent associated historical persons, artistic objects and heraldic elements. Since the existing vocabulary did not provide exactly the relations we wanted to express in this context, we proposed a small local vocabulary extension with properties such as <code>ex:hasAssociatedPerson</code>, <code>ex:containsArtisticObject</code> and <code>ex:hasHeraldicElement</code>.
</p>

<p>
  This solution made the enrichment more precise, but also required us to define new classes and properties clearly, using <code>rdfs:label</code>, <code>rdfs:comment</code>, <code>rdfs:domain</code> and <code>rdfs:range</code>.
</p>

<hr>

<h2>6. Designing SPARQL queries that were precise enough</h2>

<p>
  Some initial SPARQL queries were too broad and produced too many results, while others returned empty results because the information was not directly modeled where we expected it to be. This was especially visible when searching for historical names or internal architectural elements directly in the main resource.
</p>

<p>
  To solve this, we progressively made the queries more precise. We used <code>VALUES</code> to focus on the selected Tempio Malatestiano resource, <code>OPTIONAL</code> to retrieve labels when available, <code>FILTER</code> and <code>REGEX</code> to search for specific terms, and <code>LIMIT</code> and <code>ORDER BY</code> to keep the results manageable.
</p>

<p>
  We also used <code>UNION</code> to compare direct construction elements and photographic resource labels in the same query. This made the first gap clearer, because it showed the difference between what is directly modeled and what only appears indirectly in labels.
</p>

<hr>

<h2>7. Using LLMs without relying on them blindly</h2>

<p>
  Large Language Models were useful, but they also created a methodological challenge. They can produce fluent and historically plausible answers, but not every answer is automatically supported by the RDF data.
</p>

<p>
  For example, an LLM can easily explain the historical importance of Sigismondo Pandolfo Malatesta or the artistic relevance of Tempio Malatestiano. However, our project required something more specific: we needed to understand whether this information was represented in the knowledge graph and whether it could be turned into RDF triples.
</p>

<p>
  To address this, we used LLMs as support tools rather than as final authorities. Their answers were compared with SPARQL results. When an LLM suggested information that was not visible in the RDF data, we treated it carefully and did not use it as direct evidence for enrichment unless it was supported by the graph exploration.
</p>

<hr>

<h2>8. Building the website</h2>

<p>
  A more practical challenge was building the website itself. Since the project includes SPARQL queries, RDF triples, tables and explanations, some pages were difficult to format correctly in Markdown. Code blocks could easily break the layout if they were not closed properly, and some tables did not display as expected.
</p>

<p>
  To solve this, we used a combination of Markdown and HTML. For long SPARQL queries and Turtle triples, we used <code>&lt;pre&gt;&lt;code&gt;</code> blocks, because they were more stable on GitHub Pages. We also kept the same menu across the pages to make navigation easier and to follow the structure required for the project website.
</p>

<p>
  This part of the work was not only technical. It also helped us understand how to present the project more clearly, page by page, so that the methodology, results and enrichment proposals could be followed by a reader.
</p>

<hr>

<h2>What we learned from these challenges</h2>

<p>
  The main lesson of the project is that a knowledge graph can contain relevant information without representing it at the right semantic level. In our case, ArCo already contained many useful details about Tempio Malatestiano, but much of this information was hidden inside photographic resource labels.
</p>

<p>
  The challenge was therefore not simply to find new information, but to decide how to transform implicit textual information into explicit RDF triples. This required SPARQL exploration, careful interpretation of the results, and a small vocabulary extension.
</p>

<p>
  Overall, these challenges helped us understand that enrichment is not only about adding data. It is about making existing knowledge more structured, more searchable and more reusable.
</p>

<hr>

<div style="display: flex; justify-content: space-between; margin-top: 2em;">
  <a href="vocabulary-extension.html">Previous</a>
  <a href="conclusion.html">Next</a>
</div>