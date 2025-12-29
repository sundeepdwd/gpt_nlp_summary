Based on the provided book **"Natural Language Processing with Python"**
https://tjzhifei.github.io/resources/NLTK.pdf
### **1. Accessing Text Corpora and Lexical Resources**
NLTK provides built-in access to a vast collection of text corpora (structured text data) and lexical resources (dictionaries).

*   **Accessing Standard Corpora:** Access established bodies of text like the Gutenberg collection, Brown corpus, or Reuters news.
    *   *Code Example:*
        ```python
        import nltk
        from nltk.corpus import gutenberg
        # Get words from Jane Austen's Emma
        emma_words = gutenberg.words('austen-emma.txt')
        ```
*   **WordNet:** A semantic dictionary that links words by meaning (synonyms, hyponyms).
    *   *Code Example:*
        ```python
        from nltk.corpus import wordnet as wn
        # Find synonym sets for 'motorcar'
        wn.synsets('motorcar') 
        # Output: [Synset('car.n.01')]
        ```
*   **Stopwords:** Access lists of high-frequency words (like "the", "to") often filtered out during processing.
    *   *Code Example:*
        ```python
        from nltk.corpus import stopwords
        stopwords.words('english')
        ```

### **2. Basic Text Analysis & Statistics**
NLTK allows for the statistical analysis of text to understand word frequency and usage context.

*   **Concordance:** Find a word and its immediate context.
    *   *Code Example:*
        ```python
        text1.concordance("monstrous")
        ```
*   **Frequency Distribution:** Count word occurrences to find the most common words or hapaxes (words appearing only once).
    *   *Code Example:*
        ```python
        fdist = FreqDist(text1)
        fdist.most_common(50)
        fdist.hapaxes()
        ```
*   **Collocations & Bigrams:** Identify words that frequently appear together (e.g., "red wine").
    *   *Code Example:*
        ```python
        text4.collocations()
        # Generates list like: United States; fellow citizens...
        ```
*   **Dispersion Plots:** Visualize the location of words across a text.
    *   *Code Example:*
        ```python
        text4.dispersion_plot(["citizens", "democracy", "freedom"])
        ```

### **3. Text Processing (Raw Text)**
Tools to clean and prepare raw text strings for analysis.

*   **Tokenization:** Splitting a string into a list of words and punctuation.
    *   *Code Example:*
        ```python
        raw = "The quick brown fox."
        tokens = nltk.word_tokenize(raw)
        # Output: ['The', 'quick', 'brown', 'fox', '.']
        ```
*   **Stemming:** Stripping affixes from words to find the root (e.g., "lying" $\rightarrow$ "lie").
    *   *Code Example:*
        ```python
        porter = nltk.PorterStemmer()
        porter.stem('lying') # Output: 'lie'
        ```
*   **Lemmatization:** Similar to stemming but uses a dictionary to ensure the root is a valid word.
    *   *Code Example:*
        ```python
        wnl = nltk.WordNetLemmatizer()
        wnl.lemmatize('women') # Output: 'woman'
        ```

### **4. Part-of-Speech (POS) Tagging**
Automatically assigning grammatical categories (noun, verb, adjective) to words in a sentence.

*   **Automatic Tagging:** NLTK processes a sequence of words and attaches a tuple containing the tag.
    *   *Code Example:*
        ```python
        text = nltk.word_tokenize("And now for something completely different")
        nltk.pos_tag(text)
        # Output: [('And', 'CC'), ('now', 'RB'), ('something', 'NN')...]
        ```
*   **N-Gram Tagging:** Using the context of preceding words to determine the tag of the current word.

### **5. Classification**
Using machine learning to label text (e.g., identifying gender from names, sentiment analysis).

*   **Feature Extraction:** Defining features (like the last letter of a name) to train a model.
*   **Naive Bayes Classifier:** A statistical classifier provided by NLTK.
    *   *Code Example:*
        ```python
        classifier = nltk.NaiveBayesClassifier.train(train_set)
        classifier.classify(gender_features('Neo'))
        # Output: 'male'
        ```

### **6. Information Extraction**
Extracting structured data (entities and relationships) from unstructured text.

*   **Chunking:** Segmenting multi-token sequences (like Noun Phrases) using regular expressions.
    *   *Code Example:*
        ```python
        grammar = "NP: {<DT>?<JJ>*<NN>}" # Chunk determiner/adjective/noun
        cp = nltk.RegexpParser(grammar)
        result = cp.parse(sentence)
        ```
*   **Named Entity Recognition (NER):** Recognizing entities like People, Organizations, and Locations.
    *   *Code Example:*
        ```python
        nltk.ne_chunk(tagged_sent)
        ```

### **7. Parsing & Grammars**
Analyzing the syntactic structure of sentences using formal grammars.

*   **Context-Free Grammars (CFG):** Defining rules for sentence structure (e.g., S $\rightarrow$ NP VP).
    *   *Code Example:*
        ```python
        grammar = nltk.parse_cfg("""
          S -> NP VP
          NP -> Det N
          VP -> V NP
        """)
        ```
*   **Parsing:** Using algorithms (Recursive Descent, Shift-Reduce) to build syntax trees based on a grammar.
    *   *Code Example:*
        ```python
        rd_parser = nltk.RecursiveDescentParser(grammar)
        for tree in rd_parser.nbest_parse(sent):
            print tree
        ```

### **8. Semantics & Logic**
Representing meaning and performing logical inference.

*   **First-Order Logic:** Translating natural language into logical formulas.
    *   *Code Example:*
        ```python
        lp = nltk.LogicParser()
        lp.parse('exists x.(dog(x) & bark(x))')
        ```
*   **Discourse Semantics:** Analyzing meaning across multiple sentences (e.g., resolving pronoun references like "he" or "it").
