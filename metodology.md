Methodology

The project follows the methodology of knowledge graph exploration and enrichment.

The main goal was to analyse an existing cultural heritage resource in the ArCo knowledge graph, identify possible information gaps in its RDF description, and propose new RDF triples that could enrich the graph.

The selected resource was Tempio Malatestiano:

https://w3id.org/arco/resource/ArchitecturalOrLandscapeHeritage/0800163046

Methodological Steps

The work was divided into five main steps.

1. Selection of the resource

First, I selected a cultural heritage resource from the ArCo knowledge graph. I chose Tempio Malatestiano because it is a complex architectural monument connected to historical, artistic and symbolic elements.

2. SPARQL exploration

Then, I explored the RDF description of the selected resource through SPARQL queries.

The purpose of this step was to understand:

* which properties are directly associated with the main resource;
* which types and labels are used to describe it;
* which related resources are connected to it;
* whether internal architectural components are explicitly represented;
* whether historical and artistic entities are directly linked to the monument.

3. Identification of information gaps

After the initial exploration, I compared the direct RDF description of the main resource with the information contained in related photographic resources.

This comparison made it possible to identify two main gaps:

1. Internal architectural components, such as chapels, are mentioned in photographic resource labels but are not directly modeled as construction elements of the main architectural resource.
2. Historical figures and artistic elements associated with the monument are also mentioned in photographic resource labels but are not directly represented as structured RDF relations.

4. RDF enrichment

After identifying the gaps, I proposed new RDF triples.

The first group of triples adds internal chapels as construction elements of Tempio Malatestiano.

The second group of triples connects the monument to historical persons, artistic objects and heraldic elements.

5. Vocabulary extension

Since some of the required entities and properties were not available in the original RDF description, I proposed a small vocabulary extension using a local namespace:

@prefix ex: <https://example.org/tempio-malatestiano/enrichment/> .

The vocabulary extension introduces new classes, new resources and new properties to represent the enrichment more precisely.

Tools Used

The main tools used for the project were:

* the ArCo SPARQL endpoint;
* RDF and RDFS vocabularies;
* SPARQL SELECT and CONSTRUCT queries;
* ChatGPT and Gemini for testing LLM-based prompting strategies;
* GitHub Pages for publishing the final project website.

Purpose of the Methodology

The purpose of this methodology was not only to add new triples, but also to show how these triples were identified and justified.

The project therefore combines data exploration, gap analysis, RDF modeling and vocabulary extension.
