https://sitams.ac.in/wp-content/uploads/2025/10/NLP-notes.pdf

This is a comprehensive, detailed summary of the course material, broken down by topic. It includes specific theories, definitions, and **expanded examples** derived directly from your lecture slides to ensure nothing is missed.

---

### 1. Introduction to Natural Language Processing (NLP)

**Definition:** NLP is the branch of AI and Computer Science concerned with the interaction between computers and human language.
*   **Goal:** To interpret (NLU) and generate (NLG) human language.
*   **NLP vs. Data Processing:**
    *   *Data Processing:* Tools like the Unix `wc` command count bytes/lines blindly without understanding.
    *   *NLP:* Requires linguistic knowledge (e.g., knowing that "didn't" is two words: "did" and "not", or that "bank" is a noun).

#### The Core Challenge: Ambiguity
Language is hard because it is imprecise. The slides highlight several specific types of ambiguity:

1.  **Lexical Ambiguity:** A single word has multiple meanings or syntactic categories.
    *   *Slide Example:* "Rose rose to put rose roes on her rows of roses."
        *   *Breakdown:* "Rose" (Proper Noun/Name) "rose" (Verb: stood up) to put "rose" (Adjective: pink-colored) "roes" (Noun: fish eggs) on her "rows" (Noun: lines) of "roses" (Noun: flowers).
    *   *Slide Example:* "Will Will will Will’s will?" (Noun vs. Verb vs. Name).

2.  **Structural Ambiguity:** The grammar of a sentence allows for multiple valid parse trees (interpretations).
    *   *Slide Example:* "I saw the man with the telescope."
        *   *Meaning A:* I used a telescope to see the man.
        *   *Meaning B:* I saw a man who was holding a telescope.

3.  **Referential/Discourse Ambiguity:** It is unclear what a pronoun refers to.
    *   *Slide Example:* "The teacher is wearing sunglasses because the class is so **bright**."
        *   Does "bright" mean the students are smart, or the room is physically filled with light?

4.  **Pragmatic Ambiguity:** Meaning depends on world knowledge/context.
    *   *Slide Example:* "Manhattan calls out to Dave."
        *   *Literal:* A city is speaking (Impossible).
        *   *Pragmatic:* The city appeals to him emotionally (Metaphor).

---

### 2. Linguistics and Grammar

To process language, computers need rules (Grammar).

**Generative Grammar (Noam Chomsky):**
A set of rules capable of generating all possible grammatical sentences in a language. It distinguishes between two levels of representation:
1.  **Deep Structure:** The underlying abstract meaning.
    *   *Example:* `Subject: Pooja`, `Action: Plays`, `Object: Veena`.
2.  **Surface Structure:** The actual syntactic arrangement of words.
    *   *Example 1:* "Pooja plays veena."
    *   *Example 2:* "Veena is played by Pooja."
    *   **Theory:** Transformational rules convert Deep Structure into different Surface Structures. Both examples above have different surface structures but the *same* deep structure.

**Phrase Structure Grammar:**
Breaks sentences into constituents (Noun Phrases, Verb Phrases) based on derivation rules.
*   *Rule:* `S -> NP + VP` (A Sentence consists of a Noun Phrase and a Verb Phrase).

---

### 3. Text Pre-processing (Normalization)

Before AI models can use text, it must be cleaned and structured.

#### A. Tokenization
The process of chopping text into pieces (tokens).

*   **Concepts:**
    *   **Token:** An instance of a word.
    *   **Type:** A unique word concept.
    *   *Slide Example:* "to sleep more to learn"
        *   **Tokens (5):** to, sleep, more, to, learn.
        *   **Types (4):** to, sleep, more, learn.

*   **Methods:**
    1.  **Space-based:** Splits on whitespace. (Fails on Chinese/Japanese which have no spaces).
    2.  **Word-based:** Splits on punctuation. (Issue: "U.S.A." vs "USA").
    3.  **Sub-word Tokenization (BPE):** Used in Modern LLMs (BERT/GPT). It solves the **Out-Of-Vocabulary (OOV)** problem by breaking unknown words into known parts.

#### **Deep Dive: Byte-Pair Encoding (BPE) Algorithm**
This is a greedy algorithm to build a vocabulary of sub-words.
1.  **Start:** Treat every character as a token. Add a special end-token `_`.
    *   *Corpus:* "low _", "low _", "new _"
    *   *Vocab:* l, o, w, n, e, _
