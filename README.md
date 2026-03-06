<div style="position:fixed; top:80px; right:20px; background:#1c2330; 
border:1px solid #30363d; border-radius:8px; padding:16px; 
font-size:13px; line-height:2; z-index:999;">
  <strong style="color:#58a6ff;">Contents</strong><br>
  <a href="#motivation" style="color:#8b949e; text-decoration:none;">Motivation</a><br>
  <a href="#why-our-project-is-unique" style="color:#8b949e; text-decoration:none;">Why Unique</a><br>
  <a href="#approach" style="color:#8b949e; text-decoration:none;">Approach</a><br>
  <a href="#results" style="color:#8b949e; text-decoration:none;">Results</a><br>
  <a href="#limitations" style="color:#8b949e; text-decoration:none;">Limitations</a>
</div>



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
Large language models (LLMs) have become commonplace in everyday life. With their versatility in handling information and the sheer volume of content they produce, monitoring output quality has become a critical challenge. LLMs are simultaneously powerful and unreliable — prone to hallucinations, omissions, and factual errors — a contradiction that motivates our work. As a tool is only as useful as our ability to evaluate it, we set out to build a robust LLM judge framework.

Traditional NLP metrics like ROUGE, BLEU, and BERTScore reward surface-level similarity while missing qualities like factual grounding, semantic completeness, and practical usefulness — making them poor proxies for human judgment. This motivates our central goal: an iterative evaluation system that combines LLM-as-judge scoring with human-guided rubrics and task-based NLP metrics. Our primary stakeholders are researchers and educators who need reliable, interpretable evaluations of AI-generated summaries, and developers building LLM pipelines who require scalable quality checks without manual review. We study this through lecture slide summarization — a controllable, academically relevant domain that lets us isolate where evaluation strategies succeed or fail. Our scope is limited to the evaluation framework itself; we do not optimize or fine-tune any summarization model. Performance may vary on highly technical or out-of-distribution lecture content.

# Why our project is unique?

Our pipeline uses a suite of hybrid tools and techniques to power the evaluation. This includes:

Iterative Refinement Loop — Unlike static evaluation tools, our framework continuously re-prompts the LLM with targeted feedback, improving output quality across multiple passes rather than accepting a single response.

Domain-Aware Routing — A dedicated Domain Decision module classifies each input and pulls relevant context from a curated Data Bank, ensuring evaluations are grounded in domain-specific knowledge rather than generic criteria.

Structured Rubric System — Evaluations are anchored to benchmarks and a reference database, making scoring consistent, reproducible, and explainable rather than relying on subjective LLM judgment alone.

Chain of Density Integration — We combine standard evaluation with Chain of Density prompting to progressively refine outputs for information density and semantic completeness — a technique not commonly found in existing judge frameworks.

Piecewise Output Evaluation — Responses are broken into parallel sub-components (Piecewise A/B) and evaluated independently before being merged, catching localized errors that whole-output scoring would miss.

End-to-End Automated Pipeline — From raw LLM output to a final scored result, the entire workflow is automated with no manual intervention required, making it scalable across large evaluation tasks.

# Roadmap 
<iframe 
  src="judge_flowchart.html" 
  width="100%" 
  height="600" 
  style="border:none; border-radius:12px;">
</iframe>

# Methodology
## Dataset
Our dataset consists of lecture slides from multiple UC San Diego courses, spanning data science, biology, and interdisciplinary STEM, provided in PDF format with structured content like bullet points, definitions, and equations. Unlike traditional articles, lecture slides present unique summarization challenges — they are concise, visually structured, and omit transitional language, making automated evaluation non-trivial. We extract text while preserving structural cues like slide boundaries and section headings, which feed directly into our deterministic metrics such as section coverage and glossary recall.

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


# Scope & Limitations

Honest Scope — Our framework evaluates summaries; it does not improve the underlying summarization model. Gains in output quality come entirely from iterative re-prompting within the evaluation loop, not from model fine-tuning.

Known Limitations — LLM-as-judge scoring is sensitive to prompt design and can reflect biases in the judge model. Our domain rubric bank is also bounded by the domains we defined, so performance on out-of-distribution lecture types may degrade.


# Conclusion
