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

#### C. Stop Words
*   **Concept:** Filtering out common, low-information words (e.g., a, an, the, of).
*   **Trade-off:** Reduces noise but can lose relational information.
*   *Example of loss:* "Mark reported **to** the CEO" vs. "Suzanne reported **as** the CEO." Removing stop words makes these identical ("reported CEO"), destroying the hierarchy information.

#### D. Stemming
*   **Concept:** A crude heuristic process that chops off the ends of words to reduce them to a base form.
*   **Tools:** Porter Stemmer, Snowball Stemmer.
*   *Example:*
    *   Input: "developing", "developers", "development"
    *   Output: "develop"
*   *Flaw:* Can create non-words or confuse meanings (e.g., "better" might become "bet", conflating "good" with "gambling").

#### E. Lemmatization
*   **Concept:** A sophisticated process using a knowledge base/dictionary to reduce a word to its semantic root (lemma). It considers the Part of Speech (POS).
*   *Example:*
    *   Input: "better"
    *   Output: "good" (Stemming would fail here).
*   *Trade-off:* Slower than stemming but more accurate for capturing meaning.

### Summary Comparison: Stemming vs. Lemmatization
| Feature | Stemming | Lemmatization |
| :--- | :--- | :--- |
| **Method** | Chops suffixes (Pattern matching) | Dictionary lookup + POS tagging |
| **Speed** | Fast | Slower |
| **Accuracy** | Low (can produce non-words) | High (produces valid words) |
| **Example** | "better" $\rightarrow$ "bet" | "better" $\rightarrow$ "good" |
