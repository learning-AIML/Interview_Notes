# Q6: What is a Transformer?

**Transformers** are the neural network architecture that revolutionized AI in 2017 (introduced by Google in the paper *"Attention Is All You Need"*). Before Transformers, AI read text sequentially (left-to-right), like a human reading a sentence one word at a time. Transformers read the *entire* sentence at once.

## 1. The Core Innovation: "Attention"
The most critical part of a Transformer is the **Self-Attention** mechanism. This allows the model to weigh the importance of different words in a sentence relative to each other.

### The Analogy: Queries, Keys, and Values (Q, K, V)
To understand how Attention works mathematically, imagine every word in a sentence is broken down into three vectors:
1.  **Query (Q):** What is this word looking for?
2.  **Key (K):** What does this word contain? (Like a label).
3.  **Value (V):** The actual meaning/content of the word.

**The Process:**
Imagine the sentence: *"The bank of the river."*
1.  The model analyzes the word **"bank"**.
2.  **"bank" (Query)** scans the sentence asking: "Which other words give me context?"
3.  It matches with **"river" (Key)**.
4.  **Mathematical Result:** The similarity score is high. The model updates the **Value** of "bank" to mean *land alongside water*, effectively ignoring the meaning of *financial institution*.

### Multi-Head Attention
The model runs this process multiple times in parallel:
* **Head 1:** Focuses on grammar (connecting "The" to "bank").
* **Head 2:** Focuses on semantics (connecting "river" to "bank").
* **Head 3:** Focuses on pronouns.
This results in a rich, multi-dimensional understanding of the text.

## 2. The Step-by-Step Workflow
Here is the pipeline of data inside a Transformer:

### Step 1: Input Embeddings
Computers cannot process raw text. Each word is converted into a **Vector** (a list of numbers) that represents its semantic meaning.
* *Input:* "Hello" $\rightarrow$ `[0.12, -0.45, 0.88...]`

### Step 2: Positional Encoding
Since Transformers process all words simultaneously (parallel processing), they initially lack a sense of order. They don't know if "Dog" came before "Man".
* **The Fix:** A mathematical pattern (Sine/Cosine wave) is added to each vector to stamp it with its position (1st, 2nd, 3rd...).

### Step 3: Encoder & Decoder
* **Encoder:** Reads the input and creates a "Context Vector" (a numerical summary of the sentence's meaning).
* **Decoder:** Takes the Context Vector and generates the output text one word at a time.
    * *Note:* **GPT** models are "Decoder-Only" (Generative). **BERT** models are "Encoder-Only" (Understanding).

### Step 4: Feed-Forward Network
After Attention highlights the relevant connections, the data flows through a standard dense neural network layer to process the features.

### Step 5: Output (Softmax)
The model outputs a probability score for every word in its vocabulary.
* *Example:* `cat: 95%`, `dog: 4%`, `car: 1%`.
* The word with the highest probability is selected as the next token.

## 3. Why Transformers Won (vs. RNNs)

| Feature | RNNs / LSTMs (The Old Way) | Transformers (The New Way) |
| :--- | :--- | :--- |
| **Processing** | Sequential (Slow, word-by-word) | Parallel (Fast, all-at-once) |
| **Memory** | Struggles with long sentences (Forgets) | Perfect memory via Attention |
| **Hardware** | Hard to optimize on GPUs | Highly optimized for GPUs |
