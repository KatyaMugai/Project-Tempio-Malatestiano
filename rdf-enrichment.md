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
    <strong>Gap 1:</strong> <strong>internal architectural components</strong> are mentioned in photographic resource labels, but they are not directly modeled as construction elements of the main architectural resource.
  </li>
  <li>
    <strong>Gap 2:</strong> <strong>historical and artistic entities</strong> associated with Tempio Malatestiano are mentioned in photographic resource labels, but they are not directly linked to the main resource through structured RDF properties.
  </li>
</ul>

<p>
  For this reason, we proposed RDF triples that explicitly connect Tempio Malatestiano to internal chapels, associated historical persons, artistic objects and heraldic elements.
</p>

<hr>

<h2>1. Enrichment for Gap 1: Internal architectural components</h2>

<p>
  The first gap concerns the internal architectural structure of Tempio Malatestiano. The original RDF description directly represents only the facade as a construction element. However, related photographic resources repeatedly mention several internal chapels, such as <strong>Cappella delle Virtù / S. Sigismondo</strong>, <strong>Cappella dello Zodiaco</strong>, <strong>Cappella degli Angeli</strong> and <strong>Cappella degli Antenati</strong>.
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
  These triples make explicit the internal architectural structure of Tempio Malatestiano. Instead of leaving the chapels only in textual labels of photographic resources, <strong>the proposed enrichment models them as construction elements of the main architectural heritage resource</strong>. This improves the semantic granularity of the knowledge graph and makes the internal chapels directly searchable through SPARQL.
</p>

<hr>

## 2. Enrichment for Gap 2: Historical and artistic entities

The second gap concerns historical and artistic entities associated with Tempio Malatestiano. SPARQL exploration showed that related photographic resources mention several relevant entities, including Sigismondo Pandolfo Malatesta, Isotta degli Atti, the Crocifisso giottesco and the Stemma Malatesta. However, these entities are not directly linked to the main Tempio Malatestiano resource through structured RDF properties.

### Vocabulary reused for Gap 2

<ul>
  <li><code>core:involvesAgent</code>: used to connect Tempio Malatestiano to the historical agents mentioned in the photographic resource labels.</li>
  <li><code>a-dd:hasAssociatedObject</code>: used to connect Tempio Malatestiano to the Crocifisso giottesco as an associated object.</li>
  <li><code>a-dd:hasElementAffixedToCulturalProperty</code>: used to connect Tempio Malatestiano to the Stemma Malatesta as an affixed element of the cultural property.</li>
  <li><code>rdfs:label</code>: used to provide readable labels for the new resources.</li>
  <li><code>rdf:type</code>: used to type the historical figures as agents.</li>
</ul>

### SPARQL CONSTRUCT query

    PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX core: <https://w3id.org/arco/ontology/core/>
    PREFIX a-dd: <https://w3id.org/arco/ontology/denotative-description/>
    PREFIX ex: <https://example.org/tempio-malatestiano/enrichment/>

    CONSTRUCT {
      <https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046>
          core:involvesAgent ex:SigismondoPandolfoMalatesta ;
          core:involvesAgent ex:IsottaDegliAtti ;
          a-dd:hasAssociatedObject ex:CrocifissoGiottesco ;
          a-dd:hasElementAffixedToCulturalProperty ex:StemmaMalatesta .

      ex:SigismondoPandolfoMalatesta
          rdf:type core:Agent ;
          rdfs:label "Sigismondo Pandolfo Malatesta"@it .

      ex:IsottaDegliAtti
          rdf:type core:Agent ;
          rdfs:label "Isotta degli Atti"@it .

      ex:CrocifissoGiottesco
          rdfs:label "Crocifisso giottesco"@it ;
          rdfs:label "Giottesque Crucifix"@en .

      ex:StemmaMalatesta
          rdfs:label "Stemma Malatesta"@it ;
          rdfs:label "Malatesta coat of arms"@en .
    }
    WHERE { }

