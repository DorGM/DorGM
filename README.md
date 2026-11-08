# Hi, I'm Dor Meir 👋

**Data Scientist** who takes problems from raw data to models that can be trusted. My work spans **computer vision, recommendation systems and search, AI security, NLP**, and the **pipelines and tools** that make data science reproducible.

**How I work**
- **Frame the question first**, then pick the model.
- **Evaluate so the numbers can be trusted:** leakage-free splits, validation-only model selection, multiple seeds, held-out tests scored once.
- **Report honestly:** what worked, what didn't, and why.
- **Ship clean, tested, reproducible code.**

---

### 👁️ Computer Vision & Deep Learning
| Project | What it shows | Stack |
| --- | --- | --- |
| [**Face Verification**](https://github.com/DorGM/face-verification-metric-learning) | Open-set face verification on people the model never saw. Compares Siamese and triplet CNNs under an identity-disjoint protocol: **0.770 test ROC-AUC** on 336 unseen identities, with false-accept and false-reject trade-offs. | PyTorch, OpenCV |
| [**Neural Network from Scratch**](https://github.com/DorGM/neural-network-from-scratch-mnist) | Backprop and batch norm derived by hand and verified against autograd (about 1e-7). A controlled 12-run ablation isolates batch norm: **95.1% vs 93.8%** MNIST test accuracy, with 6× less seed-to-seed spread. | PyTorch tensors, pytest |
| [**Synthetic Tabular Data with GANs**](https://github.com/DorGM/tabular-data-generation-gan-cgan) | Stress-tests GAN and cGAN census generators with validity gates, real-vs-synthetic detection and train-on-synthetic / test-on-real utility. Shows that plausible-looking rows are still **~100% detectable** and keep only **84%** of real-data utility. | PyTorch, scikit-learn |

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
