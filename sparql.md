---
layout: default
title: SPARQL Results
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
  <a href="vocabulary-extension.html">Vocabulary Extension</a> |
  <a href="challenges.html">Challenges</a> |
  <a href="conclusion.html">Conclusion</a>
</div>

<h1>SPARQL Queries & Results</h1>

<p>
  This section presents the main SPARQL queries used to explore the ArCo Knowledge Graph and analyse the RDF description of <strong>Tempio Malatestiano</strong>.
</p>

<p>
  The purpose of these queries was to understand what is already explicitly represented in ArCo and what information appears only indirectly through related resources, especially photographic documentation.
</p>

<hr>

<h2>Query 1 — Finding the main ArCo resource</h2>

<p>
  The first step was to identify the main ArCo resource corresponding to <a href="https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046.html" target="_blank"><strong>Tempio Malatestiano</strong></a>.
</p>

<h3>Explanation of keywords used</h3>

<ul>
  <li><code>rdfs:label</code>: retrieves the textual label of a resource.</li>
  <li><code>FILTER</code>: restricts the results according to a condition.</li>
  <li><code>REGEX</code>: searches for a pattern inside a string.</li>
  <li><code>DISTINCT</code>: removes duplicate results.</li>
</ul>

<h3>SPARQL Query</h3>

<pre><code>PREFIX rdfs: &lt;http://www.w3.org/2000/01/rdf-schema#&gt;

SELECT DISTINCT ?cp ?label
WHERE {
  ?cp rdfs:label ?label .
  FILTER(REGEX(STR(?label), "Tempio Malatestiano", "i"))
}
LIMIT 50
</code></pre>

<h3>Results</h3>

<p>
  The query confirmed that ArCo <strong>contains a resource</strong> corresponding to Tempio Malatestiano.
</p>

<p>
  The selected resource for the project is:
</p>

  <pre><code>https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046
  </code></pre>

<p>
  This resource became the <strong>main subject</strong> of the following SPARQL exploration.
</p>

<hr>

<h2>Query 2 — Exploring the direct RDF description</h2>

<p>
  After identifying the main resource, we explored its direct RDF description. The goal was to understand which <strong>properties and values are directly connected</strong> to the main resource.
</p>

<h3>Explanation of keywords used</h3>

<ul>
  <li><code>?p</code>: represents the predicate or property.</li>
  <li><code>?o</code>: represents the object or value connected to the resource.</li>
  <li><code>OPTIONAL</code>: retrieves labels only when they are available.</li>
  <li><code>ORDER BY</code>: sorts the results.</li>
</ul>

<h3>SPARQL Query</h3>

<pre><code>PREFIX rdfs: &lt;http://www.w3.org/2000/01/rdf-schema#&gt;

SELECT DISTINCT ?p ?pLabel ?o ?oLabel
WHERE {
  VALUES ?cp { &lt;https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046&gt; }

  ?cp ?p ?o .

  OPTIONAL { ?p rdfs:label ?pLabel . }
  OPTIONAL { ?o rdfs:label ?oLabel . }
}
ORDER BY ?p
LIMIT 100
</code></pre>

<h3>Results</h3>

<p>
  The query showed that the main resource has several direct properties, including type, location, documentation and depictions.
</p>

<p>
  However, the direct RDF description <strong>did not provide a detailed structured representation</strong> of the internal architectural components of the monument or of the historical and artistic entities associated with it.
</p>

<hr>

<h2>Query 3 — Checking existing construction elements</h2>

<p>
  This query was used to check which construction elements are directly linked to Tempio Malatestiano.
</p>

<p>
  This step was important because one of the goals of the project was to understand whether the internal chapels of the monument are already represented as structured architectural components.
</p>

<h3>Explanation of keywords used</h3>

<ul>
  <li><code>cdesc:hasConstructionElement</code>: identifies construction elements associated with a cultural heritage resource.</li>
  <li><code>VALUES</code>: restricts the query to the selected Tempio Malatestiano resource.</li>
  <li><code>OPTIONAL</code>: retrieves the label of the construction element when available.</li>
</ul>

<h3>SPARQL Query</h3>

