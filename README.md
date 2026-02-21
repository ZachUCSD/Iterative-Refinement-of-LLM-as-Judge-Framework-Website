Iterative Refinement of LLM as Judge Framework Website
# Abstract
Large Language Models (LLMs) can produce coherent and informative sum-
maries of complex lecture materials, but evaluating those summaries at scale
raises critical issues. Human review is costly and subjective, while com-
mon automatic metrics (e.g., ROUGE, BLEU, BERTScore) often fail to cap-
ture deeper semantic understanding and factual consistency. To address
this, we developed an evaluation framework that uses GPT-5 both to gen-
erate lecture-slide summaries and to assess them using a rubric paired with
task-based benchmarks, including coverage, faithfulness, organization, clar-
ity, and style. We track performance through dashboards and validate align-
ment with human standards through targeted sanity checks. Building on this
baseline, we are expanding the system to become a more adaptive, reference-
free evaluator. A judge module first pushes each lecture to a domain-aware
rubric drawn from a data bank, enabling evaluation criteria, and even the
number of refinement iterations, to vary based on lecture domain and sum-
mary type. We also integrate a Chain-of-Density refinement stage to produce
more comprehensive and information-dense summaries, and adjust scoring
outputs to better reflect domain-based quality flags across iterations. Overall,
we aim to improve the reliability and scalability of LLM-as-judge evaluation
by combining deterministic benchmarks with domain-adaptive rubrics and
controlled iterative refinement

# Introduction
Large language models (LLMs) are rapidly expanding what is possible in natural language
processing. They can generate fluent text across a wide range of tasks, but as these systems
become more advanced, evaluating their outputs in a way that is systematic, meaningful,
and interpretable becomes increasingly difficult. Traditional NLP metrics such as ROUGE,
BLEU, METEOR, and embedding-based measures like BERTScore can be useful quality indi-
cators, but they often overvalue similarity and fail to capture practical relevance. Important
qualities like factual grounding, semantic completeness, domain-appropriate structure, and
overall usefulness to human readers are not reflected through a calculated score. This mo-
tivates the central goal of our project, which is to build an iterative evaluation system that
combines LLM-as-judge scoring with human-guided rubrics and task-based NLP metrics to
produce a scalable evaluator that aligns closely with human judgment. We study this prob-
lem through lecture slide summarization. Lecture slides are a controllable input, which
makes it possible to compare evaluation strategies consistently and to isolate where differ-
ent methods succeed or fail. It is also a very relevant metric to us as students in academia.
Our objective is not to optimize summarization, but to design an evaluation framework
that can meaningfully assess a wide range of generated outputs. In particular, we focus
on LLM-as-judge evaluation, where an LLM is prompted with a rubric to assess another
model’s summary. This approach is flexible and scalable, but is also sensitive to prompt
design and criteria definition. To make LLM-as-judge evaluation more reliable, we pair
rubric-based judging with task-based checks that provide more deterministic signals, such
as coverage and grounding measures. We also move beyond static rubrics by introducing
domain-aware criteria that reflect what different types of lectures value. Instead of forcing
the same dimensions onto every summary, our evaluator selects from a structured bank of
domain rubrics so that the scoring dimensions and feedback are better aligned with the con-
tent. Finally, we incorporate an iterative refinement process that uses evaluation feedback
to target weaknesses in a summary and improve it across iterations. Together, these com-
ponents aim to support evaluation that is scalable, better grounded in the source material,
and more aligned with human standards across diverse lecture domains.

# Methodology

# Results

# Conclusion
