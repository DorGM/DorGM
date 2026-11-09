# Hi, I'm Dor Meir 👋

**Data Scientist** who takes problems from raw data to models that can be trusted. My research focuses on **collective decision-making with humans and LLM agents**, and my work spans **computer vision, recommendation systems and search, AI security, NLP**, and the **pipelines and tools** that make data science reproducible.

**How I work**
- **Frame the question first**, then pick the model.
- **Evaluate so the numbers can be trusted:** leakage-free splits, validation-only model selection, multiple seeds, held-out tests scored once.
- **Report honestly:** what worked, what didn't, and why.
- **Ship clean, tested, reproducible code.**

---

## 🔬 Featured Research: Learning *How* a Group Should Decide, From Human Crowds to LLM Agent Teams

> **Question:** When a group answers a hard reasoning problem, can a model predict *which aggregation method* will recover the correct answer for that specific group, and how does sharing reasoning (between people or between LLM agents) change decision quality?

**Setting.** Multi-choice reasoning problems with **12 candidate answers and exactly one correct answer**. This extends prior doctoral research on *binary* group decisions to a much richer structure of agreement and disagreement.

### My contributions
| Area | What I did |
| --- | --- |
| **Problem extension** | Generalized the task from binary to **12-option** decisions, adapting preprocessing and every aggregation rule to a richer consensus structure. |
| **Representation** | Extended the CDMCR group-level feature set and added **sub-group features** (inspired by the *inner crowd* idea) that describe the internal structure of each group. |
| **Aggregation-method prediction (AMP)** | Implemented the aggregation methods and trained **XGBoost and deep neural networks** to predict, per group, which method will succeed. |
| **Interaction** | Added an **exposure-and-revision round** for human participants (see others' explanations, then update) and **N deliberation rounds** for agent groups. |
| **LLM agent environment** | Built multi-agent groups mixing LLMs of **different capability levels**, comparing individual work against collaborative work. |

### How AMP works
- **Unit of analysis:** one group answering one problem, at a given round.
- **Raw input per participant:** answer, confidence, perceived difficulty, predicted support for each answer, and a free-text explanation.
- **Features `X`:** CDMCR group descriptors plus the extensions and sub-group features. Sub-groups are used only to describe the group's internal structure; they are not treated as new independent groups.
- **Labels `y` (multi-label):** each aggregator is run on the group's responses and compared with the ground truth. Several methods can be correct at once, or none at all.
- **Inference:** predict a success probability for every aggregator, select the most likely one, and return its answer.

```
y_i  = 1[ f_i(R) = a* ]                    # did aggregator i recover the true answer?
i*   = argmax_i  P̂( y_i = 1 | X )          # pick the aggregator most likely to succeed
answer = f_{i*}(R)
```

Training is **multi-label**. The final decision is a **single aggregator choice**, and the predicted probabilities do not need to sum to 1.

### LLM agent groups: two separate sharing mechanisms
| Mechanism | What is shared | How it advances |
| --- | --- | --- |
| **Between agents in a group** | Each agent's explanation from the previous round | Synchronous rounds: all agents finish a round before the group moves on |
| **Inside a multi-model ensemble** | Outputs and reasoning, including from the current round | Models exchange information to converge on one joint answer |

Sharing is done by passing the explicit outputs and explanations into the context of the next model calls, so each model can weigh the reasoning it received and revise its decision. Only generated explanations are shared, never parameters or internal state.

**Infrastructure:** Google AI Studio · OpenRouter · Groq · OpenAI · Anthropic APIs.

### Status and early finding
- **AMP pipeline:** aggregation methods, features, deliberation rounds, sub-group features and prediction models are implemented and evaluated.
- **Agent experiments:** nearing completion. Individual and collaborative runs have been carried out.
- **Early finding:** in my experiments so far, **groups of weaker models aggregated together outperformed individual work**. The analysis is ongoing, including separating the contribution of aggregation from that of reasoning-sharing.

`Python` `XGBoost` `PyTorch` `Multi-label learning` `Collective intelligence` `Multi-agent LLMs` `Prompt orchestration`

## 📂 Projects

### 👁️ Computer Vision & Deep Learning
| Project | What it shows | Stack |
| --- | --- | --- |
| [**Face Verification**](https://github.com/DorGM/face-verification-metric-learning) | Open-set face verification on people the model never saw. Compares Siamese and triplet CNNs under an identity-disjoint protocol: **0.770 test ROC-AUC** on 336 unseen identities, with false-accept and false-reject trade-offs. | PyTorch, OpenCV |
| [**Neural Network from Scratch**](https://github.com/DorGM/neural-network-from-scratch-mnist) | Backprop and batch norm derived by hand and verified against autograd (about 1e-7). A controlled 12-run ablation isolates batch norm: **95.1% vs 93.8%** MNIST test accuracy, with 6× less seed-to-seed spread. | PyTorch tensors, pytest |
| [**Synthetic Tabular Data with GANs and Diffusion**](https://github.com/DorGM/tabular-data-generation-gan-cgan) | Conditional WGAN-GP, TabDDPM- and TabSyn-style diffusion models and a GAN-diffusion hybrid that generate census rows under domain-rule constraints. On 16,281 unseen real rows: **detection AUC about 0.70** (SDV CTGAN: 0.94), **98%** of real-data utility, zero rule-breaking rows, no copied training rows. | PyTorch, scikit-learn, SDV |

### 🎯 Recommendation Systems & Search
| Project | What it shows | Stack |
| --- | --- | --- |
| [**Cold-Start Recommendation**](https://github.com/DorGM/Cold-Start-Problem---Recommendation-System) | Extends Deezer's KDD'21 semi-personalized cold-start recommender with **fuzzy and soft cluster membership** for new users. Evaluated with Precision, Recall and NDCG@50 on 100k users. | PyTorch, scikit-learn |
| [**Wikipedia Search Engine**](https://github.com/DorGM/wikipedia-search-engine-ir) | A search engine over **6M+ Wikipedia articles**. Spark-built inverted indexes, a BM25 + PageRank + pageviews ranking blend and Word2Vec query expansion, served from GCP. | PySpark, GCP, Flask |
| [**Graph2Books**](https://github.com/DorGM/Book-Network) | Book recommendation from **text-as-graph** representations: word co-occurrence graphs, WL graph embeddings, a k-NN similarity graph and a GCN genre classifier, plus a Streamlit app. | NetworkX, PyG, Streamlit |

### 🔐 AI Security
| Project | What it shows | Stack |
| --- | --- | --- |
| [**Black-Box Attack: improved GFCS**](https://github.com/DorGM/OffensiveAI_Black-Box-Attack_improved-GFCS) | Reimplements the ICLR'22 GFCS surrogate-gradient attack and adds **four query-efficiency variants**. Includes a 34-experiment config framework across ImageNet and CIFAR-10 victim models. | PyTorch |
| [**Vulnerable Skills Detector**](https://github.com/DorGM/Vulnerable-Skills-Detector) | Audits NVIDIA and Cisco AI-agent skill scanners on **735 real skills**: zero native agreement and a ~91% false-positive rate. Deterministic filters raise precision from 13.1% to 17.2% while keeping 96% of true positives. | Python, embeddings, OWASP / MITRE ATLAS |

### 💬 NLP & LLMs
| Project | What it shows | Stack |
| --- | --- | --- |
| [**QA Paraphrase Robustness**](https://github.com/DorGM/qa-paraphrase-robustness) | Separates real QA brittleness from paraphrase meaning drift. A semantic validator (**F1 0.905**) filters 4,016 paraphrases, and meaning-filtered augmentation beats raw augmentation for all three transformer readers. | Transformers, spaCy, CI |
| [**Personal AI Dashboard**](https://github.com/DorGM/personal-ai-dashboard-submission) | An agentic analytics app where the LLM picks read-only tools but **every number is computed and verified by the backend**. About 1,740 tests, mypy --strict clean. | FastAPI, SQLite, OpenAI API |

### 🧰 Data Science Pipelines & Tools
| Project | What it shows | Stack |
| --- | --- | --- |
| [**Titanic Survival Classification**](https://github.com/DorGM/titanic-survival-classification) | A leakage-safe end-to-end workflow: fold-safe preprocessing, feature ablation decided by evidence, a single held-out evaluation (**ROC-AUC 0.84**), saved artifacts and a Streamlit app. | scikit-learn, PyTorch, Streamlit |
| [**Road Accidents Dashboard**](https://github.com/DorGM/Visualization-Project) | An interactive dashboard over **~4,000 Israeli road accidents** that compares severity across lighting, weather, road and time conditions. | Streamlit, Plotly |
| [**Numerical Methods from Scratch**](https://github.com/DorGM/numerical-analysis-algorithms-python) | Core numerical algorithms (TDMA, Regula Falsi, Gaussian quadrature, curve fitting) implemented in NumPy under function-evaluation budgets. | NumPy |

---

**Coming next:** a joint project combining GAN-based data generation with the face-verification pipeline.

**Toolbox:** Python · PyTorch · scikit-learn · Hugging Face · OpenCV · pandas · NumPy · PySpark · GCP · FastAPI · Streamlit · Plotly · pytest · Git