### Produced RDF triples

    @prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix core: <https://w3id.org/arco/ontology/core/> .
    @prefix a-dd: <https://w3id.org/arco/ontology/denotative-description/> .
    @prefix ex: <https://example.org/tempio-malatestiano/enrichment/> .

    <https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046>
        core:involvesAgent ex:SigismondoPandolfoMalatesta ;
        core:involvesAgent ex:IsottaDegliAtti ;
        a-dd:hasAssociatedObject ex:CrocifissoGiottesco ;
        a-dd:hasElementAffixedToCulturalProperty ex:StemmaMalatesta .

    ex:SigismondoPandolfoMalatesta
        rdf:type core:Agent ;
        rdfs:label "Sigismondo Pandolfo Malatesta"@it .

    ex:IsottaDegliAtti
        rdf:type core:Agent ;
        rdfs:label "Isotta degli Atti"@it .

    ex:CrocifissoGiottesco
        rdfs:label "Crocifisso giottesco"@it ;
        rdfs:label "Giottesque Crucifix"@en .

    ex:StemmaMalatesta
        rdfs:label "Stemma Malatesta"@it ;
        rdfs:label "Malatesta coat of arms"@en .

### Interpretation

These triples make explicit the connection between Tempio Malatestiano and historical or artistic entities that were previously mentioned only in the labels of related photographic resources.
The enrichment does not introduce new local properties for Gap 2. Instead, it reuses existing properties from ArCo Core and ArCo denotative-description.

The historical figures are connected to the monument through <code>core:involvesAgent</code>.

The Crocifisso giottesco is represented through <code>a-dd:hasAssociatedObject</code>, while the Stemma Malatesta is represented through <code>a-dd:hasElementAffixedToCulturalProperty</code>.

The only local resources introduced here are the URIs for the specific entities that were missing as direct structured resources in the original RDF description.

---

<h2>3. Full proposed RDF graph</h2>

<p>
  The following Turtle graph combines the proposed enrichment triples with the new resources and vocabulary extension used in the project.
</p>

<pre><code>@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix core: <https://w3id.org/arco/ontology/core/> .
@prefix cdesc: <https://w3id.org/arco/ontology/construction-description/> .
@prefix a-dd: <https://w3id.org/arco/ontology/denotative-description/> .
@prefix ex: <https://example.org/tempio-malatestiano/enrichment/> .

<https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046>
    cdesc:hasConstructionElement ex:CappellaDelleVirtu ;
    cdesc:hasConstructionElement ex:CappellaDelloZodiaco ;
    cdesc:hasConstructionElement ex:CappellaDegliAngeli ;
    cdesc:hasConstructionElement ex:CappellaDegliAntenati ;
    core:involvesAgent ex:SigismondoPandolfoMalatesta ;
    core:involvesAgent ex:IsottaDegliAtti ;
    a-dd:hasAssociatedObject ex:CrocifissoGiottesco ;
    a-dd:hasElementAffixedToCulturalProperty ex:StemmaMalatesta .

ex:CappellaDelleVirtu
    rdf:type cdesc:ConstructionElement ;
    rdfs:label "Cappella delle Virtù / S. Sigismondo"@it ;
    rdfs:label "Chapel of the Virtues / St. Sigismund"@en .

ex:CappellaDelloZodiaco
    rdf:type cdesc:ConstructionElement ;
    rdfs:label "Cappella dello Zodiaco"@it ;
    rdfs:label "Chapel of the Zodiac"@en .

ex:CappellaDegliAngeli
    rdf:type cdesc:ConstructionElement ;
    rdfs:label "Cappella degli Angeli"@it ;
    rdfs:label "Chapel of the Angels"@en .

ex:CappellaDegliAntenati
    rdf:type cdesc:ConstructionElement ;
    rdfs:label "Cappella degli Antenati"@it ;
    rdfs:label "Chapel of the Ancestors"@en .

ex:SigismondoPandolfoMalatesta
    rdf:type core:Agent ;
    rdfs:label "Sigismondo Pandolfo Malatesta"@it .

ex:IsottaDegliAtti
    rdf:type core:Agent ;
    rdfs:label "Isotta degli Atti"@it .

ex:CrocifissoGiottesco
    rdfs:label "Crocifisso giottesco"@it ;
    rdfs:label "Giottesque Crucifix"@en .

ex:StemmaMalatesta
    rdfs:label "Stemma Malatesta"@it ;
    rdfs:label "Malatesta coat of arms"@en .
</code></pre>

<hr>

<h2>Why these triples improve the knowledge graph?</h2>

<p>
  The proposed enrichment improves the representation of Tempio Malatestiano by transforming information that was previously implicit in textual labels into explicit RDF triples.
