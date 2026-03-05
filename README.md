# Iterative Refinement of LLM as Judge Framework Website
<div class="button-container">
  <a href="#motivation" class="custom-button">Paper</a>
  <a href="#introduction" class="custom-button">Poster</a>
  <a href="https://github.com/rahul-sg/HondaResearchLabs_DSC180A-Eval-Systems-Of-NextGen-LLMs" class="custom-button">Code</a>
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
## Dataset
The dataset used in our experiments consists of lecture slides collected from multiple courses at the University of California, San Diego (UCSD). These slides span diverse subject areas, including data science, biology, and interdisciplinary STEM courses, allowing us to evaluate summarization performance across varied technical domains, writing styles, and content structures.

Each lecture is provided in PDF format and contains structured educational content such as section titles, bullet points, definitions, diagrams, equations, and occasionally code snippets. Because lecture slides are typically concise, visually structured, and not written in full prose, they present unique challenges for automated summarization. Unlike traditional articles, slides often omit transitional language, rely heavily on formatting cues, and distribute key concepts across multiple short fragments.

To prepare the data for summarization and evaluation, we extract textual content from the slides while preserving structural cues such as slide boundaries and section headings. These structural elements are later used in our deterministic metrics (e.g., section coverage, glossary recall) to evaluate how well generated summaries capture the core topics of each lecture.

The diversity of subject matter and formatting styles in this dataset allows us to test the robustness, faithfulness, and generalization ability of our LLM-based summarization and evaluation pipeline.

## Pipeline
### 1. Initial Generation

The pipeline begins with an output generated by a primary LLM (e.g., a summarization model). This serves as the candidate summary to be evaluated.

### 2. Judge Module

The core of the system is the Judge, which consists of three major components:

#### (a) Domain Decision Layer

The judge first performs a domain classification step, using the input and a supporting data bank.
This allows the evaluation criteria to adapt based on lecture subject (e.g., biology vs. data science), ensuring rubric relevance.

#### (b) Rubric-Guided Evaluation

The summary is evaluated using:
- Accuracy
- Faithfulness
- Compression
- Extractiveness

These are fed into an Evaluation Pipeline, which produces structured metric outputs before any qualitative scoring occurs.

### 3. Evaluation + Chain of Density

After computing explicit metrics, the system performs:
- Structured rubric scoring (faithfulness prioritized)
- Evidence-based reasoning
- Chain-of-Density refinement (increasing information density without increasing length)

This ensures:
- No guessing of metric values
- Explicit token-level calculations
- Controlled compression with improved coverage

### 4. Iterative Refinement Loop

If weaknesses are detected:
- A new prompt is constructed
- The LLM generates piecewise revisions
- A new output is produced
- The output is re-evaluated by the Judge

This loop continues until quality thresholds are met.

# Results

# Conclusion
