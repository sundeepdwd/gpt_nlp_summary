Based on **Chapter 2: "Tokens of thought: Natural language words"** 

### 1. Tokenization
**Definition:** The process of breaking unstructured text into smaller chunks of information (tokens) that can be counted as discrete elements (packets of thought). These are usually words, but can be characters, subwords, or n-grams.

#### Approaches to Tokenization
*   **Whitespace Tokenization (The Simplest):**
    *   Method: Python's `.split()`
    *   *Pros:* Fast.
    *   *Cons:* Treats punctuation as part of the word (e.g., "rain." is different from "rain").
    *   *Example:*
        ```python
        text = "The words were on their way."
        # Output: ['The', 'words', 'were', 'on', 'their', 'way.']
        ```
*   **Rule-Based Tokenization (Regex):**
    *   Method: `re.findall()` with a pattern.
    *   *Goal:* Separate punctuation from words while keeping contractions (like "don't") together.
    *   *Example Pattern:* `r'\w+(?:\'\w+)?|[^\w\s]'`
    *   *Result:* Separates "way" and "." but keeps "There's" as one token.
*   **SpaCy Tokenization:**
    *   Method: Production-ready library that handles edge cases and adds metadata (POS tags).
    *   *Feature:* It is non-destructive (can reconstruct the original text perfectly).
*   **Subword/WordPiece Tokenization (Modern NLP):**
    *   Used in Deep Learning (BERT, GPT).
    *   Breaks rare words into meaningful chunks (e.g., "unfriendly" $\rightarrow$ "un", "friend", "ly").
    *   *Benefit:* Solves the "Out of Vocabulary" (OOV) problem by building words from known pieces.

---

### 2. Normalization (Vocabulary Improvement)
**Definition:** Techniques to reduce the size of the vocabulary (dimensionality reduction) by consolidating similar words into a single form. This helps models generalize better but may lose specific meaning.

#### A. Case Folding
*   **Concept:** Converting all text to lowercase.
*   **Goal:** Ensure "Apple" and "apple" are counted as the same word.
*   **Risk:** Loss of meaning in proper nouns (e.g., "Rose" the person vs. "rose" the flower; "doctor" vs. "Doctor" as a title).
*   *Best Practice:* Only lowercase the first word of a sentence to preserve proper nouns elsewhere.

#### B. N-grams
*   **Concept:** Grouping sequences of $n$ tokens together to retain context.
*   *Example:* "Ice cream". Treated separately, "ice" and "cream" lose the specific meaning of the dessert. As a 2-gram (bigram), they retain meaning.
*   *Utility:* Helps capture negation (e.g., "not happy" vs. just "happy").







### 1. Stemming
**Definition:** A crude, heuristic process that chops off the ends of words (suffixes) to reduce them to a common base form. The result is called a **stem**.

*   **Characteristics:**
    *   **Not always a real word:** The resulting stem is just a token/label. For example, "housing" and "houses" both become `hous`.
    *   **Rule-based:** It uses simple pattern matching (regular expressions) rather than understanding grammar or meaning.
*   **Algorithms mentioned:**
    *   **Porter Stemmer:** The most common algorithm (from the 80s). It strips suffixes like *ed*, *ing*, and *ation*.
    *   **Snowball Stemmer:** A more aggressive and accurate improvement over Porter.
        *   *Example:* Snowball stems "fairly" to `fair`, while Porter might leave it as `fairli`.
*   **Pros:**
    *   Fast to compute.
    *   Reduces vocabulary size significantly.
    *   Improves **Recall** in search engines (broadens search results).
*   **Cons (The "Spoofing" Problem):**
    *   It can conflate words with different meanings.
    *   *Example:* It strips the *er* from "better" to create `bet`. This lumps "better" (good) with "betting" (gambling), losing the original meaning.

### 2. Lemmatization
**Definition:** A more extensive normalization technique that reduces a word to its semantic root, or **lemma** (a valid dictionary word).

*   **Characteristics:**
    *   **Meaning-aware:** It uses a knowledge base (like WordNet) to understand synonyms and word endings.
    *   **Part of Speech (POS) dependent:** To get the correct lemma, the algorithm usually needs to know if the word is a noun, verb, or adjective.
*   **Algorithms/Tools mentioned:**
    *   **NLTK `WordNetLemmatizer`:** Requires you to specify the POS. If you don't, it assumes Noun.
        *   *Example:* `lemmatize("better", pos="a")` $\rightarrow$ `good`.
        *   *Limitation:* Without the POS tag, it returns "better". It also fails to connect "best" to "good" because that connection is missing in the WordNet graph.
    *   **SpaCy:** Uses a built-in dictionary and context.
        *   *Example:* `nlp("better")` $\rightarrow$ automatically detects it is an adverb/adjective and returns `well` or `good`.
*   **Pros:**
    *   Produces valid English words.
    *   Preserves semantic meaning (e.g., handles irregular words like "better" $\rightarrow$ "good").
    *   Improves **Precision** (results are more relevant to the original meaning).
*   **Cons:**
    *   Slower than stemming because it requires lookups and POS tagging.
    *   Can create ambiguity if the POS tagger makes a mistake.

---

### Summary Comparison: Stemming vs. Lemmatization

| Feature | Stemming | Lemmatization |
| :--- | :--- | :--- |
| **Example Input** | "better" | "better" |
| **Output** | `bet` | `good` |
| **Method** | Chops suffixes (Pattern matching) | Dictionary lookup + POS tagging |
| **Speed** | Fast | Slower |
| **Result Type** | Often a non-word fragment | Valid dictionary word |
| **Best Use Case** | Large-scale search / Information Retrieval (Recall) | Chatbots / NLU where meaning matters (Precision) |
| **Major Flaw** | Over-generalization (lumps "better" with "betting") | Requires context/POS to work correctly |

### Note on Non-English Languages (Chinese)
The text notes (Section 2.4.1) that concepts like stemming and lemmatization do not apply to pictographic languages like Chinese or Japanese (Kanji).
*   Characters are **radicals** or compounds.
*   Separating parts of a character changes the meaning entirely.
*   *Rule of thumb:* Do not stem or lemmatize unless statistics indicate it helps the pipeline perform better.
