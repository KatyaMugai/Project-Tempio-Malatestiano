---
layout: default
title: Vocabulary Extension
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

<h1>Vocabulary Extension</h1>

<p>
  This section presents the vocabulary extension proposed for the enrichment of the RDF description of <strong>Tempio Malatestiano</strong>.
</p>

<p>
  The SPARQL exploration showed that some relevant information about the monument is present in ArCo, but only indirectly through the labels of related photographic resources.
</p>

<p>
  In particular, the photographic resources mention internal chapels, historical figures, artistic objects and heraldic elements. However, these entities are not directly represented as structured RDF relations of the main architectural resource.
</p>

<p>
  For this reason, we proposed a small local vocabulary extension.
</p>

<hr>

<h2>Local namespace</h2>

<p>
  The proposed enrichment uses the following local namespace:
</p>

<pre><code>@prefix ex: &lt;https://example.org/tempio-malatestiano/enrichment/&gt; .
</code></pre>

<p>
  This namespace is used to define new classes, new resources and new properties that are not directly available in the original RDF description.
</p>

<hr>

<h2>New classes</h2>

<p>
  The vocabulary extension introduces three new classes:
</p>

<table>
  <thead>
    <tr>
      <th>Class</th>
      <th>Purpose</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>ex:Chapel</code></td>
      <td>Represents internal chapels as architectural components of Tempio Malatestiano.</td>
    </tr>
    <tr>
      <td><code>ex:ArtisticObject</code></td>
      <td>Represents artistic objects associated with the monument.</td>
    </tr>
    <tr>
      <td><code>ex:HeraldicElement</code></td>
      <td>Represents heraldic or symbolic elements connected to the monument.</td>
    </tr>
  </tbody>
</table>

<h3>RDF representation of the new classes</h3>

<pre><code>@prefix rdfs: &lt;http://www.w3.org/2000/01/rdf-schema#&gt; .
@prefix cdesc: &lt;https://w3id.org/arco/ontology/construction-description/&gt; .
@prefix ex: &lt;https://example.org/tempio-malatestiano/enrichment/&gt; .

ex:Chapel
    a rdfs:Class ;
    rdfs:label "Chapel"@en ;
    rdfs:label "Cappella"@it ;
    rdfs:subClassOf cdesc:ConstructionElement .

ex:ArtisticObject
    a rdfs:Class ;
    rdfs:label "Artistic object"@en ;
    rdfs:label "Oggetto artistico"@it .

ex:HeraldicElement
    a rdfs:Class ;
    rdfs:label "Heraldic element"@en ;
    rdfs:label "Elemento araldico"@it .
</code></pre>

<h3>Explanation</h3>

<p>
  The class <code>ex:Chapel</code> is defined as a subclass of <code>cdesc:ConstructionElement</code> because the internal chapels function as architectural components of Tempio Malatestiano.
</p>

<p>
  The classes <code>ex:ArtisticObject</code> and <code>ex:HeraldicElement</code> were introduced to represent artistic and symbolic entities associated with the monument.
</p>

<hr>

<h2>New resources for architectural components</h2>

<p>
  The first group of new resources represents the internal chapels identified through the labels of photographic resources.
</p>

<table>
  <thead>
    <tr>
      <th>Resource</th>
      <th>Label</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>ex:CappellaDelleVirtu</code></td>
      <td>Cappella delle Virtù / S. Sigismondo</td>
      <td><code>ex:Chapel</code></td>
    </tr>
    <tr>
      <td><code>ex:CappellaDelloZodiaco</code></td>
      <td>Cappella dello Zodiaco</td>
      <td><code>ex:Chapel</code></td>
    </tr>
    <tr>
      <td><code>ex:CappellaDegliAngeli</code></td>
      <td>Cappella degli Angeli</td>
      <td><code>ex:Chapel</code></td>
    </tr>
    <tr>
      <td><code>ex:CappellaDegliAntenati</code></td>
      <td>Cappella degli Antenati</td>
      <td><code>ex:Chapel</code></td>
    </tr>
  </tbody>
</table>

<h3>RDF representation</h3>

<pre><code>@prefix rdfs: &lt;http://www.w3.org/2000/01/rdf-schema#&gt; .
@prefix ex: &lt;https://example.org/tempio-malatestiano/enrichment/&gt; .

ex:CappellaDelleVirtu
    a ex:Chapel ;
    rdfs:label "Cappella delle Virtù / S. Sigismondo"@it ;
    rdfs:label "Chapel of the Virtues / St. Sigismund"@en .

ex:CappellaDelloZodiaco
    a ex:Chapel ;
    rdfs:label "Cappella dello Zodiaco"@it ;
    rdfs:label "Chapel of the Zodiac"@en .

ex:CappellaDegliAngeli
    a ex:Chapel ;
    rdfs:label "Cappella degli Angeli"@it ;
    rdfs:label "Chapel of the Angels"@en .

ex:CappellaDegliAntenati
    a ex:Chapel ;
    rdfs:label "Cappella degli Antenati"@it ;
    rdfs:label "Chapel of the Ancestors"@en .
</code></pre>

<p>
  These resources make explicit the internal architectural components that were repeatedly mentioned in photographic documentation but were not directly modeled as construction elements of the main Tempio Malatestiano resource.
</p>

<hr>

<h2>New resources for historical and artistic entities</h2>

<p>
  The second group of new resources represents historical figures, an artistic object and a heraldic element connected to Tempio Malatestiano.
