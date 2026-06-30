---
layout: page
title: memoRAG
description: Memory-augmented retrieval-augmented generation (RAG) framework
img: assets/img/tech_case.jpg
importance: 1
category: work
related_publications: true
---

Standard RAG systems retrieve document chunks directly from a query. This works for simple lookups but fails for:

- <strong>Questions requiring global context</strong> :  e.g. "Which year had peak revenue?" when peaks span multiple sections
- <strong>High-level aggregation</strong> : e.g. "How did the pandemic impact the company?" requires synthesizing many passages
- <strong>Open-ended summarization</strong> : summary instructions aren't directly searchable



MemoRAG addresses all three failure modes by using a lightweight memory model to first recall relevant clues and draft candidate answers, then retrieve precise evidence, then generate the final response by first building a compressed global memory of the full context, MemoRAG enables the retriever to be globally aware — generating precise clues and surrogate queries before retrieval, resulting in dramatically more accurate and complete answers.

<div class="row mt-3">
  <div class="col-md-6">
    {% include figure.liquid
      path="assets/img/tech_case.jpg"
      class="img-fluid rounded z-depth-1"
    %}
  </div>

  <div class="col-md-6">
    {% include figure.liquid
      path="assets/img/case.jpg"
      class="img-fluid rounded z-depth-1"
    %}
  </div>
</div>

### Repository

The complete implementation is available on
[GitHub](https://github.com/ekaagragupta/mem0RAG).

#### Core Pipeline
 
---
                  Long Context
                      │
                      ▼
            [Memory Model]  ──── Stores compressed KV-cache of entire context
                     │
                     ├──► recall(query)    → text spans from memory 
                     ├──► rewrite(query)   → surrogate questions
                     └──► answer(query)    → draft answer (optional)
                     │
                     ▼
            [Dense Retriever (FAISS + BGE-M3)]
                     │   Uses clues + surrogate queries + draft answer as retrieval queries
                     ▼
               [Retrieved Evidence Chunks]
                     │
                     ▼
       [Generator LLM]  ──── Produces final answer grounded in evidence

---

## DEMO 

<div class="row justify-content-center">
    <div class="col-sm-10">
        <video controls autoplay muted loop class="img-fluid rounded z-depth-1">
            <source src="/assets/video/demo.mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>
    </div>
</div>

<div class="caption">
    Demo of the memoRAG retrieval pipeline.
</div>

---

## MemoRAG Architecture

MemoRAG is available in three deployment configurations, allowing it to scale from lightweight local inference to large-scale long-context reasoning.


| Stage | Standard RAG | MemoRAG |
|:------|:-------------|:---------|
| **Pipeline** | Query → Retriever → Evidence → LLM → Answer | Query → Memory → Clues & Draft → Retriever → Evidence → LLM → Answer |
| **Retrieval Strategy** | Retrieves passages directly from the user query | Uses memory-generated clues and surrogate queries before retrieval |
| **Global Context** | Limited to retrieved chunks | Maintains compressed document-level memory |
| **Summarization** | Often fails due to lack of a retrieval anchor | Generates key points from memory before retrieval |
| **Complex Multi-hop QA** | Frequently incomplete or hallucinates | More accurate by combining memory and retrieval |
| **Long Document Understanding** | Performance degrades with document length | Designed specifically for long-context reasoning |
| **Repeated Queries** | Re-retrieves information every time | Reuses cached memory for efficient inference |


The full version uses a dedicated long-context memory model (such as Llama 3.1 8B or a custom MemoRAG beacon model) to compress an entire document into a persistent key-value memory cache. This memory enables the system to answer complex questions requiring global document understanding without repeatedly processing the entire input. It is designed for research workloads and achieves the highest retrieval quality on very large documents.


---

### API-backed Agent

Instead of using a locally hosted language model, MemoRAG can also employ external APIs such as OpenAI, Azure OpenAI, or DeepSeek as the generation model.

In this configuration, retrieval and memory remain local while answer generation is delegated to a cloud-hosted LLM, providing higher quality responses without requiring powerful local hardware.

```
from memorag import Agent

agent = Agent(
    model="gpt-4o",
    source="openai",       # "openai" | "azure" | "deepseek"
    api_dict={"api_key": "sk-..."},
    temperature=0.0
)

 Use with MemoRAGLite
from memorag import MemoRAGLite
pipe = MemoRAGLite(customized_gen_model=agent)
```

---

# Memory Formation

Unlike conventional Retrieval-Augmented Generation systems, MemoRAG performs an offline memory construction step before answering any queries.

During this stage the document is processed only once through three sequential operations:

1. **Gist Extraction** – the document is divided into chunks and each chunk is compressed into concise semantic summaries.
2. **KV Cache Construction** – the generated summaries are encoded into a transformer key-value cache, producing a compact long-term memory representation.
3. **Dense Retrieval Indexing** – the original document chunks are embedded using **BGE-M3** and indexed with **FAISS** for efficient semantic retrieval.

This preprocessing enables extremely fast repeated querying without re-encoding the entire document.

After memory construction, MemoRAG stores the generated artifacts as

```
save_dir/
├── memory.bin      # Transformer KV-cache
├── index.bin       # FAISS dense retrieval index
└── chunks.json     # Original document chunks
```

Typical cache sizes are:

| Model | Memory Size |
|-------|-------------|
| MemoRAG (Llama 3.1 8B) | 11–15 GB |
| MemoRAG Lite (Qwen 2.5 1.5B) | ~290 MB |

---

# Retrieval Pipeline

MemoRAG extends traditional dense retrieval by generating richer search queries before retrieval.

Instead of relying solely on the user's question, the retriever combines:

- Memory-recalled text spans
- Surrogate questions generated from memory
- Draft answers predicted by the memory model

These complementary retrieval queries significantly improve recall for questions requiring information distributed across multiple sections of long documents.

---

# Prompting Strategy

MemoRAG uses specialized prompt templates throughout the pipeline, each designed for a specific stage of reasoning.

| Prompt |Key| Purpose |
|---------|---------|---------|
| **Context** |context |Document ingestion |
| **Gist** |gist |Context compression |
| **Span** |span |Recall important passages |
| **Surrogate** | sur |Generate auxiliary retrieval queries |
| **QA** |qa|Direct question answering from memory |
| **Summary** |sum |Generate key points |
| **QA Generation** | qa_gen |Produce the final answer using retrieved evidence |
| **Summary Generation** |sum_gen |Produce the final summary using retrieved evidence |

---