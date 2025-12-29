*Speech and Language Processing* (3rd Edition draft) by Jurafsky and Martin

### Table 1: Foundations of Text Processing & Basic Classifiers
This section covers the fundamental tools for processing text and early probabilistic models.

| Chapter | Topic | Key Concepts | Core Algorithms / Metrics |
| :--- | :--- | :--- | :--- |
| **2** | **Text Normalization** | • **Regular Expressions:** Pattern matching tools.<br>• **Tokenization:** Splitting text into words/subwords (BPE).<br>• **Normalization:** Case folding, lemmatization, stemming (Porter). | • **Minimum Edit Distance:** Calculating similarity between strings (Levenshtein distance) using dynamic programming. |
| **3** | **N-gram Language Models** | • **Language Modeling:** Assigning probabilities to sequences of words.<br>• **Markov Assumption:** Probability depends only on recent history.<br>• **Sparsity:** Handling unseen n-grams (zeros). | • **Perplexity:** Evaluation metric for LMs.<br>• **Smoothing:** Laplace (Add-1), Kneser-Ney, Interpolation, Backoff. |
| **4** | **Naive Bayes** | • **Text Classification:** Assigning labels (e.g., Sentiment Analysis).<br>• **Bag of Words:** Ignoring word order.<br>• **Generative Models:** Modeling how data is generated. | • **Multinomial Naive Bayes:** Probabilistic classifier based on Bayes' rule and independence assumptions.<br>• **Precision/Recall/F-measure:** Evaluation metrics. |
| **5** | **Logistic Regression** | • **Discriminative Models:** Directly computing $P(y \mid x)$.<br>• **Feature Representation:** Weights and biases.<br>• **Regularization:** Preventing overfitting (L1, L2). | • **Sigmoid Function:** Squashing output to [0,1].<br>• **Cross-Entropy Loss:** The cost function to minimize.<br>• **Gradient Descent:** Optimization algorithm. |

### Table 2: Neural Networks & Representation Learning
This section covers modern deep learning architectures and how meaning is represented numerically.

| Chapter | Topic | Key Concepts | Core Algorithms / Models |
| :--- | :--- | :--- | :--- |
| **6** | **Vector Semantics** | • **Distributional Hypothesis:** Words with similar contexts have similar meanings.<br>• **Sparse vs. Dense Vectors:** Term-document matrices vs. Embeddings.<br>• **Analogy:** $King - Man + Woman = Queen$. | • **TF-IDF:** Weighing terms by frequency and inverse document frequency.<br>• **PPMI:** Positive Pointwise Mutual Information.<br>• **Word2Vec (Skip-gram):** Learning dense embeddings.<br>• **Cosine Similarity:** Measuring vector closeness. |
| **7** | **Neural Networks** | • **Units:** Computational blocks taking weighted sums.<br>• **Activation Functions:** Sigmoid, Tanh, ReLU.<br>• **Feedforward Networks:** Multilayer Perceptrons (MLPs). | • **Backpropagation:** Computing gradients for training.<br>• **Neural Language Models:** Predicting words without smoothing issues. |
| **9** | **Sequence Architectures** | • **Recurrent Neural Networks (RNNs):** Handling variable-length sequences via temporal cycles.<br>• **Gating:** Managing context/memory over time.<br>• **Self-Attention:** Comparing an item to all other items in a sequence. | • **LSTMs & GRUs:** Architectures to solve vanishing gradients.<br>• **Transformers:** Parallelizable architecture relying entirely on self-attention mechanisms.<br>• **Autoregressive Generation:** Generating text one token at a time. |
| **10** | **Contextual Embeddings** | *(Note: Text placeholder in PDF, but concept referenced elsewhere)* Dynamic representations where embeddings change based on context. | • **BERT / ELMo:** Context-dependent word representations. |

### Table 3: Syntax and Parsing
This section covers the structural analysis of sentences.

| Chapter | Topic | Key Concepts | Core Algorithms / Models |
| :--- | :--- | :--- | :--- |
| **8** | **Sequence Labeling** | • **POS Tagging:** Assigning parts of speech.<br>• **NER:** Named Entity Recognition (BIO tagging).<br>• **HMM vs. CRF:** Generative vs. Discriminative sequence models. | • **Viterbi Algorithm:** Dynamic programming for decoding the best tag sequence.<br>• **Forward-Backward:** Algorithm for training. |
| **12** | **Constituency Grammars** | • **Context-Free Grammars (CFG):** Rules describing hierarchical structure (NP, VP).<br>• **Treebanks:** Corpora of parsed sentences (e.g., Penn Treebank). | • **Chomsky Normal Form (CNF):** Binary branching standard for grammars. |
| **13** | **Constituency Parsing** | • **Structural Ambiguity:** Attachment and coordination issues.<br>• **Span-based Parsing:** Scoring constituents using neural classifiers. | • **CKY Algorithm:** Bottom-up dynamic programming parser.<br>• **PARSEVAL:** Metrics for evaluating parsers. |
| **14** | **Dependency Parsing** | • **Dependency Relations:** Binary head-dependent links (Subject, Object).<br>• **Projectivity:** Whether dependency arcs cross.<br>• **Universal Dependencies:** Cross-linguistic standard. | • **Transition-Based:** Shift-Reduce parsing with a stack and buffer.<br>• **Graph-Based:** Maximum Spanning Tree (MST) algorithms (Chu-Liu-Edmonds). |

