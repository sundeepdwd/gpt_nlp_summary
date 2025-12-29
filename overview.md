**"Overview of Natural Language Processing: Tools and Techniques"** by Harvard Business School Research Computing Services.

***

# Natural Language Processing (NLP) Overview

### **1. Introduction**
*   **Definition:** A subfield of AI and linguistics using computers to understand, interpret, and manipulate human language.
*   **Common Applications:**
    *   **Text Processing:** Translation, Autocorrect, Grammar Checkers, Autocomplete.
    *   **Speech/Voice:** Siri/Alexa, Clinical dictation.
    *   **Language Models:** Chatbots (Customer Service).
    *   **Market Intelligence:** Sentiment analysis, fraud detection, news-based trading, resume evaluation.

### **2. The Text Classification Workflow**
The core process of NLP involves four distinct steps:

#### **Step 1: Data Acquisition**
*   **Sources:** Documents, emails, web-sites, speech, tables.
*   **Methods & Tools:**
    *   **Web Scraping:** Python, R, Mozenda.
    *   **Direct Download:** Databases like Capital IQ, Data.gov.
    *   **Public APIs:** Twitter, NY Times, Facebook Graph API.
    *   **OCR (Optical Character Recognition):** AWS Textract, Abbyy FineReader (Used to digitize scanned PDFs like the "1940 Official Register of the US").
    *   **Voice-to-Text:** IBM Watson.

#### **Step 2: Pre-processing**
Cleaning raw text to make it analyzing-ready.
*   **Techniques:**
    *   **Tokenization:** Segmenting text into words or sentences.
    *   **Normalization:** Converting numbers (e.g., "twenty-three" $\rightarrow$ "23"), handling acronyms ("US" $\rightarrow$ "United States").
    *   **Cleaning:** Removing punctuation, white spaces, and special characters.
    *   **Stop Word Removal:** Removing low-value words (the, a, and, is).
    *   **Lemmatization:** Converting words to their dictionary form (e.g., "studies" $\rightarrow$ "studi").
    *   **Stemming:** Removing suffixes.

#### **Step 3: Feature Extraction**
Transforming text into numerical vectors (Text Vectorization) so models can understand it.

| Method | Description | Pros/Cons |
| :--- | :--- | :--- |
| **Bag-of-Words (BoW)** | Counts word frequencies. | Simple, but ignores context and grammar. |
| **N-Grams** | Sequences of *N* words (Bigrams, Trigrams). | Captures local context (e.g., "New York"). |
| **TF-IDF** | Term Frequency-Inverse Document Frequency. Weighs words by rarity. | Reduces impact of common words; easy to compute but ignores position/semantics. |
| **Word Embeddings** | Dense numerical vectors (e.g., Word2Vec, GloVe, BERT). | Captures semantic meaning and context; computationally expensive. |

#### **Step 4: Classification & Analysis**
Two primary analytical techniques were highlighted:

---

### **3. Deep Dive: Topic Modeling**
*   **Goal:** Unsupervised learning to discover abstract "themes" or topics within a large collection of documents (corpus).
*   **Output:** A short summary of themes (e.g., a "Budget" topic containing words like *million, tax, program*).
*   **Evolution of Models:**
    *   **LSI (1990):** Uses SVD; good for finding groups but rigid.
    *   **LDA (Latent Dirichlet Allocation - 2002):** The standard generative model. Assumes documents are mixtures of topics and topics are mixtures of words.
    *   **DTM (Dynamic Topic Models - 2006):** Adds a time component to track topic evolution.
    *   **BERT/Neural Models (Present):** Uses transformers for context-aware modeling (e.g., BERTopic, FinBERT).
*   **Supervised Topic Modeling:**
    *   Modifying LDA with known labels to improve accuracy.
    *   **FinBERT:** A domain-specific model pre-trained on financial documents (10-Ks, analyst reports).

---

### **4. Deep Dive: Sentiment Analysis**
*   **Goal:** Opinion mining to determine the attitude (Positive, Negative, Neutral) of a text.
*   **Workflow:** Data Selection $\rightarrow$ Scraping $\rightarrow$ Pre-processing $\rightarrow$ Analysis $\rightarrow$ Visualization.
*   **Three Main Approaches:**

    **A. Lexicon-Based (Rule-Based)**
    *   Uses lists of words labeled with "valence scores" (e.g., "Good" = +1, "Bad" = -1).
    *   **Tools:** VADER (optimized for social media), TextBlob, AFINN.
    *   **Pros:** Fast, no training data needed, transparent logic.
    *   **Cons:** Misses sarcasm and context; requires domain-specific dictionaries.

    **B. Classic Machine Learning**
    *   Uses classifiers like Naïve Bayes, SVM, or Decision Trees.
    *   Requires manual feature extraction (BoW, TF-IDF).
    *   **Pros:** Can be more accurate than Lexicons.
    *   **Cons:** Requires labeled training data.

    **C. Deep Learning**
    *   Uses Neural Networks (LSTM, CNN, Transformers).
    *   **Tools:** BERT, GPT-3, Roberta.
    *   **Pros:** State-of-the-art accuracy; handles complex context.
    *   **Cons:** "Black box" (hard to explain), resource-intensive.

---

### **5. Tools and Resources**
*   **Python Libraries:**
    *   **NLTK:** General purpose, popular.
    *   **SpaCy:** Fast, advanced tasks.
    *   **Gensim:** Best for Topic Modeling (LDA).
    *   **TextBlob:** Simple interface for sentiment.
*   **R Libraries:**
    *   `tidytext`, `text2vec`.
*   **No-Code/Low-Code Tools:**
    *   KNIME, Dataiku.
*   **Cloud Services:**
    *   AWS (Textract), Google Cloud, IBM Watson.
