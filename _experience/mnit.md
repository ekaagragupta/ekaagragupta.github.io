---

title: AI Research Intern — Malaviya National Institute of Technology (MNIT)

company: MNIT Jaipur

duration: May 2026 – Present

importance: 1

---

**Duration:** May 2026 – July 2026  
**Role:** AI Research Intern  
**Research Domain:** Information Retrieval, Retrieval-Augmented Generation (RAG), Large Language Models (LLMs), Hybrid Search, Explainable AI

---

### Overview

Worked as an AI Research Intern at **Malaviya National Institute of Technology (MNIT), Jaipur**, contributing to the development of a large-scale **Retrieval-Augmented Generation (RAG)** framework for long-document question answering and evidence retrieval.

The internship focused on building a **production-scale retrieval pipeline** capable of efficiently searching hundreds of thousands of document chunks while maintaining low latency, reduced memory footprint, and high retrieval accuracy.

The project involved designing and optimizing every stage of the retrieval pipeline, including document preprocessing, dense retrieval, sparse retrieval, reranking, evidence fusion, metadata management, indexing, benchmarking, and memory optimization.

---

### Research Problem

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

### System Architecture

```
                                                Raw Documents
                                                        │
                                                        ▼
                                                Sentence-aware Chunking
                                                        │
                                                        ▼
                                                Metadata Generation
                                                        │
                                                        ├────────► manifest.csv
                                                        ├────────► retrieval_map.csv
                                                        ├────────► docs.jsonl
                                                        └────────► chunk_text.parquet
                                                        │
                                                        ▼
                                                Embedding Generation
                                                        │
                                                        ▼
                                                Dense Index (HNSW)
                                                        │
                                                Sparse Index (BM25)
                                                        │
                                                        ▼
                                                Hybrid Retrieval
                                                        │
                                                        ▼
                                                Multi-Query Expansion
                                                        │
                                                        ▼
                                                Reciprocal Rank Fusion
                                                        │
                                                        ▼
                                                Dual-stage Reranking
                                                        │
                                                        ▼
                                                Evidence Selection
                                                        │
                                                        ▼
                                                LLM Response Generation
```

---

### Responsibilities

#### 1. Document Preprocessing

Developed a scalable preprocessing pipeline responsible for converting raw corpus documents into optimized retrieval artifacts.

#### Features

- Sentence-aware document chunking
- Sliding-window chunk generation
- Configurable overlap
- Token-aware segmentation
- Chunk metadata generation
- BM25 compatible corpus generation
- Dense retrieval metadata generation

Generated multiple optimized artifacts simultaneously:

- manifest.csv
- retrieval_map.csv
- docs.jsonl
- chunk_text.parquet

---

#### 2. Hybrid Retrieval Pipeline

Implemented a hybrid search framework combining sparse lexical retrieval and dense semantic retrieval.

#### Sparse Retrieval

- BM25 indexing
- Lucene-based search
- Exact keyword matching
- High recall for entity-centric queries

#### Dense Retrieval

- Qwen3-Embedding-4B
- HNSW Approximate Nearest Neighbor Search
- Semantic similarity retrieval
- GPU accelerated embedding inference

---

#### 3. Multi-Query Retrieval

Designed a query expansion mechanism where each user query was expanded into multiple semantically diverse reformulations.

Pipeline:

Original Query

↓

LLM Generated Query Variants

↓

Embedding Generation

↓

Dense Retrieval

↓

Sparse Retrieval

↓

Result Fusion

This significantly improved recall for ambiguous and underspecified queries.

---

## 4. Reciprocal Rank Fusion (RRF)

Implemented Multi-Query Reciprocal Rank Fusion to combine retrieval results obtained from multiple expanded queries.

Advantages:

- Increased retrieval robustness
- Better evidence diversity
- Reduced dependence on a single query formulation
- Higher Recall@K

---

## 5. Dual-stage Reranking

Integrated multiple reranking strategies.

### Qwen Reranker

- Cross-encoder reranking
- Semantic relevance estimation
- Pairwise document scoring

### ColBERT Reranker

- Late interaction retrieval
- Token-level similarity
- High precision ranking

### Ensemble Fusion

Combined multiple rerankers using weighted score aggregation to maximize ranking performance.

---

# Metadata Optimization

One of the primary engineering contributions involved redesigning metadata management across the retrieval pipeline.

Initially, every pipeline stage loaded the complete manifest containing:

- chunk_id
- document_id
- chunk_index
- file_path

Even though each stage required only a subset of these fields.