### Table 4: Semantics and Discourse
This section covers meaning at the logical, lexical, and document levels.

| Chapter | Topic | Key Concepts | Core Algorithms / Models |
| :--- | :--- | :--- | :--- |
| **15** | **Logical Representations** | • **First-Order Logic (FOL):** Predicates, variables, quantifiers ($\exists, \forall$).<br>• **Lambda Notation:** Composing meaning ($\lambda$).<br>• **Event Representation:** Neo-Davidsonian events. | • **Modus Ponens:** Logical inference.<br>• **Description Logics:** Ontologies and subsumption relationships. |
| **18** | **Word Senses** | • **WordNet:** Database of lexical relations (synonyms, hypernyms).<br>• **WSD:** Word Sense Disambiguation.<br>• **Supersenses:** Coarse semantic categories. | • **Lesk Algorithm:** Dictionary-based WSD.<br>• **Nearest Neighbor:** WSD using contextual embeddings. |
| **19** | **Semantic Role Labeling** | • **Thematic Roles:** Agent, Patient, Theme.<br>• **Resources:** PropBank (verb-specific roles) vs. FrameNet (frame-specific roles).<br>• **Selectional Restrictions:** Constraints on arguments. | • **BiLSTM / BERT Labelers:** Classifying spans into semantic roles.<br>• **Integer Linear Programming:** Ensuring global consistency in role assignment. |
| **20** | **Sentiment & Affect** | • **Affective Lexicons:** Lists of words with valence/arousal scores.<br>• **Connotation Frames:** Implied sentiment of predicates toward arguments. | • **Semi-supervised Induction:** Learning lexicons from seed words using graph propagation or semantic axis methods. |
| **21** | **Coreference Resolution** | • **Mentions & Antecedents:** Linking "She" to "Victoria".<br>• **Architectures:** Mention-Pair vs. Mention-Ranking.<br>• **Winograd Schema:** Hard problems requiring world knowledge. | • **End-to-End Neural Coref:** Jointly detecting spans and clustering them.<br>• **Evaluation Metrics:** MUC, $B^3$, CEAF. |
| **22** | **Discourse Coherence** | • **Coherence Relations:** Explanation, Elaboration, Contrast.<br>• **Frameworks:** RST (Rhetorical Structure Theory) and PDTB.<br>• **Centering Theory:** Entity-based coherence. | • **Entity Grid Model:** Modeling coherence via entity transitions.<br>• **Shift-Reduce Discourse Parsing:** Building RST trees. |

### Table 5: Applications
This section covers how NLP is applied to real-world tasks.

| Chapter | Topic | Key Concepts | Core Algorithms / Models |
| :--- | :--- | :--- | :--- |
| **11** | **Machine Translation** | • **Encoder-Decoder:** Sequence-to-sequence mapping.<br>• **Attention:** Solving the bottleneck problem by focusing on specific source words.<br>• **Backtranslation:** Using monolingual data. | • **Beam Search:** Heuristic search for decoding.<br>• **BLEU:** N-gram precision metric for evaluation. |
| **17** | **Information Extraction** | • **Relation Extraction:** Detecting relationships (e.g., *employed-by*) between entities.<br>• **Temporal Extraction:** Identifying and normalizing dates/times.<br>• **Template Filling:** Extracting specific fields for events. | • **Distant Supervision:** Using databases to bootstrap training data.<br>• **Bootstrapping:** Iterative pattern learning. |
| **23** | **Question Answering** | • **IR-based QA:** Retrieve-and-Read paradigm.<br>• **Knowledge-based QA:** Querying databases (RDF triples).<br>• **Entity Linking:** Mapping text mentions to ontology IDs. | • **Bi-Encoders:** Dense vector retrieval.<br>• **Span Extraction:** Neural reading comprehension to identify answer spans (SQuAD). |
| **24** | **Chatbots & Dialogue** | • **Chatbots:** Unstructured conversation (ELIZA, Neural Chatbots).<br>• **Task-Oriented:** Frame-based (GUS) systems with slots.<br>• **Dialogue State:** Tracking user intent and slot values. | • **Rule-based:** Pattern matching (ELIZA).<br>• **Dialogue Policy:** Reinforcement learning for system actions.<br>• **Response Generation:** Encoder-Decoder models. |
| **25/26** | **Speech** | • **Phonetics:** Phones, Spectrograms, Formants, Mel scale.<br>• **ASR:** Mapping waveforms to text.<br>• **TTS:** Mapping text to waveforms. | • **CTC:** Connectionist Temporal Classification loss.<br>• **RNN-T:** Streaming recognition.<br>• **Tacotron2 / WaveNet:** Neural TTS and Vocoding.<br>• **WER:** Word Error Rate evaluation. |
