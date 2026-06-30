---
layout: page
title: memoRAG
description: A memory-augmented retrieval-augmented generation (RAG) framework that overcomes the core limitations of standard RAG systems when handling long, complex documents.
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

### Repository

The complete implementation is available on
[GitHub](https://github.com/ekaagragupta/mem0RAG).

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



<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>

The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}

```html
<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
```

{% endraw %}