<pre><code>PREFIX rdfs: &lt;http://www.w3.org/2000/01/rdf-schema#&gt;
PREFIX cdesc: &lt;https://w3id.org/arco/ontology/construction-description/&gt;

SELECT DISTINCT ?element ?elementLabel
WHERE {
  VALUES ?cp { &lt;https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046&gt; }

  ?cp cdesc:hasConstructionElement ?element .

  OPTIONAL { ?element rdfs:label ?elementLabel . }
}
ORDER BY ?elementLabel
LIMIT 100
</code></pre>

<h3>Results</h3>

<p>
  The query returned only <strong>one construction element</strong>:
</p>

<p>
  <code>https://w3id.org/arco/resource/Facade/0800163046-1</code>
</p>

<p>
  The labels of this resource are:
</p>

<ul>
  <li><code>Facade 1 of cultural property: 0800163046</code></li>
  <li><code>Facciata 1 del bene culturale: 0800163046</code></li>
</ul>

<h3>Interpretation</h3>

<p>
  This result shows that, in the direct RDF description, only the facade is explicitly modeled as a construction element of Tempio Malatestiano.
</p>

<p>
  This result became the starting point for the first identified gap: <strong>internal chapels are not directly represented as construction elements</strong>.
</p>

<hr>

<h2>Query 4 — Finding internal chapels in photographic resources</h2>

<p>
  Since the direct RDF description returned only the facade as a construction element, the next step was to examine the photographic resources linked to Tempio Malatestiano through <code>rdfs:seeAlso</code>.
</p>

<p>
  In this query, we used <code>UNION</code> in order to compare two different types of information in one query:
</p>

<ul>
  <li>construction elements directly connected to the main Tempio Malatestiano resource;</li>
  <li>internal chapels mentioned only in the labels of related photographic resources.</li>
</ul>

<p>
  The aim was to check whether internal architectural elements were explicitly modeled as construction elements or only indirectly mentioned in photographic resource labels.
</p>

<h3>Explanation of keywords used</h3>

<ul>
  <li><code>UNION</code>: combines the results of two different graph patterns in one query.</li>
  <li><code>cdesc:hasConstructionElement</code>: retrieves construction elements directly connected to the main cultural heritage resource.</li>
  <li><code>rdfs:seeAlso</code>: links the main resource to related resources, including photographic documentation.</li>
  <li><code>photoLabel</code>: contains the label of each related photographic resource.</li>
  <li><code>REGEX</code>: searches for specific chapel names in the labels.</li>
  <li><code>COUNT</code>: counts how many resources mention or represent each element.</li>
  <li><code>GROUP BY</code>: groups the results by source and element name.</li>
</ul>

<h3>SPARQL Query</h3>

<pre><code>PREFIX rdfs: &lt;http://www.w3.org/2000/01/rdf-schema#&gt;
PREFIX cdesc: &lt;https://w3id.org/arco/ontology/construction-description/&gt;

SELECT ?source ?elementName (COUNT(DISTINCT ?item) AS ?numberOfResources)
WHERE {
  VALUES ?cp { &lt;https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046&gt; }

  {
    ?cp cdesc:hasConstructionElement ?item .
    BIND("Direct construction element" AS ?source)
    BIND("Facade" AS ?elementName)
  }

  UNION

  {
    ?cp rdfs:seeAlso ?item .
    ?item rdfs:label ?photoLabel .

    BIND("Photographic resource label" AS ?source)

    BIND(
      IF(REGEX(STR(?photoLabel), "Cappella degli Antenati", "i"), "Cappella degli Antenati",
      IF(REGEX(STR(?photoLabel), "Cappella degli Angeli", "i"), "Cappella degli Angeli",
      IF(REGEX(STR(?photoLabel), "Cappella delle Virt", "i"), "Cappella delle Virtù / S. Sigismondo",
      IF(REGEX(STR(?photoLabel), "Cappella dello Zodiaco", "i"), "Cappella dello Zodiaco",
      IF(REGEX(STR(?photoLabel), "Cappella d.Isotta", "i"), "Cappella d'Isotta",
      ""))))) AS ?elementName
    )

    FILTER(?elementName != "")
  }
}
GROUP BY ?source ?elementName
ORDER BY ?source DESC(?numberOfResources)
</code></pre>

