## **Detailed Software Development Checklist for AIM2 Project**

This checklist breaks down each development ticket into granular tasks, emphasizing a Test-Driven Development (TDD) approach where unit tests are developed *before* the corresponding functionality and executed afterwards.

### **I. Core Infrastructure & Utilities**

* **INF-001: Project Setup and Dependency Management**  
- [ ] INF-001-01: **Develop Unit Tests for Environment Setup.** Create a unit test to verify Python version, virtual environment creation, and basic package installation.  
- [ ] INF-001-02: **Create Project Root Directory and Virtual Environment.** Set up the primary project directory and initialize a Python virtual environment.  
- [ ] INF-001-03: **Install Core Dependencies.** Install Owlready2, Biopython, spaCy, NLTK, GitPython, RDKit, langchain, text2term, OntoAligner, NCBI-taxonomist, PyPDF2, pdfminer.six, pyLODE, requests, BeautifulSoup4, pandas, scikit-learn, fuzzywuzzy, rdflib, PyYAML, toml, matplotlib, seaborn.  
- [ ] INF-001-04: **Generate requirements.txt.** Create a requirements.txt file listing all installed dependencies.  
- [ ] INF-001-05: **Execute Unit Tests for Environment Setup.** Run the unit tests developed in INF-001-01 to confirm successful setup.  
* **INF-002: Logging and Error Handling Module**  
- [ ] INF-002-01: **Develop Unit Tests for Logging Configuration.** Create unit tests to verify log file creation, log levels, and message formatting.  
- [ ] INF-002-02: **Create logging\_config.py module.** Define a centralized logging configuration using Python's logging module.  
- [ ] INF-002-03: **Implement Custom Exception Classes.** Define project-specific exception classes (e.g., OntologyError, ExtractionError).  
- [ ] INF-002-04: **Integrate Logging into a Dummy Function.** Add logging statements (info, debug, error) to a sample function.  
- [ ] INF-002-05: **Implement Generic Error Handling Decorator/Utility.** Create a decorator or utility function for consistent error handling.  
- [ ] INF-002-06: **Execute Unit Tests for Logging Configuration.** Run unit tests from INF-002-01.  
* **INF-003: Configuration Management Module**  
- [ ] INF-003-01: **Develop Unit Tests for Config Parsing.** Create unit tests to verify loading, accessing, and handling missing keys in configuration files.  
- [ ] INF-003-02: **Create config\_manager.py module.** Implement functions to load configurations from YAML or TOML files.  
- [ ] INF-003-03: **Define Project Configuration Schema (Initial).** Create an initial config.yaml or config.toml with placeholders for API keys, file paths, etc.  
- [ ] INF-003-04: **Implement Configuration Access Methods.** Add methods to safely retrieve configuration values.  
- [ ] INF-003-05: **Execute Unit Tests for Config Parsing.** Run unit tests from INF-003-01.

### **II. Automated Ontology Development and Management (OD)**

#### **A. Ontology Acquisition and Initial Processing**

