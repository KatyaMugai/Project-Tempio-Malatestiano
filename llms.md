---
layout: default
title: LLM Prompts
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

## LLM Models

We are working on a project to enrich a cultural heritage knowledge graph using RDF triples. We need to verify whether there is a historical relationship between a spesific person and a monument. Can you answer the final question the same style? 

Q: Is there a historical link between Federico II and the Castello Svevo of Bari? 

A: Yes. The Castello Svevo of Bari was built by Emperor Frederick II in 1233. He turned it into a fortitied castle, and it served as an important part of his defensive system in Southern Italy. 

Q: Did did the napoleon Bonaparte has connection with the Castello Sforzesco in Milan? 

A: Yes, Napoleon Bonaparte had a major, transformative connection to Castello Sforzesco in Milan. During his occupation, his troops used the fortress as barracks, and in 1800, he ordered the destruction of much of its outer fortifications and defensive towers to redesign the area. 
Q: Is there historical relationship between Leon Alberti and the Tample Malatestiano in Rimini?"

---

## Gemini

A: Yes, Leon Battista Alberti had a direct, foundational connection to the Tempio Malatestiano in Rimini. Around 1450, he was commissioned by Sigismondo Pandolfo Malatesta to design the revolutionary white marble exterior façade and lateral arcades, turning the pre-existing Gothic church into a pioneering masterpiece of Renaissance architecture.Would you like me to generate the corresponding RDF triples in Turtle format for this specific relationship, or do you have more historical pairs to verify for your knowledge graph project?

---

## ChatGPT

A: Yes. Leon Battista Alberti had a major architectural connection to the Tempio Malatestiano in Rimini. Around 1450, he designed the Renaissance transformation of the medieval church of San Francesco at the request of Sigismondo Pandolfo Malatesta. Alberti created the classical marble façade and overall architectural scheme, making the Tempio Malatestiano one of the earliest and most influential examples of Renaissance architecture.

First RDF Triple
Depiction Zero-Shot Promt


We are working on a cultural heritage knowledge graph using SPARQL. Generate a SPARQL CONSTRUCKT query and a corresponding RDF  triple in Turtle syntax that links the following agent to a depiction using the foaf:depiction predicate/
•  Subject — main IRI of Tempio Malatestiano, Rimini https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046 
•  Predicate — foaf:depiction 
•  Object - https://upload.wikimedia.org/wikipedia/commons/b/bd/Tempio_malatestiano%2C_esterno_04.JPG> .

Second RDF Triple 
Dating Zero-Shot prompt

We are working on a cultural heritage knowledge graph using SPARQL.
The Tempio Malatestiano in Rimini was build in 1450.  This is the commonly cited year for Leon Battista Alberti’s commission and the start of the major Renaissance transformation (reconstruction of the earlier Gothic Church of San Francesco)
Please write a SPARQL CONSTRUCT query that creates an RDF triple with:

Subject: https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046

Predicate: arco:hasDating

Object: 1450              
First, provide the CONSTRUCT query, then the RDF triple in Turtle syntax. Include all necessary PREFIX declarifications.

Third RDF triple
Let’s think step by step.
1. We are working with RDF triples using the ArCo ontology.
2. We want to indicate that the Tempio Malatestiano was commissioned by the Comune di Rimini.
3. The subject is the Tempio Malatestiano, whose IRI is: https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046

4. The predicate is the ArCo property used to express who commissioned a cultural heritage site:a-cd:hasCommittent
5. The object is the Comune di Rimini, which exists in ArCo with the following IRI:: <https://w3id.org/arco/resource/Agent/d801d3392b7a87fb2af08> 
Now:
First, write a SPARQL CONSTRUCT query to generate this triple.
Then, write the resulting triple in Turtle syntax.
Include all nacessary prefixes.
<img width="928" height="757" alt="image" src="https://github.com/user-attachments/assets/03b7eca3-ae6c-4070-bd6e-8665b2ab8bb7" />
<img width="818" height="617" alt="image" src="https://github.com/user-attachments/assets/cf38f09b-aadf-40aa-9b68-8f476d121f59" />

Sixth RDF Triple
Cultural Events – Zero-Shot Prompt
We are working with the ArCo and CIS ontologies and need to represent that a cultural property is involved in a cultural event.
Please generate:
a SPARQL CONSTRUCT query
and the corresponding RDF triple in Turtle syntax
Subject: <https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800242914>
Predicate: cis:isInvolvedInCulturalEvent
Object: <https://w3id.org/arco/resource/Event/eve-s56-rsef18b>
Make sure to use the correct prefixes and return only the CONSTRUCT query and the Turtle triple
<img width="755" height="733" alt="image" src="https://github.com/user-attachments/assets/87db07bd-db46-4de5-97be-aef97ab181c7" />

<img width="786" height="717" alt="image" src="https://github.com/user-attachments/assets/4fa4c5e2-d29e-4cb8-b67e-99995562a3e2" />


---

<div style="display: flex; justify-content: space-between; margin-top: 2em;">
  <a href="gaps.html">← Previous</a>
  <a href="rdf-enrichment.html">Next →</a>
</div>
