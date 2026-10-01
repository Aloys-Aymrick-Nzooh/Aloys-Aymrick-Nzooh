<h1 align="center">Hi, I'm Aloys 👋</h1>

<p align="center">
  <b>AI Scientist · Data Science & AI (MSc, Aivancity) · Paris area</b><br/>
  Machine Learning, Deep Learning, Agentic RAG, knowledge graphs, and sovereign / local LLM deployment
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/aloys-aymrick-nzooh/"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"/></a>
  <a href="mailto:nzoohaymrick@gmail.com"><img src="https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"/></a>
  <a href="https://aymrick.netlify.app/"><img src="https://img.shields.io/badge/Portfolio-000000?style=for-the-badge&logo=vercel&logoColor=white" alt="Portfolio"/></a>
</p>

---

## About

I build AI systems that have to work on real, messy data: machine learning models,multi-agent orchestration, retrieval over knowledge graphs, and structured extraction from documents. Two years in industry as an AI Scientist at **ZENETYS**, previously at **SOCOTEC** (NLP / document processing) and **PitchBoy** (conversational AI for VR-based training).

My research interest is making retrieval-augmented generation verifiable: evidence selection with formal objectives, entailment checks before propagation, and ontology-grounded retrieval instead of vector similarity alone. I also care about local, open-weight LLM deployment for regulated environments.

- 🎓 Master's thesis (Aivancity, 2025): agentic multi-source RAG with ontology-grounded retrieval (OGRAG), reaching **94.8% NL-to-SPARQL success on a network RDF graph**
- 📖 Co-author of a book chapter published by **IGI Global**
- 🔬 Independent research: **RAA**, currently being finalized as a paper
- 🇫🇷 French (native) · 🇬🇧 English

---

## Selected work

### 🔬 RAA — Request Assertion Alignment *(research, paper in progress)*
Multi-hop RAG architecture that decomposes a question into the facets the answer must cover, selects evidence to cover them, and verifies each claim before it can influence downstream reasoning.

**Pipeline (v2)**
1. **Facet decomposition**: the request is broken into assertions/facets that must be supported to answer it
2. **Retrieval**: candidates are retrieved from the corpus (FAISS index, all-MiniLM embeddings)
3. **Submodular evidence selection**: a greedy selection maximizes **facet coverage** under a budget, so redundant passages are penalized (diminishing returns)
4. **Dependency-gated LLM invocation**: a hop is only sent to the LLM (Claude API) once the hops it depends on are resolved, which avoids calls on unanswerable or premature sub-questions
5. **Verify-before-propagate NLI gate**: each intermediate assertion is checked by natural language inference against its evidence; only entailed assertions are propagated to later hops
6. **Final answer** composed from verified assertions only

**Why a redesign:** v1 optimized a proxy that diverged from the actual target (proxy–target gap). v2 reformulates the objective so selection optimizes what the evaluation measures.

**Evaluation:** HotpotQA (distractor), 2WikiMultiHopQA, MuSiQue; BEIR/SciFact for open-domain.
`Python` `FAISS` `all-MiniLM` `NLI` `Claude API`

### 🕸️ Ontology-grounded agentic RAG *(Master's thesis)*
Agentic multi-source RAG where retrieval is grounded in an ontology. Natural-language questions in French are translated to SPARQL over a temporal network knowledge graph in GraphDB.
`RDF` `SPARQL` `GraphDB` `LLM agents`

### ⚖️ Legal Chatbot — GraphRAG
Legal assistant that answers questions over a corpus of legal texts using a knowledge graph instead of flat vector retrieval, so answers can draw on relationships between entities, provisions and concepts.

**Indexing pipeline (offline)**
1. **Ingest & chunk** legal documents into text units
2. **Extract entities and relations** with an LLM to build a knowledge graph
3. **Detect communities** (hierarchical clustering) and generate a summary per community
4. **Embed** text units, entities and community reports, and store the vectors in **LanceDB**

**Query pipeline (online)**
1. **FastAPI** receives the user question
2. **Retrieval**: *local search* (entity-centric: neighbors, relations, source chunks) for specific questions, *global search* (community summaries) for broad, corpus-level questions
3. **Generation**: the LLM answers from the retrieved context only
4. **PostgreSQL** stores conversation state and metadata (verify exact usage)

**Engineering notes**
- Built on GraphRAG 2.7.0; most of the work went into reconciling its internal API changes with LanceDB's vector format requirements
- Documented in a formal technical write-up and a blog evaluation of the system (link here if public)

`GraphRAG` `LanceDB` `FastAPI` `PostgreSQL`

### 🍽️ DISHVIEW *(in development)*
Restaurant discovery platform with visual, dish-level interactive menus. Mobile app (client + restaurateur) and web admin; NestJS API with a separate Python/FastAPI AI service (menu OCR/vision ingestion, semantic search).
`NestJS` `FastAPI` `pgvector`

### 👁️ Computer vision
PCB defect detection (YOLO + SAM) and automated veterinary VHS measurement from DICOM images.

> Industrial work at ZENETYS (multi-agent orchestration with LangGraph + Ollama, operational intelligence platform with real-time machine-health classification and agentic root-cause analysis) is proprietary, so there's no public repo.

---

## Tech stack

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![NestJS](https://img.shields.io/badge/NestJS-E0234E?style=flat-square&logo=nestjs&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)
![Neo4j](https://img.shields.io/badge/Neo4j-4581C3?style=flat-square&logo=neo4j&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![LaTeX](https://img.shields.io/badge/LaTeX-008080?style=flat-square&logo=latex&logoColor=white)

---

## Machine learning & AI concepts

| Domain | Concepts I work with |
|---|---|
| **Classical ML** | Supervised / unsupervised learning, feature engineering, bias-variance trade-off, regularization, cross-validation, ensemble methods (random forest, gradient boosting), metric selection (precision/recall/F1, ROC-AUC) |
| **Deep learning** | Transformers and attention, embeddings, fine-tuning vs. prompting vs. RAG trade-offs, CNN-based object detection and segmentation (YOLO, SAM) |
| **NLP** | Information extraction, NER, document processing, natural language inference (NLI), multilingual (FR/EN) pipelines, NL-to-SPARQL translation |
| **Retrieval & RAG** | Dense retrieval, multi-hop retrieval, GraphRAG, ontology-grounded retrieval, evidence selection, hallucination mitigation through verification |
| **Optimization** | Submodular maximization (facet coverage), confidence scoring, objective design (proxy vs. target alignment) |
| **Knowledge representation** | Ontologies, RDF/OWL, property graphs, SPARQL / Cypher, temporal knowledge graphs |
| **Agents** | Multi-agent orchestration, tool calling, state management, human-in-the-loop routing |
| **Evaluation** | RAGAS-style metrics (faithfulness, answer relevance, context precision/recall), multi-hop QA benchmarks (HotpotQA, 2WikiMultiHopQA, MuSiQue, BEIR) |
| **MLOps & deployment** | Local / on-prem LLM serving (Ollama, open-weight models), service isolation (Python AI service behind an API), monitoring, governance (EU AI Act, DORA, BCBS 239 awareness) |
| **Research tooling** | Jupyter, LaTeX, Pydantic |

---

## Currently

- Finalizing the RAA paper (formal proofs, hyperparameter justification)
- Building DISHVIEW
- Exploring local / sovereign LLM deployment for regulated sectors



<p align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=Aloys-Aymrick-Nzooh&show_icons=true&hide_border=true" height="150"/>
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=Aloys-Aymrick-Nzooh&layout=compact&hide_border=true" height="150"/>
</p>

