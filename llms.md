---
layout: default
title: LLM Prompts
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

<h1>LLM Prompts</h1>

<p>
  Large Language Models were used as supporting tools during the project. The goal was not to replace the SPARQL analysis, but to test whether LLMs could help identify possible enrichment gaps, suggest modelling options and compare different ways of representing implicit information as RDF triples.
</p>

<p>
  Two models were tested:
</p>

<ul>
  <li><a href="https://chat.openai.com/" target="_blank"><strong>ChatGPT</strong></a></li>
 <li><a href="https://gemini.google.com/?hl=it" target="_blank"><strong>Gemini</strong></a></li>
</ul>

<p>
  For each prompting technique, the same prompt was submitted to both models. Their answers were then compared with the evidence obtained through SPARQL queries and with the final modelling decisions used in the project.
</p>

<p>
  Three prompting techniques were used:
</p>

<ul>
  <li>zero-shot prompting;</li>
  <li>chain-of-thought prompting;</li>
  <li>few-shot prompting.</li>
</ul>

<hr>

<h2>1. Zero-shot prompting</h2>

<p>
  The first test used a zero-shot prompt. No SPARQL evidence or RDF modelling context was provided to the models. The aim was to see what architectural components the models would identify from general knowledge about Tempio Malatestiano.
</p>

<h3>Prompt</h3>

<pre><code>What architectural components does Tempio Malatestiano in Rimini have?</code></pre>

<h3>ChatGPT result</h3>

<a href="assets/images/chatgpt1.png" target="_blank">
  Open screenshot of ChatGPT answer
</a>

<p>
  ChatGPT produced a structured answer divided into exterior, interior and unfinished components. It mentioned the marble facade, central entrance arch, semi-columns and pilasters, side arcades, single nave, wooden roof trusses, side chapels, marble balustrades, Gothic arches, sculptural decoration and unfinished upper facade.
</p>

<h3>Gemini result</h3>

<a href="assets/images/gemini1.jpg" target="_blank">
  Open screenshot of Gemini answer
</a>

<p>
  Gemini produced a richer architectural description. It focused on the triumphal arch facade, side facades, aqueduct-style arcades, funerary arcosolia, the high podium, the interior nave and chapels, and unbuilt or unfinished components such as the dome and upper structure.
</p>

<h3>Comparison</h3>

<p>
  Both answers were generally accurate from an architectural and historical point of view. They correctly described Tempio Malatestiano as a Renaissance architectural work designed by Leon Battista Alberti around a pre-existing Gothic Franciscan church.
</p>

<p>
  Gemini gave a more detailed architectural analysis, especially of the facade and side arcades. ChatGPT gave a clearer and more compact list of components, which was easier to connect to the structure of our project.
</p>

<h3>Evaluation</h3>

<p>
  The zero-shot prompt was useful for orientation, but it was not sufficient for gap identification. The answers helped identify possible relevant entities, but the final gaps had to be confirmed through SPARQL queries.
</p>

<hr>

<h2>2. Chain-of-thought prompting</h2>

<p>
  The second test used a chain-of-thought prompt. This time, the models were given the main SPARQL evidence and asked to follow a structured reasoning process from direct RDF data to indirect photographic labels, gap identification and modelling decisions.
</p>

<h3>Prompt</h3>

<pre><code>We are working on a Semantic Web project about knowledge graph enrichment using the ArCo Knowledge Graph.

The selected resource is:

&lt;https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046&gt;

Resource label:
Tempio Malatestiano

Evidence from SPARQL:

1. The direct RDF description of Tempio Malatestiano represents only one construction element: the facade.
2. The labels of related photographic resources mention several internal chapels:
   - Cappella delle Virtù / S. Sigismondo
   - Cappella dello Zodiaco
   - Cappella degli Angeli
   - Cappella degli Antenati
3. The labels of related photographic resources also mention historical and artistic entities:
   - Sigismondo Pandolfo Malatesta
   - Isotta degli Atti
   - Crocifisso giottesco
   - Stemma Malatesta
4. A separate SPARQL query checking whether these historical and artistic entities are directly connected to the main Tempio Malatestiano resource returned no results.

Reason step by step and follow this exact structure:

Step 1 — Analyse what is directly represented in the RDF description.

Step 2 — Analyse what appears only indirectly in photographic resource labels.

Step 3 — Explain whether this difference can be considered a knowledge graph enrichment gap.

Step 4 — Identify the two main gaps:
- internal architectural components;
- historical and artistic entities.

Step 5 — Suggest how these gaps could be enriched with RDF triples.

Step 6 — Decide whether new local properties are necessary or whether existing ontology properties can be reused.

Use the following existing properties if they are suitable:
- cdesc:hasConstructionElement for internal architectural components;
- core:involvesAgent for historical figures;
- a-dd:hasAssociatedObject for artistic objects;
- a-dd:hasElementAffixedToCulturalProperty for heraldic or affixed elements;
- rdfs:label for readable labels.

Step 7 — Give a final conclusion explaining why reusing existing ArCo properties is better than creating a vocabulary extension in this case.

Do not invent new properties unless absolutely necessary.

