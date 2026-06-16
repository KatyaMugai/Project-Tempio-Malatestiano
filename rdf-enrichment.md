---
layout: default
title: RDF Enrichment
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

<h1>RDF Triples and Proposed Enrichment</h1>

<p>
  This section presents the RDF triples proposed to enrich the representation of <strong>Tempio Malatestiano</strong> in the <strong>ArCo knowledge graph</strong>.
</p>

<p>
  The enrichment is based on the information gaps identified through SPARQL exploration. The analysis showed that some relevant information about the monument is already present in the dataset, but only indirectly through the labels of related photographic resources.
</p>

<p>
  The proposed RDF triples aim to transform this implicit textual information into explicit, structured and machine-readable relations.
</p>

<hr>

<h2>Main resource</h2>

<p>
  The main ArCo resource selected for the project is:
</p>

<pre><code>https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046
  </code></pre>

<p>
  A browsable version of the resource is available here:
</p>

<p>
  <a href="https://dati.beniculturali.it/lodview-arco/resource/ArchitecturalOrLandscapeHeritage/0800163046" target="_blank">
    Tempio Malatestiano in ArCo
  </a>
</p>

<hr>

<h2>Enrichment strategy</h2>

<p>
  The enrichment focuses on two main gaps:
</p>

<ul>
  <li>
    <strong>Gap 1:</strong> internal architectural components are mentioned in photographic resource labels, but they are not directly modeled as construction elements of the main architectural resource.
  </li>
  <li>
    <strong>Gap 2:</strong> historical and artistic entities associated with Tempio Malatestiano are mentioned in photographic resource labels, but they are not directly linked to the main resource through structured RDF properties.
  </li>
</ul>

<p>
  For this reason, we proposed RDF triples that explicitly connect Tempio Malatestiano to internal chapels, associated historical persons, artistic objects and heraldic elements.
</p>

<hr>

<h2>1. Enrichment for Gap 1: Internal architectural components</h2>

<p>
  The first gap concerns the internal architectural structure of Tempio Malatestiano.
</p>

<p>
  The original RDF description directly represents only the facade as a construction element. However, related photographic resources repeatedly mention several internal chapels, such as <strong>Cappella delle Virtù / S. Sigismondo</strong>, <strong>Cappella dello Zodiaco</strong>, <strong>Cappella degli Angeli</strong> and <strong>Cappella degli Antenati</strong>.
</p>

<p>
  To enrich the knowledge graph, we propose adding direct <code>cdesc:hasConstructionElement</code> relations between Tempio Malatestiano and these internal chapels.
</p>

<h3>SPARQL CONSTRUCT query</h3>

<pre><code>PREFIX cdesc: &lt;https://w3id.org/arco/ontology/construction-description/&gt;
PREFIX ex: &lt;https://example.org/tempio-malatestiano/enrichment/&gt;

CONSTRUCT {
  &lt;https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046&gt;
      cdesc:hasConstructionElement ex:CappellaDelleVirtu ;
      cdesc:hasConstructionElement ex:CappellaDelloZodiaco ;
      cdesc:hasConstructionElement ex:CappellaDegliAngeli ;
      cdesc:hasConstructionElement ex:CappellaDegliAntenati .
}
WHERE { }
</code></pre>

<h3>Produced RDF triples</h3>

<pre><code>@prefix cdesc: &lt;https://w3id.org/arco/ontology/construction-description/&gt; .
@prefix ex: &lt;https://example.org/tempio-malatestiano/enrichment/&gt; .

&lt;https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046&gt;
    cdesc:hasConstructionElement ex:CappellaDelleVirtu ;
    cdesc:hasConstructionElement ex:CappellaDelloZodiaco ;
    cdesc:hasConstructionElement ex:CappellaDegliAngeli ;
    cdesc:hasConstructionElement ex:CappellaDegliAntenati .
</code></pre>

<h3>Interpretation</h3>

<p>
  These triples make explicit the internal architectural structure of Tempio Malatestiano.
</p>

<p>
  Instead of leaving the chapels only in textual labels of photographic resources, the proposed enrichment models them as construction elements of the main architectural heritage resource.
</p>

<p>
  This improves the semantic granularity of the knowledge graph and makes the internal chapels directly searchable through SPARQL.
</p>

<hr>

<h2>2. Enrichment for Gap 2: Historical and artistic entities</h2>

<p>
  The second gap concerns historical and artistic entities associated with Tempio Malatestiano.
</p>

<p>
  SPARQL exploration showed that related photographic resources mention several relevant entities, including <strong>Sigismondo Pandolfo Malatesta</strong>, <strong>Isotta degli Atti</strong>, the <strong>Crocifisso giottesco</strong> and the <strong>Stemma Malatesta</strong>.