<h3>Results</h3>

<table>
  <thead>
    <tr>
      <th>Source</th>
      <th>Architectural element</th>
      <th>Number of resources</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Direct construction element</td>
      <td>Facade</td>
      <td>1</td>
    </tr>
    <tr>
      <td>Photographic resource label</td>
      <td>Cappella delle Virtù / S. Sigismondo</td>
      <td>54</td>
    </tr>
    <tr>
      <td>Photographic resource label</td>
      <td>Cappella dello Zodiaco</td>
      <td>43</td>
    </tr>
    <tr>
      <td>Photographic resource label</td>
      <td>Cappella degli Angeli</td>
      <td>28</td>
    </tr>
    <tr>
      <td>Photographic resource label</td>
      <td>Cappella degli Antenati</td>
      <td>26</td>
    </tr>
    <tr>
      <td>Photographic resource label</td>
      <td>Cappella d'Isotta</td>
      <td>1</td>
    </tr>
  </tbody>
</table>

<h3>Interpretation</h3>

<p>
  The results show a clear difference between structured RDF data and information that appears only indirectly in textual labels.
</p>

<p>
  The first part of the query returns the <strong>facade</strong> as the only construction element directly connected to the main Tempio Malatestiano resource.
</p>

<p>
  The second part of the query returns several internal chapels that are repeatedly mentioned in the labels of related photographic resources, such as <strong>Cappella delle Virtù / S. Sigismondo</strong>, <strong>Cappella dello Zodiaco</strong>, <strong>Cappella degli Angeli</strong> and <strong>Cappella degli Antenati</strong>.
</p>

<p>
  This confirms that information about the internal architectural structure of Tempio Malatestiano exists in ArCo, but it is stored indirectly in photographic resource labels rather than explicitly represented as construction-element relations.
</p>

<h2>Query 5 — Finding historical and artistic entities in photographic resources</h2>

<p>
  The next query focused on <strong>historical and artistic entities</strong> associated with Tempio Malatestiano.
</p>

<p>
  The aim was to check whether important persons, artistic objects and symbolic elements appear in the labels of related photographic resources.
</p>

<h3>Explanation of keywords used</h3>

<ul>
  <li><code>REGEX</code>: searches for historical and artistic names in photographic labels.</li>
  <li><code>BIND</code>: creates a new variable to group different textual matches.</li>
  <li><code>COUNT</code>: counts how many photographic resources mention each entity.</li>
  <li><code>GROUP BY</code>: groups the results by entity name.</li>
</ul>

<h3>SPARQL Query</h3>

<pre><code>PREFIX rdfs: &lt;http://www.w3.org/2000/01/rdf-schema#&gt;

SELECT ?entityName (COUNT(DISTINCT ?photo) AS ?numberOfPhotos)
WHERE {
  VALUES ?cp { &lt;https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046&gt; }

  ?cp rdfs:seeAlso ?photo .
  ?photo rdfs:label ?photoLabel .

  BIND(
    IF(REGEX(STR(?photoLabel), "Sigismondo Pandolfo Malatesta", "i"), "Sigismondo Pandolfo Malatesta",
    IF(REGEX(STR(?photoLabel), "Sigismondo Malatesta", "i"), "Sigismondo Malatesta",
    IF(REGEX(STR(?photoLabel), "Isotta degli Atti", "i"), "Isotta degli Atti",
    IF(REGEX(STR(?photoLabel), "San Sigismondo", "i"), "San Sigismondo",
    IF(REGEX(STR(?photoLabel), "Crocifisso giottesco", "i"), "Crocifisso giottesco",
    IF(REGEX(STR(?photoLabel), "stemma.*Malatesta|Malatesta.*stemma", "i"), "Stemma Malatesta",
    IF(REGEX(STR(?photoLabel), "statua di Sigismondo", "i"), "Statua di Sigismondo",
    ""))))))) AS ?entityName
  )

  FILTER(?entityName != "")
}
GROUP BY ?entityName
ORDER BY DESC(?numberOfPhotos)
</code></pre>

<h3>Results</h3>

