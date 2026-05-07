LLM-as-a-Judge Toxicity Moderation using Gemma 2B
Advanced NLP / LLM Moderation Pipeline

This project implements an LLM-as-a-Judge toxicity moderation system using the instruction-tuned model:

google/gemma-1.1-2b-it

The pipeline performs structured toxicity moderation without fine-tuning and evaluates multiple moderation strategies, uncertainty handling, robustness, and adversarial mitigation.

Features
Prompt-based toxicity moderation
Strict JSON output schema
Abstention / DEFER mechanism
Three moderation mechanisms:
Direct generation
Log-likelihood scoring
Self-consistency voting
Robustness attack evaluation
Adversarial mitigation preprocessing
Coverage-risk analysis
Failure analysis
Latency and throughput measurements
CSV export for reproducibility
Model
Model: google/gemma-1.1-2b-it
Inference: 4-bit NF4 quantization
Framework: Hugging Face Transformers + BitsAndBytes
Hardware: Google Colab T4 GPU
Dataset

Evaluation uses the dataset:

SetFit/toxic_conversations

The dataset is used strictly for evaluation purposes only.

A balanced subset is sampled:

200 toxic comments
200 non-toxic comments

No fine-tuning or additional training is performed.

Moderation Output Format

The system generates strict JSON outputs such as:

{
  "label": "TOXIC",
  "category": "insult",
  "confidence": 0.99,
  "short_rationale": "Direct personal insult."
}

Supported labels:

TOXIC
NON_TOXIC
DEFER
Moderation Mechanisms
A — Direct Generation

Prompt-based moderation using:

structured prompting,
confidence thresholds,
JSON validation,
retry handling.
B — Log-Likelihood Scoring

Computes toxicity using:

token-level log probabilities,
toxic vs non-toxic completion scoring,
confidence-based abstention.
C — Self-Consistency Voting

Uses:

multiple stochastic generations,
majority voting,
agreement-based uncertainty estimation.
Robustness Attacks

The system evaluates robustness against:

typos,
repetition attacks,
spaced toxic words,
leetspeak,
benign quote attacks.

Example:

"You are stupid"
→
"y0u 4r3 s t u p i d"
Mitigation

Normalization preprocessing includes:

leetspeak normalization,
repeated-character cleanup,
deobfuscation,
toxic word reconstruction.
Evaluation Metrics

The project evaluates:

Accuracy
F1-score
Precision
Recall
AUROC
AUPRC
FPR / FNR
Coverage
Risk
JSON validity rate
Latency
Tokens/sec
Coverage–Risk Analysis

The project analyzes the tradeoff between:

prediction coverage,
abstention,
moderation risk.

Higher abstention can reduce unsafe predictions while lowering coverage.

Failure Analysis

Failure analysis examines:

implicit toxicity,
contextual ambiguity,
sarcasm,
quoted toxicity,
adversarial obfuscation,
borderline political language.
Repository Structure
.
├── toxicity_llm_judge.ipynb
├── report.pdf
├── requirements.txt
├── README.md
├── results/
│   ├── metrics_abc.csv
│   ├── robustness_results.csv
│   └── all_results_abc.csv
└── src/
Installation
pip install -r requirements.txt
Running the Notebook

Open:

toxicity_llm_judge.ipynb

and run all cells sequentially.

Recommended environment:

Google Colab
T4 GPU enabled
Example Output
{
  "label": "TOXIC",
  "category": "insult",
  "confidence": 0.99,
  "short_rationale": "Direct personal insult."
}

Authors

Rodia Konstantinidou
Maria Cambouridou
Petros Antoniou

License

MIT License