* **OD-001: Implement Owlready2 Integration**  
- [ ] OD-001-01: **Develop Unit Tests for Owlready2 Loading.** Create unit tests to verify loading a sample OWL file and accessing basic classes/properties.  
- [ ] OD-001-02: **Create ontology\_loader.py module.** Implement a function load\_ontology(file\_path\_or\_url) that uses Owlready2.World().get\_ontology().load().  
- [ ] OD-001-03: **Test with Local Sample OWL.** Download a small sample OWL file and test the load\_ontology function.  
- [ ] OD-001-04: **Execute Unit Tests for Owlready2 Loading.** Run unit tests from OD-001-01.  
* **OD-002: Chemont/ChEBI Data Acquisition (libChEBIpy)**  
- [ ] OD-002-01: **Develop Unit Tests for libChEBIpy Integration.** Create unit tests to verify ChEBI flat file download, parsing, and retrieval of sample chemical entities.  
- [ ] OD-002-02: **Create chebi\_parser.py module.** Implement a class/function to initialize libChEBIpy and manage local ChEBI flat files.  
- [ ] OD-002-03: **Implement ChEBI Data Extraction.** Write logic to extract relevant Chemont classification data (hierarchy, terms) from ChEBI.  
- [ ] OD-002-04: **Integrate into Owlready2.** Develop a function to convert extracted ChEBI data into Owlready2 classes and properties within a new or existing ontology.  
- [ ] OD-002-05: **Execute Unit Tests for libChEBIpy Integration.** Run unit tests from OD-002-01.  
* **OD-003: NCBI Taxonomy Data Acquisition (NCBI-taxonomist)**  
- [ ] OD-003-01: **Develop Unit Tests for NCBI-taxonomist.** Create unit tests to verify NCBI-taxonomist installation, database setup, and retrieval of taxonomic information for sample species.  
- [ ] OD-003-02: **Create ncbi\_taxonomy\_parser.py module.** Implement a class/function to query NCBI-taxonomist for species and lineage data.  
- [ ] OD-003-03: **Implement NCBI Taxonomy Data Extraction.** Write logic to extract relevant species names, IDs, and hierarchical relationships.  
- [ ] OD-003-04: **Integrate into Owlready2.** Develop a function to convert extracted taxonomy data into Owlready2 classes and is\_a relationships.  
- [ ] OD-003-05: **Execute Unit Tests for NCBI-taxonomist.** Run unit tests from OD-003-01.  
* **OD-004: OLS Ontology Acquisition (PO, PECO, GO, TO)**  
- [ ] OD-004-01: **Develop Unit Tests for OLS Acquisition.** Create unit tests to verify ols-client functionality (e.g., querying for an ontology, checking for direct OWL download URL patterns from OBO Foundry).  
- [ ] OD-004-02: **Create ols\_downloader.py module.** Implement a function download\_ontology\_from\_ols(ontology\_id) that attempts to fetch the OWL file.  
- [ ] OD-004-03: **Handle OLS API vs. Direct OBO Foundry Download.** Prioritize direct OBO Foundry PURL downloads if available (e.g., http://purl.obolibrary.org/obo/po.owl), fallback to ols-client for query-based retrieval and reconstruction if direct OWL download is not exposed via ols-client.  
- [ ] OD-004-04: **Loop through PO, PECO, GO, TO.** Use the downloader to acquire each specified ontology.  
- [ ] OD-004-05: **Load into Owlready2.** Load each downloaded OWL file into the Owlready2 environment.  
- [ ] OD-004-06: **Execute Unit Tests for OLS Acquisition.** Run unit tests from OD-004-01.  
* **OD-005: ChemFont OWL Acquisition**  
- [ ] OD-005-01: **Develop Unit Tests for ChemFont Download.** Create unit tests to verify the programmatic download of the ChemFont OWL file from its expected URL.  
- [ ] OD-005-02: **Create chemfont\_downloader.py module.** Implement a function to download the ChemFont OWL file using requests.  
- [ ] OD-005-03: **Load into Owlready2.** Load the downloaded ChemFont OWL into the Owlready2 environment.  
- [ ] OD-005-04: **Execute Unit Tests for ChemFont Download.** Run unit tests from OD-005-01.  
* **OD-006: NP Classifier JSON to OWL Conversion**  
- [ ] OD-006-01: **Develop Unit Tests for NP Classifier Conversion.** Create unit tests to verify parsing of a sample NP Classifier JSON and the creation of corresponding Owlready2 classes/properties.  
- [ ] OD-006-02: **Acquire Sample NP Classifier JSON.** Obtain a representative JSON file (e.g., from Natural Products Atlas).  
- [ ] OD-006-03: **Create np\_classifier\_converter.py module.** Implement a parser to read the NP Classifier JSON.  
- [ ] OD-006-04: **Programmatically Convert JSON Hierarchy to Owlready2.** Write logic to traverse the JSON and create Owlready2 classes (e.g., family, sub-family, scaffold) and is\_a relationships.  
- [ ] OD-006-05: **Execute Unit Tests for NP Classifier Conversion.** Run unit tests from OD-006-01.  
* **OD-007: Plant Metabolic Network (PMN) BioPAX/OWL Acquisition**  
- [ ] OD-007-01: **Develop Unit Tests for PMN Acquisition.** Create unit tests to verify the loading of a sample BioPAX OWL file (simulated if actual license not available for testing).  
- [ ] OD-007-02: **Create pmn\_loader.py module.** Implement a function to load the PMN biopax.owl file (assuming it's programmatically accessible post-license).  
- [ ] OD-007-03: **Execute Unit Tests for PMN Acquisition.** Run unit tests from OD-007-01.

#### **B. Automated Ontology Trimming and Filtering**

* **OD-008: GOslim Mapping Implementation**  
- [ ] OD-008-01: **Develop Unit Tests for GOslim Mapping.** Create unit tests to verify correct mapping of sample GO terms to their GOslim equivalents using goatools.  
- [ ] OD-008-02: **Create go\_trimmer.py module.** Implement a function to apply goatools.map2slim to the loaded GO ontology.  
- [ ] OD-008-03: **Integrate Trimmed GO into Working Ontology.** Ensure the trimmed GO terms and their hierarchy replace or are marked alongside the full GO hierarchy.  
- [ ] OD-008-04: **Execute Unit Tests for GOslim Mapping.** Run unit tests from OD-008-01.  
* **OD-009: LLM-Driven Semantic Ontology Filtering Module**  
- [ ] OD-009-01: **Develop Unit Tests for LLM Filtering.** Create unit tests with synthetic ontology terms and relevance criteria. Test LLM's ability to identify relevant/irrelevant terms.  
- [ ] OD-009-02: **Create llm\_ontology\_filter.py module.** Implement a function filter\_terms\_by\_relevance(terms, project\_description) that prompts an LLM.  
- [ ] OD-009-03: **Design LLM Prompts for Relevance Scoring.** Craft effective zero-shot/few-shot prompts for LLM to score or categorize terms based on project relevance.  
- [ ] OD-009-04: **Implement LLM API Calls.** Integrate with the generic LLM module (LLM-001, to be defined later) to send prompts and receive responses.  
- [ ] OD-009-05: **Process LLM Output and Apply Filtering.** Parse LLM response (e.g., JSON output) and apply filtering logic to Owlready2 ontology.  
- [ ] OD-009-06: **Execute Unit Tests for LLM Filtering.** Run unit tests from OD-009-01.  
* **OD-010: Rule-Based Ontology Pruning Module**  
- [ ] OD-010-01: **Develop Unit Tests for Rule-Based Pruning.** Create unit tests with sample ontology terms and predefined exclusion rules (e.g., "Exclude any term with 'human' in its label/definition").  
- [ ] OD-010-02: **Create rule\_based\_pruner.py module.** Implement functions to define and apply pruning rules.  
- [ ] OD-010-03: **Define Specific Exclusion Rules.** Programmatically define rules for excluding non-plant species, human traits, or other irrelevant categories.  
- [ ] OD-010-04: **Apply Pruning to Ontology.** Integrate pruning logic to remove or mark irrelevant terms in the Owlready2 ontology.  
- [ ] OD-010-05: **Execute Unit Tests for Rule-Based Pruning.** Run unit tests from OD-010-01.

#### **C. Refined Ontology Scheme Development**

* **OD-011: Define Core Ontology Categories (Structural, Source, Function)**  
- [ ] OD-011-01: **Develop Unit Tests for Category Definition.** Create unit tests to verify the creation of specific OWL classes and their properties.  
- [ ] OD-011-02: **Create aim2\_ontology\_schema.py module.** Implement Python code using Owlready2 to define the top-level World and classes like StructuralAnnotation, Source, Function.  
- [ ] OD-011-03: **Execute Unit Tests for Category Definition.** Run unit tests from OD-011-01.  
* **OD-012: Define Custom Object Properties (is\_a, made\_via, accumulates\_in, affects)**  
- [ ] OD-012-01: **Develop Unit Tests for Property Definition.** Create unit tests to verify the creation of custom ObjectProperty instances with specified domains and ranges.  
- [ ] OD-012-02: **Add Custom Properties to aim2\_ontology\_schema.py.** Define made\_via, accumulates\_in, affects as ObjectProperty classes in Owlready2.  
- [ ] OD-012-03: **Define Property Domains and Ranges.** Specify appropriate domain and range for each custom property (e.g., accumulates\_in domain: Metabolite, range: AnatomicalStructure).  
- [ ] OD-012-04: **Execute Unit Tests for Property Definition.** Run unit tests from OD-012-01.  
* **OD-013: LLM-Assisted Ontology Schema Enrichment**  
- [ ] OD-013-01: **Develop Unit Tests for Schema Enrichment.** Create unit tests with high-level categories and sample terms. Test LLM's ability to suggest relevant sub-categories or properties.  
- [ ] OD-013-02: **Create llm\_schema\_enricher.py module.** Implement a function enrich\_schema(ontology\_elements, llm\_module) that prompts an LLM.  
- [ ] OD-013-03: **Design LLM Prompts for Schema Enrichment.** Craft prompts to guide LLM in suggesting sub-classes or properties based on existing ontology structure and terms from OD-009/OD-010.  
- [ ] OD-013-04: **Process LLM Output and Incorporate Suggestions.** Parse LLM response (e.g., suggested new classes/properties) and add them to the Owlready2 ontology.  
- [ ] OD-013-05: **Execute Unit Tests for Schema Enrichment.** Run unit tests from OD-013-01.  
* **OD-014: Automated Relationship Inference (SWRL/Rule Engine)**  
- [ ] OD-014-01: **Develop Unit Tests for Relationship Inference.** Create unit tests with sample ontology instances and rules. Verify correct inference of new relationships.  
- [ ] OD-014-02: **Create relationship\_inferencer.py module.** Implement functions to define and apply inference rules.  
- [ ] OD-014-03: **Define SWRL Rules (or pyKE rules).** Programmatically define rules (e.g., "if A is\_part\_of B and B accumulates\_in C, then A accumulates\_in C").  
- [ ] OD-014-04: **Integrate Reasoner.** Utilize Owlready2's built-in reasoner or pyKE to apply the defined rules and infer new facts/relationships.  
- [ ] OD-014-05: **Execute Unit Tests for Relationship Inference.** Run unit tests from OD-014-01.

#### **D. Automated Ontology Integration and Alignment**

* **OD-015: Integrate OntoAligner for Ontology Alignment**  
- [ ] OD-015-01: **Develop Unit Tests for OntoAligner Integration.** Create unit tests with small, overlapping sample ontologies. Verify that OntoAligner can propose mappings.  
- [ ] OD-015-02: **Create ontology\_aligner.py module.** Implement functions to load source ontologies and the target AIM2 ontology.  
- [ ] OD-015-03: **Run OntoAligner.** Invoke OntoAligner with appropriate parameters to find correspondences between source and target ontologies.  
- [ ] OD-015-04: **Process Alignment Results.** Parse OntoAligner's output (proposed mappings).  
- [ ] OD-015-05: **Execute Unit Tests for OntoAligner Integration.** Run unit tests from OD-015-01.  
* **OD-016: LLM-Driven Semantic Conflict Resolution**  
- [ ] OD-016-01: **Develop Unit Tests for Conflict Resolution.** Create unit tests with synthetic conflicting terms and their definitions. Test LLM's ability to choose the correct mapping or suggest merging.  
- [ ] OD-016-02: **Create llm\_conflict\_resolver.py module.** Implement a function resolve\_conflict(term1, term2, context, llm\_module) that prompts an LLM.  
- [ ] OD-016-03: **Design LLM Prompts for Conflict Resolution.** Craft prompts to present conflicting terms, their definitions, and a set of options (e.g., merge, keep one, discard).  
- [ ] OD-016-04: **Implement LLM API Calls.** Integrate with LLM-001.  
- [ ] OD-016-05: **Apply Resolution to Ontology.** Update Owlready2 ontology based on LLM's resolution.  
- [ ] OD-016-06: **Execute Unit Tests for Conflict Resolution.** Run unit tests from OD-016-01.  
* **OD-017: Programmatic Ontology Deduplication**  
- [ ] OD-017-01: **Develop Unit Tests for Deduplication.** Create unit tests with an Owlready2 ontology containing known redundant terms (e.g., synonyms, terms mapped to the same canonical ID).  
- [ ] OD-017-02: **Create ontology\_deduplicator.py module.** Implement a function deduplicate\_ontology(ontology) that iterates through terms.  
- [ ] OD-017-03: **Implement Deduplication Logic.** Use identified alignments (from OD-015, OD-016) and Owlready2 functionalities (e.g., All.instances) to merge or redirect redundant terms to a single canonical ID.  
- [ ] OD-017-04: **Execute Unit Tests for Deduplication.** Run unit tests from OD-017-01.  
* **OD-018: Integrate text2term for Post-Extraction Mapping**  
- [ ] OD-018-01: **Develop Unit Tests for text2term Mapping.** Create unit tests with sample free-text strings and a small target ontology subset. Verify correct mapping.  
- [ ] OD-018-02: **Create text\_mapper.py module.** Implement a wrapper for text2term to configure it with the refined AIM2 ontology.  
- [ ] OD-018-03: **Implement Mapping Functionality.** Provide a function map\_text\_to\_ontology(text\_string) that uses text2term to suggest ontology terms.  
- [ ] OD-018-04: **Execute Unit Tests for text2term Mapping.** Run unit tests from OD-018-01.

#### **E. Ontology Storage and Version Control**

* **OD-019: OWL/XML Ontology Export**  
- [ ] OD-019-01: **Develop Unit Tests for OWL Export.** Create unit tests to verify that the Owlready2 ontology can be saved to an OWL/XML file and re-loaded without loss of information.  
- [ ] OD-019-02: **Create ontology\_exporter.py module.** Implement a function export\_ontology\_owl(ontology, file\_path).  
- [ ] OD-019-03: **Execute Unit Tests for OWL Export.** Run unit tests from OD-019-01.  
* **OD-020: Flattened CSV Ontology Export**  
- [ ] OD-020-01: **Develop Unit Tests for CSV Export.** Create unit tests to verify that ontology terms and specified properties can be correctly extracted into a pandas DataFrame and saved as CSV.  
- [ ] OD-020-02: **Add CSV Export Function to ontology\_exporter.py.** Implement export\_ontology\_csv(ontology, file\_path, fields) to flatten relevant ontology data.  
- [ ] OD-020-03: **Define CSV Export Schema.** Determine which properties and relationships should be flattened into the CSV.  
- [ ] OD-020-04: **Execute Unit Tests for CSV Export.** Run unit tests from OD-020-01.  
* **OD-021: Automated GitHub Version Control (GitPython)**  
- [ ] OD-021-01: **Develop Unit Tests for GitPython.** Create unit tests to simulate Git operations (init, add, commit, tag) on a dummy repository.  
- [ ] OD-021-02: **Create git\_manager.py module.** Implement functions for add\_files, commit\_changes, tag\_version.  
- [ ] OD-021-03: **Integrate with Ontology Export.** Call git\_manager functions after OD-019 and OD-020 to automatically commit/tag.  
- [ ] OD-021-04: **Execute Unit Tests for GitPython.** Run unit tests from OD-021-01.  
* **OD-022: Automated Ontology Documentation (pyLODE)**  
- [ ] OD-022-01: **Develop Unit Tests for pyLODE.** Create unit tests to verify that pyLODE can generate an HTML file from a sample OWL ontology.  
- [ ] OD-022-02: **Add Documentation Function to ontology\_exporter.py.** Implement generate\_documentation(ontology\_file, output\_html\_file) using pyLODE.  
- [ ] OD-022-03: **Execute Unit Tests for pyLODE.** Run unit tests from OD-022-01.

### **III. Automated Literature Information Extraction using LLMs (LE)**

#### **A. Comprehensive Corpus Building**

* **LE-001: PubMed/PubMed Central Data Acquisition (Biopython.Bio.Entrez)**  
- [ ] LE-001-01: **Develop Unit Tests for Entrez Query.** Create unit tests to verify successful connection to Entrez, basic search queries, and retrieval of article IDs.  
- [ ] LE-001-02: **Create pubmed\_scraper.py module.** Implement functions for keyword-based search via Bio.Entrez.esearch.  
- [ ] LE-001-03: **Implement Abstract and XML Download.** Add functions to fetch abstracts via Bio.Entrez.efetch and full-text XMLs for PubMed Central articles.  
- [ ] LE-001-04: **Implement Rate Limiting.** Ensure Bio.Entrez usage adheres to NCBI's usage policies.  
- [ ] LE-001-05: **Execute Unit Tests for Entrez Query.** Run unit tests from LE-001-01.  
* **LE-002: Generic Web Scraper for Journal Articles (HTML/PDF)**  
- [ ] LE-002-01: **Develop Unit Tests for Web Scraper.** Create unit tests for basic HTTP requests, HTML parsing, and handling of different status codes.  
- [ ] LE-002-02: **Create web\_scraper.py module.** Implement functions using requests and BeautifulSoup4 to fetch and parse HTML content.  
- [ ] LE-002-03: **Implement Rate Limiting and User-Agent Rotation.** Add logic to handle robots.txt, set delays, and rotate user agents to mitigate bot detection.  
- [ ] LE-002-04: **Identify Target Journal URL Patterns.** Research and define patterns for relevant journal articles to extract content.  
- [ ] LE-002-05: **Implement Headless Browser Support (Optional/If Necessary).** Integrate selenium or playwright for dynamic content if requests is insufficient (headless mode only).  
- [ ] LE-002-06: **Execute Unit Tests for Web Scraper.** Run unit tests from LE-002-01.  
* **LE-003: PDF Text Extraction Module**  
- [ ] LE-003-01: **Develop Unit Tests for PDF Extraction.** Create unit tests with sample PDFs (single-column, multi-column, image-heavy) to verify text extraction accuracy.  
- [ ] LE-003-02: **Create pdf\_extractor.py module.** Implement a function extract\_text\_from\_pdf(pdf\_path) using PyPDF2 or pdfminer.six.  
- [ ] LE-003-03: **Handle Layout Variations.** Add logic to improve text order and readability for common scientific paper layouts.  
- [ ] LE-003-04: **Execute Unit Tests for PDF Extraction.** Run unit tests from LE-003-01.  
* **LE-004: Text Preprocessing and Intelligent Chunking**  
- [ ] LE-004-01: **Develop Unit Tests for Text Preprocessing.** Create unit tests with raw text containing boilerplate, special characters, and verify cleaning.  
- [ ] LE-004-02: **Develop Unit Tests for Chunking.** Create unit tests with long text and verify that it's split into appropriate chunks with desired overlap and context.  
- [ ] LE-004-03: **Create text\_preprocessor.py module.** Implement functions for cleaning (e.g., regex for citations, removing headers/footers).  
- [ ] LE-004-04: **Implement Tokenization and Sentence Segmentation.** Use spaCy or NLTK for linguistic processing.  
- [ ] LE-004-05: **Implement Intelligent Text Chunking.** Use langchain's RecursiveCharacterTextSplitter or similar for context-aware chunking for LLM input.  
- [ ] LE-004-06: **Execute Unit Tests for Text Preprocessing and Chunking.** Run unit tests from LE-004-01 and LE-004-02.

#### **B. Named Entity Recognition (NER) with LLMs**

* **LLM-001: LLM Integration Module (Generic)**  
- [ ] LLM-001-01: **Develop Unit Tests for LLM API Interaction.** Create unit tests to verify connection, basic text generation, and error handling for LLM API calls.  
- [ ] LLM-001-02: **Create llm\_client.py module.** Implement a generic interface for various LLM APIs (e.g., OpenAI, Hugging Face transformers).  
- [ ] LLM-001-03: **Implement API Key Management.** Integrate with INF-003 for secure API key access.  
- [ ] LLM-001-04: **Implement API Rate Limiting and Retry Logic.** Ensure robust API interaction.  
- [ ] LLM-001-05: **Execute Unit Tests for LLM API Interaction.** Run unit tests from LLM-001-01.  
* **LE-005: Ontology-Guided NER Module**  
- [ ] LE-005-01: **Develop Unit Tests for Ontology-Guided NER.** Create unit tests with synthetic text containing entities from the refined ontology and verify correct extraction of specified types.  
- [ ] LE-005-02: **Create ner\_extractor.py module.** Implement a function extract\_entities(text\_chunk, ontology\_terms, llm\_module).  
- [ ] LE-005-03: **Design LLM Prompts for Ontology-Guided NER.** Craft prompts that include instructions on entity types (from OD-017), examples (from LE-006), and output format (e.g., JSON list of entities with type and span).  
- [ ] LE-005-04: **Integrate with LLM-001.** Send prepared prompts to the LLM and receive responses.  
- [ ] LE-005-05: **Parse LLM Output for Entities.** Extract entities from LLM's structured response.  
- [ ] LE-005-06: **Execute Unit Tests for Ontology-Guided NER.** Run unit tests from LE-005-01.  
* **LE-006: Dynamic Few-Shot Example Generation for NER (Synthetic Data)**  
- [ ] LE-006-01: **Develop Unit Tests for Few-Shot Generation.** Create unit tests to verify that generated examples are syntactically correct and contain the intended entities with annotations.  
- [ ] LE-006-02: **Create synthetic\_ner\_data\_generator.py module.** Implement a function generate\_ner\_examples(ontology\_terms, num\_examples\_per\_type, llm\_module).  
- [ ] LE-006-03: **Design LLM Prompts for Synthetic Text Generation.** Prompt LLM to generate sentences based on ontology terms, and then self-annotate these sentences for NER.  
- [ ] LE-006-04: **Automate Example Annotation and Validation.** Implement logic to ensure consistency of generated annotations (e.g., entity spans match generated text).  
- [ ] LE-006-05: **Execute Unit Tests for Few-Shot Generation.** Run unit tests from LE-006-01.  
* **LE-007: Species Normalization Module (Post-NER)**  
- [ ] LE-007-01: **Develop Unit Tests for Species Normalization.** Create unit tests with various common and uncommon species names, verifying their mapping to NCBI TaxIDs.  
- [ ] LE-007-02: **Create species\_normalizer.py module.** Implement a function normalize\_species(species\_name\_list) using NCBI-taxonomist.  
- [ ] LE-007-03: **Implement Plant-Specific Filtering.** Add logic to filter out non-plant species IDs.  
- [ ] LE-007-04: **Execute Unit Tests for Species Normalization.** Run unit tests from LE-007-01.

#### **C. Relationship Extraction with LLMs**

* **SD-001: Synthetic Data Generation for Relationship Extraction**  
- [ ] SD-001-01: **Develop Unit Tests for RE Synthetic Data.** Create unit tests to verify that generated sentences correctly represent target relations (e.g., (compound, affects, trait)).  
- [ ] SD-001-02: **Create synthetic\_re\_data\_generator.py module.** Implement generate\_re\_examples(ontology\_relations, num\_examples\_per\_relation, llm\_module).  
- [ ] SD-001-03: **Define Relation Triplets from Ontology.** Programmatically extract valid subject-predicate-object combinations from the refined ontology (OD-017).  
- [ ] SD-001-04: **Design LLM Prompts for Sentence Generation.** Prompt LLM to create sentences exemplifying these triplets, ensuring diverse linguistic patterns.  
- [ ] SD-001-05: **Automate Quality Control for Synthetic Sentences.** Implement metrics or secondary LLM validation to filter out low-quality or hallucinated sentences.  
- [ ] SD-001-06: **Execute Unit Tests for RE Synthetic Data.** Run unit tests from SD-001-01.  
* **LE-008: LLM-Based Relationship Extraction Module**  
- [ ] LE-008-01: **Develop Unit Tests for Relationship Extraction.** Create unit tests with synthetic text containing known relationships and verify correct extraction of structured triplets.  
- [ ] LE-008-02: **Create re\_extractor.py module.** Implement a function extract\_relationships(text\_chunk, entities\_in\_chunk, llm\_module).  
- [ ] LE-008-03: **Design LLM Prompts for Relationship Extraction.** Craft prompts that provide context, identified entities, and a list of target relationships (from OD-012), asking for structured output.  
- [ ] LE-008-04: **Handle Hierarchical Relationships.** Design prompts to allow for differentiation (e.g., upregulates vs. affects).  
- [ ] LE-008-05: **Parse LLM Output for Relations.** Extract structured relationship triplets from LLM's response.  
- [ ] LE-008-06: **Execute Unit Tests for Relationship Extraction.** Run unit tests from LE-008-01.  
* **LE-009: Automated Relationship Validation (Rule-Based)**  
- [ ] LE-009-01: **Develop Unit Tests for Relationship Validation.** Create unit tests with valid and invalid relationship triplets against ontology rules.  
- [ ] LE-009-02: **Create relationship\_validator.py module.** Implement a function validate\_relationship(subject, predicate, object, ontology\_rules) that checks against ontology domain/range, property restrictions.  
- [ ] LE-009-03: **Define Validation Rules.** Programmatically define rules based on the refined ontology's structure and property definitions (OD-014).  
- [ ] LE-009-04: **Execute Unit Tests for Relationship Validation.** Run unit tests from LE-009-01.  
* **LE-010: LLM Self-Correction for Relationship Extraction**  
- [ ] LE-010-01: **Develop Unit Tests for Self-Correction.** Create unit tests with an initial incorrect extraction, verify the LLM's ability to correct it based on feedback from LE-009.  
- [ ] LE-010-02: **Create llm\_self\_corrector.py module.** Implement a function self\_correct\_extraction(original\_output, validation\_feedback, llm\_module).  
- [ ] LE-010-03: **Design LLM Prompts for Self-Correction.** Craft prompts that provide the LLM's initial output and specific validation errors, asking for revision.  
- [ ] LE-010-04: **Integrate with Validation (LE-009).** If validation fails, trigger the self-correction loop.  
- [ ] LE-010-05: **Execute Unit Tests for Self-Correction.** Run unit tests from LE-010-01.

### **IV. Ontology Mapping and Post-processing (OMP)**

* **OMP-001: Extracted Entity and Relationship Mapping to Ontology**  
- [ ] OMP-001-01: **Develop Unit Tests for Mapping.** Create unit tests with extracted (but unmapped) entities/relations and verify their correct mapping to canonical ontology terms.  
- [ ] OMP-001-02: **Create data\_mapper.py module.** Implement map\_extracted\_to\_ontology(extracted\_data, ontology\_mapper\_module) using OD-018 (text2term).  
- [ ] OMP-001-03: **Handle Unmappable Entities.** Implement a strategy for terms that cannot be mapped (e.g., flag, store in a separate "unmapped" category).  
- [ ] OMP-001-04: **Execute Unit Tests for Mapping.** Run unit tests from OMP-001-01.  
* **OMP-002: Entity Name Normalization Module**  
- [ ] OMP-002-01: **Develop Unit Tests for Normalization.** Create unit tests with various spellings/synonyms of entity names and verify normalization to canonical forms.  
- [ ] OMP-002-02: **Add Normalization Function to data\_mapper.py.** Implement normalize\_entity\_name(entity\_name, ontology\_synonyms) using fuzzy matching.  
- [ ] OMP-002-03: **Utilize Ontology Synonyms.** Leverage Owlready2's hasLabel or hasSynonym properties for robust normalization.  
- [ ] OMP-002-04: **Execute Unit Tests for Normalization.** Run unit tests from OMP-002-01.  
* **OMP-003: Deduplication of Extracted Facts**  
- [ ] OMP-003-01: **Develop Unit Tests for Fact Deduplication.** Create unit tests with lists of extracted facts containing redundancies and verify that duplicates are correctly removed.  
- [ ] OMP-003-02: **Create fact\_deduplicator.py module.** Implement deduplicate\_facts(fact\_list) based on normalized entities and relationships.  
- [ ] OMP-003-03: **Define Deduplication Criteria.** Specify what constitutes a duplicate fact (e.g., same subject, predicate, object, potentially with confidence scores).  
- [ ] OMP-003-04: **Execute Unit Tests for Fact Deduplication.** Run unit tests from OMP-003-01.  
* **OMP-004: Extracted Data Formatting Module**  
- [ ] OMP-004-01: **Develop Unit Tests for Data Formatting.** Create unit tests to verify conversion of processed facts into specified output formats (e.g., RDF triples, CSV, JSON).  
- [ ] OMP-004-02: **Create data\_formatter.py module.** Implement functions like to\_rdf\_triples(), to\_dataframe(), to\_json().  
- [ ] OMP-004-03: **Integrate RDFLib.** For RDF output, use rdflib to construct and serialize triples.  
- [ ] OMP-004-04: **Execute Unit Tests for Data Formatting.** Run unit tests from OMP-004-01.

### **V. Evaluation and Benchmarking (EB)**

* **EB-001: Synthetic Gold Standard Generation for NER/RE**  
- [ ] EB-001-01: **Develop Unit Tests for Gold Standard Generation.** Create unit tests to verify that the generated synthetic gold standard adheres to specified formats and includes diverse examples.  
- [ ] EB-001-02: **Create gold\_standard\_generator.py module.** Implement generate\_synthetic\_gold\_standard(ontology, llm\_module, num\_samples).  
- [ ] EB-001-03: **Utilize SD-001 and LE-006.** Leverage previously developed synthetic data generation for consistent data.  
- [ ] EB-001-04: **Automate Gold Standard Validation.** Implement a programmatic check to ensure the generated gold standard is consistent and properly annotated (e.g., cross-check with a simple rule-based annotator or another LLM for agreement).  
- [ ] EB-001-05: **Execute Unit Tests for Gold Standard Generation.** Run unit tests from EB-001-01.  
* **EB-002: Automated LLM Benchmarking Module**  
- [ ] EB-002-01: **Develop Unit Tests for Benchmarking Metrics.** Create unit tests to verify correct calculation of precision, recall, and F1 scores.  
- [ ] EB-002-02: **Create llm\_benchmarker.py module.** Implement benchmark\_llm\_model(model\_name, gold\_standard, extraction\_module).  
- [ ] EB-002-03: **Integrate with Extraction Modules.** Call LE-005 and LE-008 with different LLM models.  
- [ ] EB-002-04: **Implement Metric Calculation.** Use scikit-learn to compute precision, recall, and F1.  
- [ ] EB-002-05: **Generate Benchmarking Report (Programmatic).** Output results in a structured format (e.g., JSON, CSV).  
- [ ] EB-002-06: **Execute Unit Tests for Benchmarking Metrics.** Run unit tests from EB-002-01.  
* **EB-003: Automated Self-Correction and Verification Framework**  
- [ ] EB-003-01: **Develop Unit Tests for Framework Orchestration.** Create unit tests that simulate an extraction, validation, and correction cycle, ensuring the loop functions correctly.  
- [ ] EB-003-02: **Create auto\_correction\_framework.py module.** Implement an orchestration logic that chains extraction (LE-005, LE-008), validation (LE-007, LE-009), and self-correction (LE-010).  
- [ ] EB-003-03: **Define Correction Thresholds.** Set criteria for when an extraction requires self-correction (e.g., validation score below a certain threshold).  
- [ ] EB-003-04: **Execute Unit Tests for Framework Orchestration.** Run unit tests from EB-003-01.

### **VI. Data Visualization (DV)**

* **DV-001: eFP Browser Data Export Module**  
- [ ] DV-001-01: **Develop Unit Tests for eFP Export.** Create unit tests to verify that data is formatted correctly for eFP browser input (e.g., tab-separated gene expression matrix, annotation files).  
- [ ] DV-001-02: **Create efp\_exporter.py module.** Implement a function export\_for\_efp(metabolite\_data, gene\_expression\_data).  
- [ ] DV-001-03: **Map Metabolite/Gene Data to eFP Format.** Transform OMP-004 output into eFP compatible structures.  
- [ ] DV-001-04: **Execute Unit Tests for eFP Export.** Run unit tests from DV-001-01.  
* **DV-002: PMN Pathway Projection Data Export Module**  
- [ ] DV-002-01: **Develop Unit Tests for Pathway Export.** Create unit tests to verify that extracted metabolite data can be represented in a format suitable for PMN or BioPAX viewers.  
- [ ] DV-002-02: **Create pmn\_exporter.py module.** Implement a function export\_for\_pmn(metabolite\_pathway\_data).  
- [ ] DV-002-03: **Integrate with BioPAX/SBML Libraries (if needed).** If direct BioPAX generation is required (beyond loading in OD-007), use libsbml or a BioPAX Python library.  
- [ ] DV-002-04: **Execute Unit Tests for Pathway Export.** Run unit tests from DV-002-01.

### **VII. Compound Prioritization (CP)**

* **CP-001: Unique Compound Identification Module**  
- [ ] CP-001-01: **Develop Unit Tests for Compound Uniqueness.** Create unit tests with lists of chemical compounds (with varying identifiers) and verify correct identification of unique entries using structural comparison.  
- [ ] CP-001-02: **Create compound\_identifier.py module.** Implement identify\_unique\_compounds(compound\_list).  
- [ ] CP-001-03: **Utilize RDKit for Structural Canonicalization.** Convert chemical names/identifiers to canonical SMILES/InChIKey using RDKit.  
- [ ] CP-001-04: **Implement Similarity-Based Deduplication.** Handle cases where compounds are nearly identical.  
- [ ] CP-001-05: **Execute Unit Tests for Compound Uniqueness.** Run unit tests from CP-001-01.  
* **CP-002: Metabolite Prioritization Module**  
- [ ] CP-002-01: **Develop Unit Tests for Prioritization.** Create unit tests with sample metabolite lists and prioritization criteria, verifying correct ranking.  
- [ ] CP-002-02: **Create metabolite\_prioritizer.py module.** Implement prioritize\_metabolites(unique\_compounds, criteria).  
- [ ] CP-002-03: **Define Prioritization Criteria (Programmatic).** Implement criteria like structural similarity to known compounds (using RDKit), frequency of extraction, connection density in knowledge graph.  
- [ ] CP-002-04: **Implement Ranking Algorithm.** Use scikit-learn or custom ranking logic.  
- [ ] CP-002-05: **Execute Unit Tests for Prioritization.** Run unit tests from CP-002-01.

### **VIII. Database and Tool Integration (DTI)**

* **DTI-001: GNPS/MetaboAnalyst/NP Classifier Data Export Module**  
- [ ] DTI-001-01: **Develop Unit Tests for Tool-Specific Exports.** Create unit tests for each specific format (e.g., GNPS MGF, MetaboAnalyst CSV, NP Classifier JSON for annotation).  
- [ ] DTI-001-02: **Create tool\_exporter.py module.** Implement functions like export\_for\_gnps(data), export\_for\_metaboanalyst(data), export\_for\_np\_classifier(data).  
- [ ] DTI-001-03: **Map Data to Tool-Specific Formats.** Transform OMP-004 output into required formats.  
- [ ] DTI-001-04: **Execute Unit Tests for Tool-Specific Exports.** Run unit tests from DTI-001-01.  
* **DTI-002: General API Interaction Module (External Services)**  
- [ ] DTI-002-01: **Develop Unit Tests for Generic API Calls.** Create unit tests for making parameterized HTTP requests and parsing JSON responses from mock APIs.  
- [ ] DTI-002-02: **Create api\_client.py module.** Implement generic functions for get\_data(url, params), post\_data(url, data).  
- [ ] DTI-002-03: **Integrate with Config Management.** Use INF-003 for base URLs, API keys.  
- [ ] DTI-002-04: **Execute Unit Tests for Generic API Calls.** Run unit tests from DTI-002-01.  
* **DTI-003: Standardized Data Export for New Database**  
- [ ] DTI-003-01: **Develop Unit Tests for Database Export.** Create unit tests to verify that the integrated data can be serialized into OWL, RDF, JSON-LD, and CSV, and that integrity is maintained.  
- [ ] DTI-003-02: **Add Database Export Functions to tool\_exporter.py.** Implement functions like export\_to\_rdf\_database(ontology\_data, extracted\_facts), export\_to\_jsonld\_database().  
- [ ] DTI-003-03: **Utilize RDFLib for RDF/JSON-LD.** Ensure proper serialization of the knowledge graph.  
- [ ] DTI-003-04: **Execute Unit Tests for Database Export.** Run unit tests from DTI-003-01.

---

**Note on LLM Integration:** For all LLM-dependent tasks (OD-009, OD-013, OD-016, LE-005, LE-006, LE-008, LE-010, SD-001, EB-001, EB-002), the specific LLM model (Llama, Gemma, GPT-4o) would be configured via the INF-003 (Configuration Management) ticket, and the LLM-001 (LLM Integration Module) ticket provides the generic interface. The "Develop Unit Tests for LLM..." tasks should focus on testing the *prompting logic* and *output parsing* rather than the LLM's internal reasoning, as the latter is external to the developed code. Simulating LLM responses or using a small, local model for testing can be considered.