</p>

<table>
  <thead>
    <tr>
      <th>Resource</th>
      <th>Label</th>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>ex:SigismondoPandolfoMalatesta</code></td>
      <td>Sigismondo Pandolfo Malatesta</td>
      <td><code>foaf:Person</code></td>
    </tr>
    <tr>
      <td><code>ex:IsottaDegliAtti</code></td>
      <td>Isotta degli Atti</td>
      <td><code>foaf:Person</code></td>
    </tr>
    <tr>
      <td><code>ex:CrocifissoGiottesco</code></td>
      <td>Crocifisso giottesco</td>
      <td><code>ex:ArtisticObject</code></td>
    </tr>
    <tr>
      <td><code>ex:StemmaMalatesta</code></td>
      <td>Stemma Malatesta</td>
      <td><code>ex:HeraldicElement</code></td>
    </tr>
  </tbody>
</table>

<h3>RDF representation</h3>

<pre><code>@prefix rdfs: &lt;http://www.w3.org/2000/01/rdf-schema#&gt; .
@prefix foaf: &lt;http://xmlns.com/foaf/0.1/&gt; .
@prefix ex: &lt;https://example.org/tempio-malatestiano/enrichment/&gt; .

ex:SigismondoPandolfoMalatesta
    a foaf:Person ;
    rdfs:label "Sigismondo Pandolfo Malatesta"@it .

ex:IsottaDegliAtti
    a foaf:Person ;
    rdfs:label "Isotta degli Atti"@it .

ex:CrocifissoGiottesco
    a ex:ArtisticObject ;
    rdfs:label "Crocifisso giottesco"@it ;
    rdfs:label "Giottesque Crucifix"@en .

ex:StemmaMalatesta
    a ex:HeraldicElement ;
    rdfs:label "Stemma Malatesta"@it ;
    rdfs:label "Malatesta coat of arms"@en .
</code></pre>

<p>
  The two historical figures are modeled as <code>foaf:Person</code>, while the Crocifisso giottesco and the Malatesta coat of arms are modeled through the proposed classes <code>ex:ArtisticObject</code> and <code>ex:HeraldicElement</code>.
</p>

<hr>

<h2>New properties</h2>

<p>
  The vocabulary extension also introduces three new properties. These properties are used to express historical, artistic and heraldic relations that were not directly available in the original RDF description.
</p>

<table>
  <thead>
    <tr>
      <th>Property</th>
      <th>Meaning</th>
      <th>Range</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>ex:hasAssociatedPerson</code></td>
      <td>Connects a cultural heritage resource to a historical person associated with it.</td>
      <td><code>foaf:Person</code></td>
    </tr>
    <tr>
      <td><code>ex:containsArtisticObject</code></td>
      <td>Connects an architectural heritage resource to an artistic object associated with or contained in it.</td>
      <td><code>ex:ArtisticObject</code></td>
    </tr>
    <tr>
      <td><code>ex:hasHeraldicElement</code></td>
      <td>Connects a cultural heritage resource to a heraldic element associated with it.</td>
      <td><code>ex:HeraldicElement</code></td>
    </tr>
  </tbody>
</table>

<h3>RDF representation</h3>

<pre><code>@prefix rdf: &lt;http://www.w3.org/1999/02/22-rdf-syntax-ns#&gt; .
@prefix rdfs: &lt;http://www.w3.org/2000/01/rdf-schema#&gt; .
@prefix foaf: &lt;http://xmlns.com/foaf/0.1/&gt; .
@prefix arco: &lt;https://w3id.org/arco/ontology/arco/&gt; .
@prefix ex: &lt;https://example.org/tempio-malatestiano/enrichment/&gt; .

ex:hasAssociatedPerson
    a rdf:Property ;
    rdfs:label "has associated person"@en ;
    rdfs:comment "Relates a cultural heritage resource to a historical person associated with it."@en ;
    rdfs:domain arco:ArchitecturalOrLandscapeHeritage ;
    rdfs:range foaf:Person .

ex:containsArtisticObject
    a rdf:Property ;
    rdfs:label "contains artistic object"@en ;
    rdfs:comment "Relates an architectural heritage resource to an artistic object connected to or contained in it."@en ;
    rdfs:domain arco:ArchitecturalOrLandscapeHeritage ;
    rdfs:range ex:ArtisticObject .

ex:hasHeraldicElement
    a rdf:Property ;
    rdfs:label "has heraldic element"@en ;
    rdfs:comment "Relates a cultural heritage resource to a heraldic element associated with it."@en ;
    rdfs:domain arco:ArchitecturalOrLandscapeHeritage ;
    rdfs:range ex:HeraldicElement .
</code></pre>

<hr>

<h2>Why this extension is useful</h2>

<p>
  The proposed vocabulary extension makes the enrichment more precise and understandable.
</p>

<p>
  Instead of adding unnamed or unexplained resources, each new entity is defined with a type and multilingual labels.
</p>

<p>
  The extension also clarifies the difference between architectural components, historical persons, artistic objects and heraldic elements.
</p>

<p>
  This improves the semantic granularity of the knowledge graph and makes the information more searchable, reusable and machine-readable.
</p>

<hr>

<div style="display: flex; justify-content: space-between; margin-top: 2em;">
  <a href="rdf-enrichment.html">Previous</a>
  <a href="challenges.html">Next</a>
</div>