</p>

<p>
  However, these entities are not directly linked to the main Tempio Malatestiano resource through structured RDF properties.
</p>

<p>
  To enrich the graph, we propose adding explicit relations between the monument and these historical, artistic and heraldic entities.
</p>

<h3>SPARQL CONSTRUCT query</h3>

<pre><code>PREFIX ex: &lt;https://example.org/tempio-malatestiano/enrichment/&gt;

CONSTRUCT {
  &lt;https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046&gt;
      ex:hasAssociatedPerson ex:SigismondoPandolfoMalatesta ;
      ex:hasAssociatedPerson ex:IsottaDegliAtti ;
      ex:containsArtisticObject ex:CrocifissoGiottesco ;
      ex:hasHeraldicElement ex:StemmaMalatesta .
}
WHERE { }
</code></pre>

<h3>Produced RDF triples</h3>

<pre><code>@prefix ex: &lt;https://example.org/tempio-malatestiano/enrichment/&gt; .

&lt;https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046&gt;
    ex:hasAssociatedPerson ex:SigismondoPandolfoMalatesta ;
    ex:hasAssociatedPerson ex:IsottaDegliAtti ;
    ex:containsArtisticObject ex:CrocifissoGiottesco ;
    ex:hasHeraldicElement ex:StemmaMalatesta .
</code></pre>

<h3>Interpretation</h3>

<p>
  These triples make explicit the connection between Tempio Malatestiano and historically or artistically relevant entities.
</p>

<p>
  The properties <code>ex:hasAssociatedPerson</code>, <code>ex:containsArtisticObject</code> and <code>ex:hasHeraldicElement</code> are part of the proposed local vocabulary extension.
</p>

<p>
  This enrichment allows the knowledge graph to represent not only the monument as an architectural object, but also its historical and artistic context.
</p>

<hr>

<h2>3. Full proposed RDF graph</h2>

<p>
  The following Turtle graph combines the proposed enrichment triples with the new resources and vocabulary extension used in the project.
</p>

<pre><code>@prefix rdf: &lt;http://www.w3.org/1999/02/22-rdf-syntax-ns#&gt; .
@prefix rdfs: &lt;http://www.w3.org/2000/01/rdf-schema#&gt; .
@prefix foaf: &lt;http://xmlns.com/foaf/0.1/&gt; .
@prefix arco: &lt;https://w3id.org/arco/ontology/arco/&gt; .
@prefix cdesc: &lt;https://w3id.org/arco/ontology/construction-description/&gt; .
@prefix ex: &lt;https://example.org/tempio-malatestiano/enrichment/&gt; .

&lt;https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046&gt;
    cdesc:hasConstructionElement ex:CappellaDelleVirtu ;
    cdesc:hasConstructionElement ex:CappellaDelloZodiaco ;
    cdesc:hasConstructionElement ex:CappellaDegliAngeli ;
    cdesc:hasConstructionElement ex:CappellaDegliAntenati ;
    ex:hasAssociatedPerson ex:SigismondoPandolfoMalatesta ;
    ex:hasAssociatedPerson ex:IsottaDegliAtti ;
    ex:containsArtisticObject ex:CrocifissoGiottesco ;
    ex:hasHeraldicElement ex:StemmaMalatesta .

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

<h2>Why these triples improve the knowledge graph</h2>

<p>
  The proposed enrichment improves the representation of Tempio Malatestiano in three main ways.
</p>

<ul>
  <li>
    It makes the internal architectural structure of the monument more explicit by representing chapels as construction elements.
  </li>
  <li>
    It makes historical and artistic entities directly queryable through RDF properties.
  </li>
  <li>
    It transforms information that was previously implicit in textual labels into explicit RDF triples.
  </li>
</ul>

<p>
  As a result, the enriched graph would be more precise, more searchable and more reusable for cultural heritage research.
</p>

<hr>

<h2>Example of possible future query</h2>

<p>
  After adding the proposed triples, it would be possible to directly query the internal chapels of Tempio Malatestiano:
</p>

<pre><code>PREFIX cdesc: &lt;https://w3id.org/arco/ontology/construction-description/&gt;
PREFIX rdfs: &lt;http://www.w3.org/2000/01/rdf-schema#&gt;

SELECT ?chapel ?label
WHERE {
  &lt;https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046&gt;
      cdesc:hasConstructionElement ?chapel .

  OPTIONAL { ?chapel rdfs:label ?label . }
}
</code></pre>

<p>
  This kind of query would be more direct and semantically meaningful than searching for chapel names inside photographic resource labels.
</p>

<hr>

<div style="display: flex; justify-content: space-between; margin-top: 2em;">
  <a href="llms.html">Previous</a>
  <a href="vocabulary-extension.html">Next</a>
</div>