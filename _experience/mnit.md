---

title: Artifical intelligence Research Intern 

company: Malaviya National Institute of Technology (MNIT)

duration: May 2026 – July 2026

importance: 2

---
**company:** Malaviya National Institute of Technology (MNIT)

**Duration:** May 2026 – July 2026  
**Role:** AI Research Intern  
**Research Domain:** Information Retrieval, Retrieval-Augmented Generation (RAG), Large Language Models (LLMs), Hybrid Search, Explainable AI

---

### Overview

Worked as an AI Research Intern at **Malaviya National Institute of Technology (MNIT), Jaipur**, contributing to the development of a large-scale **Retrieval-Augmented Generation (RAG)** framework for long-document question answering and evidence retrieval.

The internship focused on building a **production-scale retrieval pipeline** capable of efficiently searching hundreds of thousands of document chunks while maintaining low latency, reduced memory footprint, and high retrieval accuracy.
<div class="row justify-content-center mt-4">

  <div class="col-lg-3 col-md-4 col-sm-4">
    {% include figure.liquid
      loading="eager"
      path="assets/img/m1.jpeg"
      class="img-fluid rounded z-depth-1"
    %}
  </div>

  <div class="col-lg-3 col-md-4 col-sm-4">
    {% include figure.liquid
      loading="eager"
      path="assets/img/m4.png"
      class="img-fluid rounded z-depth-1"
    %}
  </div>

  <div class="col-lg-3 col-md-4 col-sm-4">
    {% include figure.liquid
      loading="eager"
      path="assets/img/m6.png"
      class="img-fluid rounded z-depth-1"
    %}
  </div>

</div>


The project involved designing and optimizing every stage of the retrieval pipeline, including document preprocessing, dense retrieval, sparse retrieval, reranking, evidence fusion, metadata management, indexing, benchmarking, and memory optimization.

---


### Research Problem

<div style="float:right; width:260px; margin-left:20px;">

<img src="/assets/img/m3.png" class="img-fluid rounded" style="margin-bottom:15px;">

<img src="/assets/img/m2.jpeg" class="img-fluid rounded" style="margin-bottom:15px;">

<img src="/assets/img/m5.png" class="img-fluid rounded">

</div>

Large Language Models possess limited context windows and cannot directly reason over massive document collections.

Traditional retrieval systems also struggle because:

- Sparse lexical search (BM25) misses semantic matches.
- Dense retrieval may overlook exact keyword matches.
- Long documents exceed transformer context lengths.
- Multiple retrieval stages repeatedly reload metadata into memory.
- Large-scale indexing introduces high RAM overhead and I/O latency.



The objective was to engineer a scalable hybrid retrieval pipeline capable of:

- Retrieving highly relevant evidence
- Reducing GPU and CPU memory usage
- Supporting hundreds of thousands of chunks
- Improving retrieval accuracy
- Optimizing inference latency

---
### Key Contributions

* Developed a scalable document preprocessing pipeline that performs sentence-aware chunking with configurable sliding-window overlap and token-aware segmentation. The pipeline generates all downstream retrieval artifacts—including manifest.csv, retrieval_map.csv, docs.jsonl, and chunk_text.parquet—in a single preprocessing pass, eliminating redundant preprocessing steps.
* Engineered a hybrid retrieval framework by integrating sparse lexical retrieval using Lucene BM25 with dense semantic retrieval using Qwen3-Embedding-4B embeddings indexed through HNSW Approximate Nearest Neighbor Search, enabling both keyword-level precision and semantic search capabilities.
* Implemented a multi-query retrieval strategy where each user query is expanded into multiple semantically diverse reformulations before retrieval. The expanded queries are independently searched across dense and sparse indices, significantly improving recall for ambiguous and underspecified information needs.
* Designed a Multi-Query Reciprocal Rank Fusion (RRF) module to aggregate retrieval results from multiple expanded queries. The fusion strategy improves retrieval robustness, increases evidence diversity, reduces dependence on a single query formulation, and consistently enhances Recall@K.
* Integrated a dual-stage reranking pipeline combining a Qwen Cross-Encoder reranker for semantic relevance estimation and pairwise document scoring with ColBERT’s late-interaction architecture for token-level similarity matching. Final rankings are produced through weighted ensemble fusion to maximize retrieval precision.
* Redesigned metadata management across the retrieval pipeline by replacing repeated loading of the complete manifest.csv with stage-specific metadata artifacts. Introduced a lightweight retrieval_map.csv containing only chunk_id and doc_id, reducing unnecessary RAM consumption, redundant CSV parsing, disk I/O, and overall retrieval latency.
* Optimized the BM25 indexing workflow by generating docs.jsonl directly during preprocessing rather than reconstructing it immediately before indexing. This eliminated repeated manifest loading, reduced preprocessing duplication, and streamlined the sparse indexing pipeline.
* Implemented a compressed chunk_text.parquet lookup store containing chunk identifiers and corresponding text for reranking and generation stages. Leveraging Parquet’s columnar storage format reduced memory footprint, improved read efficiency, and accelerated downstream evidence retrieval.
* Built large-scale retrieval indices using Lucene BM25 for sparse retrieval and SentenceTransformers with Qwen3-Embedding-4B embeddings for dense retrieval over HNSW indices, supporting datasets containing tens of thousands of documents and hundreds of thousands of chunks.


---

## Tech Stack Used

| Category | Technologies |
|----------|--------------|
| **Programming Language** | Python |
| **Deep Learning & AI** | PyTorch, Hugging Face Transformers, SentenceTransformers |
| **Large Language Models (LLMs)** | Qwen3-Embedding-4B, Qwen Reranker |
| **Retrieval & Information Retrieval** | Retrieval-Augmented Generation (RAG), Hybrid Search, Dense Retrieval, Sparse Retrieval, BM25, Lucene, HNSW Indexing, ColBERT, Reciprocal Rank Fusion (RRF), Multi-Query Retrieval, Cross-Encoder Reranking |
| **Data Processing** | Pandas, NumPy, PyArrow, Apache Parquet |
| **Performance Engineering** | Memory Optimization, Metadata Engineering, Pipeline Optimization, Performance Benchmarking, GPU Computing |
| **Infrastructure & Development** | CUDA, NVIDIA A10 GPU, Linux, Conda, Bash, VS Code Remote |
| **Core Expertise** | Production AI Systems, Information Retrieval, Large Language Models (LLMs), Retrieval Pipeline Engineering, Scalable Indexing, Hybrid Retrieval Systems |