This resulted in:

- unnecessary RAM consumption
- repeated CSV parsing
- redundant disk I/O
- increased pipeline latency

To address this, designed specialized metadata artifacts during preprocessing.

---

## retrieval_map.csv

Contains only

```
chunk_id
document_id
```

Purpose:

- Retrieval stage
- Lightweight metadata lookup
- Reduced memory usage

---

## docs.jsonl

Generated during preprocessing rather than immediately before BM25 indexing.

Each entry:

```json
{
    "id": "chunk_001",
    "contents": "document chunk text..."
}
```

Benefits

- Eliminated repeated manifest loading
- Removed redundant JSONL generation
- Reduced preprocessing duplication
- Faster BM25 indexing

---

## chunk_text.parquet

Designed a compact lookup table for downstream pipeline stages.

Schema

```
chunk_id
text
```

Purpose

- Reranking
- Generation
- Evidence reconstruction

Advantages

- Columnar storage
- Faster reads
- Better compression
- Lower RAM footprint
- Sequential disk access

---

# Memory Optimization

Refactored preprocessing to generate all retrieval artifacts in a single pass.

Previous workflow

```
Chunking

↓

Manifest

↓

Reload Manifest

↓

Generate JSONL

↓

Reload Manifest

↓

Generate Retrieval Map

↓

Reload Manifest

↓

Generation
```

Optimized workflow

```
Chunking

↓

Generate
    manifest.csv
    retrieval_map.csv
    docs.jsonl
    chunk_text.parquet

↓

Pipeline directly consumes artifacts
```

Benefits

- Eliminated repeated manifest parsing
- Reduced disk I/O
- Lower preprocessing latency
- Reduced memory overhead
- Cleaner pipeline architecture

---

# Indexing Pipeline

Built large-scale retrieval indices.

## Dense

- SentenceTransformer
- Qwen3-Embedding-4B
- HNSW Index

## Sparse

- Lucene BM25

Supported datasets containing tens of thousands of documents and hundreds of thousands of chunks.

---

# Benchmarking

Performed extensive benchmarking across multiple retrieval configurations.

Evaluated

- Dense Retrieval
- Sparse Retrieval
- Hybrid Retrieval
- Multi-Query Retrieval
- Qwen Reranker
- ColBERT
- Ensemble Reranking

Measured

- Retrieval latency
- GPU utilization
- CPU utilization
- Peak RAM usage
- Average RAM usage
- Recall@K
- MRR
- NDCG
- Throughput

---

# Technologies Used

## Languages

- Python

## Deep Learning

- PyTorch
- HuggingFace Transformers
- SentenceTransformers

## Retrieval

- BM25
- Lucene
- HNSW
- FAISS concepts
- Reciprocal Rank Fusion
- ColBERT

## Large Language Models

- Qwen3-Embedding-4B
- Qwen Reranker

## Data Processing

- Pandas
- NumPy
- PyArrow
- Parquet

## Infrastructure

- CUDA
- NVIDIA A10 GPU
- Linux
- Conda
- Bash
- VS Code Remote

---

# Engineering Highlights

- Built an end-to-end production-style Retrieval-Augmented Generation pipeline.
- Engineered hybrid sparse–dense retrieval combining BM25 and semantic embeddings.
- Developed sentence-aware chunking with configurable sliding-window overlap.
- Designed modular metadata artifacts for retrieval, reranking, and generation stages.
- Refactored preprocessing to generate all retrieval resources in a single execution pass.
- Reduced redundant metadata loading and disk I/O by generating retrieval-specific assets during preprocessing.
- Integrated HNSW indexing for scalable approximate nearest neighbor search.
- Implemented multi-query retrieval with Reciprocal Rank Fusion.
- Developed an ensemble reranking framework combining Qwen Cross-Encoder and ColBERT.
- Benchmarked latency, throughput, RAM utilization, GPU utilization, and retrieval quality across multiple retrieval configurations.
- Optimized the pipeline for scalability on GPU-enabled Linux infrastructure.

---

# Skills Demonstrated

- Retrieval-Augmented Generation (RAG)
- Large Language Models (LLMs)
- Information Retrieval
- Hybrid Search
- Dense Retrieval
- Sparse Retrieval
- Cross Encoder Reranking
- HNSW Indexing
- BM25
- Multi-Query Retrieval
- Reciprocal Rank Fusion
- ColBERT
- Memory Optimization
- Pipeline Optimization
- Metadata Engineering
- GPU Computing
- Performance Benchmarking
- Linux Development
- Production AI Systems