<table>
  <thead>
    <tr>
      <th>Entity</th>
      <th>Number of photographic resources</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Sigismondo Pandolfo Malatesta</td>
      <td>9</td>
    </tr>
    <tr>
      <td>Sigismondo Malatesta</td>
      <td>8</td>
    </tr>
    <tr>
      <td>Isotta degli Atti</td>
      <td>3</td>
    </tr>
    <tr>
      <td>Statua di Sigismondo</td>
      <td>2</td>
    </tr>
    <tr>
      <td>Stemma Malatesta</td>
      <td>2</td>
    </tr>
    <tr>
      <td>Crocifisso giottesco</td>
      <td>1</td>
    </tr>
  </tbody>
</table>

<h3>Interpretation</h3>

<p>
  The query shows that several historical and artistic entities are present in the labels of related photographic resources and are connected to Tempio Malatestiano.
</p>

<hr>

<h2>Query 6 — Checking whether historical and artistic entities are directly linked</h2>

<p>
  The final query was used to check whether the historical and artistic entities identified in photographic labels were already directly linked to the main Tempio Malatestiano resource.
</p>

<p>
  To do this, we excluded <code>rdfs:seeAlso</code> and searched only among the direct properties of the main resource.
</p>

<h3>Explanation of keywords used</h3>

<ul>
  <li><code>FILTER(?p != rdfs:seeAlso)</code>: excludes related photographic resources.</li>
  <li><code>REGEX</code>: searches for selected names among direct object values and labels.</li>
  <li><code>OPTIONAL</code>: retrieves labels for properties and objects when available.</li>
</ul>

<h3>SPARQL Query</h3>

<pre><code>PREFIX rdfs: &lt;http://www.w3.org/2000/01/rdf-schema#&gt;

SELECT DISTINCT ?p ?pLabel ?o ?oLabel
WHERE {
  VALUES ?cp { &lt;https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046&gt; }

  ?cp ?p ?o .

  OPTIONAL { ?p rdfs:label ?pLabel . }
  OPTIONAL { ?o rdfs:label ?oLabel . }

  FILTER(?p != rdfs:seeAlso)

  FILTER(
    REGEX(STR(?o), "Sigismondo", "i") ||
    REGEX(STR(?o), "Malatesta", "i") ||
    REGEX(STR(?o), "Isotta", "i") ||
    REGEX(STR(?o), "Giotto", "i") ||
    REGEX(STR(?o), "Crocifisso", "i") ||
    REGEX(STR(?o), "stemma", "i") ||
    REGEX(STR(?oLabel), "Sigismondo", "i") ||
    REGEX(STR(?oLabel), "Malatesta", "i") ||
    REGEX(STR(?oLabel), "Isotta", "i") ||
    REGEX(STR(?oLabel), "Giotto", "i") ||
    REGEX(STR(?oLabel), "Crocifisso", "i") ||
    REGEX(STR(?oLabel), "stemma", "i")
  )
}
ORDER BY ?p
LIMIT 100
</code></pre>

<h3>Results</h3>

<p>
  This query returned no results.
</p>

<h3>Interpretation</h3>

<p>
  The absence of results confirms that the selected historical and artistic entities are not directly connected to the main Tempio Malatestiano resource through structured RDF properties. They appear mainly through the labels of related photographic resources. This became the basis for the second identified gap and for the proposed RDF enrichment.
</p>

<hr>

<h2>Conclusion of the SPARQL exploration</h2>

<p>
  The SPARQL exploration showed that Tempio Malatestiano is already well documented in ArCo, especially through related photographic resources. However, the analysis also revealed that some important information is not represented as explicit RDF relations of the main architectural resource. 
</p>
  
  <p>
  The first gap concerns the internal architectural components of the monument. The second gap concerns historical and artistic entities associated with it.
</p>

<p>
  These results provided the evidence for the following sections of the project: <strong>Identifying Gaps</strong>, <strong>RDF Triples</strong> and <strong>Vocabulary Extension</strong>.
</p>

<hr>

<div style="display: flex; justify-content: space-between; margin-top: 2em;">
  <a href="methodology.html">Previous</a>
  <a href="gaps.html">Next</a>
</div>