At the end, provide a short table with:
- entity;
- type of entity;
- suggested existing property;
- reason for choosing this property.</code></pre>

<h3>ChatGPT result</h3>

<a href="assets/images/chatgpt2.png" target="_blank">
  Open screenshot of ChatGPT answer
</a>

<p>
  ChatGPT correctly followed the logic of the prompt. It identified the facade as the only directly represented construction element and explained that the chapels, historical figures, artistic object and heraldic element appeared only indirectly in photographic labels.
</p>

<p>
  It correctly interpreted this situation as a knowledge graph gap: the information is present in the dataset, but not represented as direct structured RDF relations of the main Tempio Malatestiano resource.
</p>

<p>
  The answer was especially useful because it emphasized that labels should be treated as candidate evidence and that enrichment should be verified before being added to a knowledge graph.
</p>

<h3>Gemini result</h3>

<a href="assets/images/gemini2.png" target="_blank">
  Open screenshot of Gemini answer
</a>

<p>
  Gemini also correctly identified the situation as a knowledge graph gap and used the useful idea of moving from “strings” to “things”, meaning from textual labels to RDF resources.
</p>

<p>
  However, Gemini’s answer was more speculative. It proposed several additional ontology classes and properties, such as generic component, patronage and hosted-in relations, which were not part of our final modelling and were not all verified in the ArCo ontology modules used for this project.
</p>

<h3>Comparison</h3>

<p>
  ChatGPT produced the more useful answer for this project. It followed the required reasoning sequence more closely: direct RDF data, indirect photographic labels, gap identification, possible enrichment and verification.
</p>

<p>
  Gemini was useful for brainstorming because it suggested a broader enrichment workflow, including entity extraction and entity linking. However, it introduced more assumptions and moved beyond the evidence provided by the SPARQL queries.
</p>

<h3>Evaluation</h3>

<p>
  The chain-of-thought prompt was effective because it forced the models to follow the project logic. It showed that LLMs can help explain why something is a knowledge graph gap, but their modelling suggestions still need to be checked against the actual ontology.
</p>

<p>
  For this reason, the final RDF model was not taken directly from either answer. It was revised according to SPARQL evidence and existing ArCo properties.
</p>

<hr>

<h2>3. Few-shot prompting</h2>

<p>
  The third test used a few-shot prompt. In this case, the models were given examples of how textual evidence can be transformed into RDF triples. The goal was to test whether the models could generate RDF triples for Tempio Malatestiano while reusing existing ontology properties instead of inventing new local ones.
</p>

<h3>Prompt</h3>

<pre><code>You are helping with a Semantic Web project about cultural heritage knowledge graph enrichment.

Your task is to generate possible RDF triples from textual evidence, using existing ontology properties whenever possible.

Do not invent new properties if suitable existing properties are provided.

Use the following namespaces:

@prefix cdesc: &lt;https://w3id.org/arco/ontology/construction-description/&gt; .
@prefix core: &lt;https://w3id.org/arco/ontology/core/&gt; .
@prefix a-dd: &lt;https://w3id.org/arco/ontology/denotative-description/&gt; .
@prefix rdfs: &lt;http://www.w3.org/2000/01/rdf-schema#&gt; .
@prefix ex: &lt;https://example.org/tempio-malatestiano/enrichment/&gt; .

Example 1:

Evidence:
A church resource has only one direct construction element in its RDF description: the facade. However, the labels of related photographic resources repeatedly mention an internal chapel called “Chapel of Saint Michael”.

Possible RDF enrichment:

&lt;ChurchResource&gt;
    cdesc:hasConstructionElement ex:ChapelOfSaintMichael .

ex:ChapelOfSaintMichael
    a cdesc:ConstructionElement ;
    rdfs:label "Chapel of Saint Michael"@en .

Reason:
The chapel is an internal architectural component. Therefore, it can be represented as a construction element using the existing property cdesc:hasConstructionElement.

Example 2:

Evidence:
A monument has labels of related photographic resources mentioning a historical person and an artistic object. The person is “Giovanni Rossi” and the object is “Painted Crucifix”.

Possible RDF enrichment:

&lt;MonumentResource&gt;
    core:involvesAgent ex:GiovanniRossi ;
    a-dd:hasAssociatedObject ex:PaintedCrucifix .

ex:GiovanniRossi
    a core:Agent ;
    rdfs:label "Giovanni Rossi"@en .

ex:PaintedCrucifix
    rdfs:label "Painted Crucifix"@en .

Reason:
The historical person can be represented through the existing ArCo Core property core:involvesAgent. The artistic object can be represented through the existing ArCo denotative-description property a-dd:hasAssociatedObject.

Now apply the same method to the following case.

Resource:
&lt;https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046&gt;

Resource label:
Tempio Malatestiano

Evidence from SPARQL:
The direct RDF description of Tempio Malatestiano represents only the facade as a construction element. However, the labels of related photographic resources mention several internal chapels:

- Cappella delle Virtù / S. Sigismondo
- Cappella dello Zodiaco
- Cappella degli Angeli
- Cappella degli Antenati

The labels of related photographic resources also mention historical and artistic entities:

- Sigismondo Pandolfo Malatesta
- Isotta degli Atti
- Crocifisso giottesco
- Stemma Malatesta

Use only the following existing properties:

- cdesc:hasConstructionElement for internal architectural components
- core:involvesAgent for historical figures
- a-dd:hasAssociatedObject for artistic objects
- a-dd:hasElementAffixedToCulturalProperty for heraldic or affixed elements
- rdfs:label for readable labels
- rdf:type or a for resource types

Generate RDF triples in Turtle format.

Then briefly explain:
1. Which triples enrich Gap 1.
2. Which triples enrich Gap 2.
3. Why existing ontology properties are sufficient here.
4. Why creating new local properties is not necessary.</code></pre>

<h3>ChatGPT result</h3>

<p>
  ChatGPT generated RDF triples using the expected existing properties. It connected the internal chapels to Tempio Malatestiano through <code>cdesc:hasConstructionElement</code>, historical figures through <code>core:involvesAgent</code>, the Crocifisso giottesco through <code>a-dd:hasAssociatedObject</code> and the Stemma Malatesta through <code>a-dd:hasElementAffixedToCulturalProperty</code>.
</p>

<p>
  It also provided a strong explanation of which triples enrich Gap 1 and Gap 2 and why creating new local properties was not necessary.
</p>

<h3>Gemini result</h3>

<p>
  Gemini also generated RDF triples using the correct existing properties. Its Turtle output was compact, well structured and very close to the final modelling adopted in the project.
</p>

<p>
  It correctly grouped the enrichment into Gap 1, concerning internal architectural components, and Gap 2, concerning historical figures and artistic or heraldic entities.
</p>

<h3>Comparison</h3>

<p>
  In this test, both models performed well because the few-shot prompt gave them clear examples and explicitly limited the allowed properties.
</p>

<p>
  Gemini produced the cleaner RDF output because its Turtle code was concise and close to the final model. ChatGPT produced the stronger explanation because it more clearly described why the triples enrich the two gaps and why vocabulary extension was not needed.
</p>

<h3>Evaluation</h3>

<p>
  The few-shot prompt was the most effective prompting technique. It helped both models follow the required modelling strategy: generating new RDF triples while reusing existing ArCo properties instead of inventing new local properties.
</p>

<p>
  This result confirmed that LLMs can be useful for RDF generation when the prompt includes examples, constraints and a controlled list of ontology properties.
</p>

<hr>

<h2>Overall comparison of the models</h2>

<table>
  <thead>
    <tr>
      <th>Prompting technique</th>
      <th>ChatGPT</th>
      <th>Gemini</th>
      <th>Most useful result</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Zero-shot prompting</td>
      <td>Clearer and more structured list of components.</td>
      <td>More detailed architectural description.</td>
      <td>ChatGPT for project structure; Gemini for architectural detail.</td>
    </tr>
    <tr>
      <td>Chain-of-thought prompting</td>
      <td>Better followed the SPARQL-based reasoning process.</td>
      <td>Useful for brainstorming, but more speculative.</td>
      <td>ChatGPT.</td>
    </tr>
    <tr>
      <td>Few-shot prompting</td>
      <td>Strong explanation of RDF enrichment decisions.</td>
      <td>Cleaner Turtle triples closer to the final RDF model.</td>
      <td>Gemini for RDF output; ChatGPT for explanation.</td>
    </tr>
  </tbody>
</table>

<hr>

<h2>Final evaluation</h2>

<p>
  The comparison showed that both models were useful, but in different ways.
</p>

<p>
  <a href="https://chat.openai.com/" target="_blank"><strong>ChatGPT</strong></a> was generally stronger at explaining the reasoning process and connecting the answers to the project methodology. It was especially useful for understanding why the information found in photographic labels can be considered a knowledge graph gap.
</p>

<p>
  <a href="https://gemini.google.com/?hl=it" target="_blank"><strong>Gemini</strong></a> was stronger in producing compact RDF output when the prompt was highly constrained. However, in less constrained prompts, it tended to introduce additional modelling assumptions that were not directly supported by the SPARQL evidence.
</p>

<p>
  Overall, the LLM outputs were useful as support tools, but the final decisions were based on SPARQL results and on the existing ArCo ontology properties selected for the project:
</p>

<ul>
  <li><code>cdesc:hasConstructionElement</code> for internal architectural components;</li>
  <li><code>core:involvesAgent</code> for historical figures;</li>
  <li><code>a-dd:hasAssociatedObject</code> for the Crocifisso giottesco;</li>
  <li><code>a-dd:hasElementAffixedToCulturalProperty</code> for the Stemma Malatesta.</li>
</ul>

<p>
  The most important conclusion is that LLMs can help generate ideas and possible triples, but their outputs must be verified against the knowledge graph and the ontology. In this project, the final RDF enrichment was not based only on model suggestions, but on the combination of SPARQL evidence, ontology reuse and critical evaluation of the LLM outputs.
</p>

<hr>

<div style="display: flex; justify-content: space-between; margin-top: 2em;">
  <a href="gaps.html">← Previous</a>
  <a href="rdf-enrichment.html">Next →</a>
</div>