</p>

<p>
  In the original RDF description, some relevant information about the monument appeared only indirectly, mainly through the labels of related photographic resources. For example, the labels mentioned internal chapels, historical figures, the Crocifisso giottesco and the Stemma Malatesta. However, these entities were not directly represented as structured relations of the main Tempio Malatestiano resource.
</p>

<p>
  The proposed triples improve the knowledge graph in three main ways.
</p>

<ul>
  <li>
    They make the internal architectural structure of the monument more explicit by representing chapels as construction elements through <code>cdesc:hasConstructionElement</code>.
  </li>
  <li>
    They make historical figures directly queryable by linking them to the monument through the existing ArCo Core property <code>core:involvesAgent</code>.
  </li>
  <li>
    They represent artistic and heraldic entities using existing ArCo denotative-description properties, namely <code>a-dd:hasAssociatedObject</code> and <code>a-dd:hasElementAffixedToCulturalProperty</code>.
  </li>
</ul>

<p>
  The only local resources introduced in the graph are the specific entities that were missing as direct structured resources in the original RDF description, such as the chapels, Sigismondo Pandolfo Malatesta, Isotta degli Atti, the Crocifisso giottesco and the Stemma Malatesta. As a result, the enriched graph becomes more precise, more searchable and more reusable for cultural heritage research.
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
  This query would return the internal chapels proposed in the enrichment, such as the Cappella delle Virtù, the Cappella dello Zodiaco, the Cappella degli Angeli and the Cappella degli Antenati.
</p>

<p>
  It would also be possible to directly query the historical agents associated with the monument:
</p>

<pre><code>PREFIX core: &lt;https://w3id.org/arco/ontology/core/&gt;
PREFIX rdfs: &lt;http://www.w3.org/2000/01/rdf-schema#&gt;

SELECT ?agent ?label
WHERE {
  &lt;https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046&gt;
      core:involvesAgent ?agent .

  OPTIONAL { ?agent rdfs:label ?label . }
}
</code></pre>

<p>
  This query would return historical figures such as Sigismondo Pandolfo Malatesta and Isotta degli Atti as agents involved in the historical and cultural context of Tempio Malatestiano.
</p>

<p>
  It would also be possible to directly query associated objects and affixed elements connected to the monument:
</p>

<pre><code>PREFIX a-dd: &lt;https://w3id.org/arco/ontology/denotative-description/&gt;
PREFIX rdfs: &lt;http://www.w3.org/2000/01/rdf-schema#&gt;

SELECT ?property ?entity ?label
WHERE {
  &lt;https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046&gt;
      ?property ?entity .

  VALUES ?property {
    a-dd:hasAssociatedObject
    a-dd:hasElementAffixedToCulturalProperty
  }

  OPTIONAL { ?entity rdfs:label ?label . }
}
  </code></pre>

<p>
  This query would make it possible to retrieve the Crocifisso giottesco as an associated object and the Stemma Malatesta as an element affixed to the cultural property.
</p>

<p>
  These future queries would be more direct and semantically meaningful than searching for entity names inside photographic resource labels.
</p>

<hr>

<h2>Modelling decision</h2>

<p>
  The enrichment follows a reuse-first modelling strategy.
</p>

<p>
  At the beginning of the project, local properties such as <code>ex:hasAssociatedPerson</code>, <code>ex:containsArtisticObject</code> and <code>ex:hasHeraldicElement</code> were considered. However, after checking the existing ArCo ontology modules thoroughly, we decided not to introduce these custom properties. Instead, the final RDF enrichment reuses existing properties:
</p>

<ul>
  <li><code>cdesc:hasConstructionElement</code> for internal architectural components;</li>
  <li><code>core:involvesAgent</code> for historical agents;</li>
  <li><code>a-dd:hasAssociatedObject</code> for the Crocifisso giottesco;</li>
  <li><code>a-dd:hasElementAffixedToCulturalProperty</code> for the Stemma Malatesta.</li>
</ul>

<p>
  This makes the proposed enrichment less artificial and more consistent with the modelling choices already available in ArCo.
</p>
</hr>

<div style="display: flex; justify-content: space-between; margin-top: 2em;">
  <a href="llms.html">Previous</a>
  <a href="challenges.html">Next</a>
</div>
