
# Multilingual Analysis of CHOKE Hallucinations

This repository contains the code and experimental setup for the thesis project **“Multilingual Analysis of CHOKE Hallucinations”**, which investigates hallucination behavior in large language models (LLMs) under a multilingual CHOKE framework.

The experiments evaluate how hallucinations manifest across **English, Turkish, and Malayalam**, using controlled decoding strategies, multilingual embeddings, translation pipelines, and semantic entropy–based sampling.


# Abstract

Large Language Models (LLMs) frequently generate hallucinations that undermine their reliability in knowledge
intensive applications. A particularly concerning subset of these hallucinations is CHOKE (Certain Hallucinations
Overriding Known Evidence), where LLMs produce incorrect responses with high confidence despite possessing
the correct knowledge. While CHOKE has been identified in English only settings, its manifestation across
typologically diverse languages remains unexplored.
This thesis presents a systematic multilingual analysis of CHOKE, examining their prevalence and detectability
across three languages representing different resource levels: English (high-resource), Turkish (medium-resource)
and Malayalam (low-resource). Using an adapted TriviaQA dataset with human verified translations, we
evaluate two LLMs GPT-4o-mini and DeepSeek V3 across two persona based prompt settings designed to induce
hallucinations.
We quantify CHOKE using three certainty metrics: first token probability, probability difference, and semantic
entropy. Our experiments reveal that CHOKE exist across LLMs, with prevalence increasing substantially as
language resource level decreases. In GPT-4o-mini, CHOKE rates are substantially lower in English and rise
sharply in Malayalam, whereas DeepSeek V3 displays an almost universal level of overconfidence, with probability
based CHOKE rates remaining extremely high across all evaluated languages. Semantic entropy emerges as the
most robust and language-agnostic metric for CHOKE detection, maintaining partial discriminative power even
where probability-based metrics fail.
Furthermore, we demonstrate that existing uncertainty-based mitigation strategies are less effective in low
resource languages, with predictive entropy outperforming probability-based approaches on DeepSeek. Our
f
indings indicate that certainty metrics calibrated on English do not transfer reliably to morphologically complex,
low-resource languages, highlighting the need for language specific detection thresholds and culturally aware
evaluation frameworks.



## 📌 Project Overview

The **CHOKE framework** is designed to probe and analyze hallucinations in LLM responses by:

* Partitioning knowledge under controlled decoding
* Querying LLMs with multilingual inputs
* Measuring semantic uncertainty and answer variability
* Comparing hallucination patterns across languages

## 🧪 Experimental Setup

### Large Language Models (LLMs)

* **GPT-4o-mini** (OpenAI, 2024)

  * Accessed via **OpenAI API v1**
* **DeepSeek V3** (DeepSeek AI, 2024)

### Dataset

* **TriviaQA** (Joshi et al., 2017)

### Languages

* English
* Turkish
* Malayalam

### Translation Tools

Used in combination with **human annotation**:

* Google Translate (2026)
* NLLB (No Language Left Behind)
* GPT-4o-mini


## 🔤 Tokenization

* **GPT-4o-mini**

  * `tiktoken`
  * Encoding: `cl100k_base`
* **DeepSeek V3**

  * Hugging Face `AutoTokenizer`
  * Tokenization aligns with native spelling variations accepted by speakers

---

## 🧠 Embedding Models

* **English**

  * `all-MiniLM-L6-v2`
  * Clustering threshold: **0.5**
* **Turkish & Malayalam**

  * `paraphrase-multilingual-MiniLM-L12-v2`

These embeddings are used for semantic similarity, clustering, and entropy estimation.

---

## ⚙️ Model Parameters

### Temperature-Based Decoding

Temperature controls sampling randomness (range: **0–2**):

**Knowledge Partition Phase**

* Greedy generation: `temperature = 0`
* Stochastic sampling: `temperature = 0.5`

**LLM Querying Phase**

* Initial generation: `temperature = 0.1`
* Semantic entropy sampling: `temperature = 1.0`


### Stop Sequences

* Used to terminate generation and enforce minimal answer formats
* Includes:

  * `"`, `.`
  * Programmed stop words

### System Instructions

* High-level instructions guiding LLM behavior across all phases
* Applied consistently throughout the conversational pipeline (see Figure 1 in thesis)


### Other Generation Settings

* **top_logprobs**: `20` (top 20 alternative tokens per output position)
* **Max Tokens**

  * English: `10`
  * Turkish: `20`
  * Malayalam: `50`
    
* **Response Format**

  * Single answer in **JSON** format
## 🔎 String Matching

Used for fuzzy matching of multilingual answers:

* **Malayalam**: RapidFuzz threshold = `0.65`
* **Turkish**: RapidFuzz threshold = `0.85`



## 💻 Programming Environment

* **Python**: 3.10.12
* **Platform**: Google Colab (Free Tier)


## 🔐 LLM Access & Security

* API keys for OpenAI and DeepSeek are stored as **Google Colab Secrets**
* Prevents accidental exposure of credentials in notebooks or logs



## 📦 Key Libraries

```text
json
random
time
logging
sys
os
re
unicodedata
collections
difflib
deepseek
numpy
tqdm
openai
huggingface
transformers
sentence-transformers
scikit-learn
seaborn


## 📬 Contact

For questions or collaboration related to this thesis work, feel free to open an issue or contact me in dhnzchrs@gmail.com
