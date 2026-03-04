# Iterative Refinement of LLM as Judge Framework Website
<div class="button-container">
  <a href="#motivation" class="custom-button">Paper</a>
  <a href="#introduction" class="custom-button">Poster</a>
  <a href="#methodology" class="custom-button">Code</a>
  <a href="#results" class="custom-button">Website Code</a>
</div>

<style>
.button-container {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 18px;
  margin: 30px 0;
}

.custom-button {
  padding: 12px 26px;
  background-color: #24292e;
  color: white;
  text-decoration: none;
  border-radius: 10px;
  font-weight: 600;
  letter-spacing: 0.5px;
  transition: all 0.2s ease-in-out;
}

.custom-button:hover {
  background-color: #0366d6;
  transform: translateY(-3px);
}
</style>

# Motivation
Large language models (LLMs) have become commonplace in everday life. With their versatility in handing information and the sheer amount of data that LLMs are capable of producing it has become a struggle to monitor the quality of these amazing tools. LLMs are notorious for both being useful and unreliable a bizarre contradiction that we seek to solve. From hallucinations to ignoring information LLMs have a multitude of quality issues. In order to fix this issue we believe that methods to evaluate LLM outputs must be created, as a tool is only as useful as it's ability to be evaluated. To this end we have created an LLM judge framework.

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