2.  **Iterate:** Count the most frequent adjacent pair of characters.
    *   *Example:* If 'e' and 'r' appear together most often, merge them into a new symbol `er`.
3.  **Repeat:** Count again with the new symbol. If `er` and `_` appear together often, merge to `er_`.
4.  **Result:** Common words remain whole ("low_"); rare words are segmented ("unlikeliest" $\to$ "un", "likely", "est").

#### B. Word Normalization
*   **Case Folding:** Converting to lower case.
    *   *Benefit:* "General Motors" matches "general motors".
    *   *Risk:* "US" (Country) becomes "us" (Pronoun).
*   **Stop Word Removal:** Removing function words (the, is, at, which).
    *   *Benefit:* Reduces file size for search engines.
    *   *Risk:* "To be or not to be" disappears entirely if stop words are removed.

#### C. Sentence Segmentation
Deciding where a sentence ends is a binary classification problem.
*   **The Ambiguous Period (`.`):** Is it a sentence end? An abbreviation (Dr.)? A decimal (4.3)?
*   **Solution:** Use a Decision Tree.
    *   *Feature 1:* Is the word `etc.`? $\to$ Not EOS.
    *   *Feature 2:* Is the next word capitalized? $\to$ Likely EOS.

---

### 4. Morphology: Stemming vs. Lemmatization

Morphology is the study of internal word structure.

#### 1. Stemming
A crude, rule-based heuristic to chop off suffixes.
*   **Porter Stemmer (1980):** The most common algorithm. It uses a cascade of rules.
    *   *Step 1a Rules:*
        *   `sses` $\to$ `ss` (caresses $\to$ caress)
        *   `s` $\to$ `null` (cats $\to$ cat)
    *   *Step 1b Rules:*
        *   `(*v*)ing` $\to$ null (walking $\to$ walk). *Note: The rule requires a vowel in the stem to prevent "sing" becoming "s".*
*   **Errors:**
    *   **Over-stemming:** "Organization" $\to$ "Organ" (Too aggressive, meaning is lost).
    *   **Under-stemming:** "Alumnus" vs "Alumni" (Fails to merge them).

#### 2. Lemmatization
A sophisticated process that uses a dictionary (lexicon) and morphological analysis to return the **Lemma** (the dictionary headword).
*   *Stemming result:* "better" $\to$ "better" (No rule for irregulars).
*   *Lemmatization result:* "better" $\to$ **"good"** (Understands the root meaning).
*   *Stemming result:* "meeting" $\to$ "meet" (Indiscriminate).
*   *Lemmatization result:* "meeting" (Noun) $\to$ "meeting"; "meeting" (Verb) $\to$ "meet".

---

### 5. Statistical Language Modeling (N-Grams)

Language models assign probabilities to sequences of words. $P(W)$.
*   *Example:* A model should know that "I am going **home**" is more probable than "I am going **house**".

**The Chain Rule:**
$$P(w_1...w_n) = P(w_1) \times P(w_2|w_1) \times P(w_3|w_1w_2) ...$$

**The Markov Assumption:**
We cannot calculate probability based on *entire* history (too much data). We assume a word depends only on the last $N-1$ words.

1.  **Unigram (N=1):** No history. Uses simple frequency.
    *   $P(w_i)$
    *   *Assumption:* Words are independent. "The" is just as likely to start a sentence as end it.

2.  **Bigram (N=2):** Looks at the previous 1 word.
    *   $P(w_i | w_{i-1})$
    *   *Slide Example:* "The office is about fifteen minutes from my house."
    *   *Approximation:* $P(\text{office} | \text{about fifteen minutes from}) \approx P(\text{office} | \text{from})$.

3.  **Trigram (N=3):** Looks at previous 2 words.
    *   $P(w_i | w_{i-2} w_{i-1})$

---

### 6. Processing Indian Languages
Indian languages (Hindi, Urdu, Dravidian langs) present unique challenges compared to English.
*   **Word Order:** English is **SVO** (Subject-Verb-Object). Indian languages are typically **SOV**.
*   **Free Word Order:** In English, "Ram killed Ravana" is different from "Ravana killed Ram." In Indian languages, markers attached to words allow you to move words around without changing the meaning.
*   **Post-positions:** English uses Pre-positions (*in* the box). Indian languages use Post-positions (box *in* / box *me*).
*   **Computational Framework:** The **Paninian Grammar** is often used. It focuses on **Karaka** relations (syntactic-semantic relations between verbs and nouns, like Agent, Object, Instrument) rather than position-based parsing.
