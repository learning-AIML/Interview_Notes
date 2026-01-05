# Q3: What is RAG Architecutre

**RAG** is an architecture that gives Large Language Models (LLMs) the ability to "look up" external information before answering a question. It bridges the gap between the LLM's frozen training data and your live, private data.

## 1. The 3-Step Architecture

### Phase 1: Retrieval (The Search)
Before the LLM speaks, the system searches a **Vector Database** (your private library) for information relevant to the user's query.
* **Input:** User question ("What is our refund policy?").
* **Action:** System searches indexed documents for keywords like "refund", "return", "money back".
* **Output:** The specific paragraph containing the policy.

### Phase 2: Augmentation (The Assembly)
The system combines the user's question with the retrieved data into a single prompt.
* **Prompt Construction:**
    > "You are a helpful assistant. Use the following context to answer the question.
    > **Context:** 'Refunds are processed within 14 days if the item is unopened.'
    > **User Question:** 'How long does a refund take?'"

### Phase 3: Generation (The Answer)
The LLM generates the final answer using *only* the facts provided in Phase 2.
* **Result:** "Refunds take 14 days, provided the item is unopened."

## 2. Comparison: RAG vs. Fine-Tuning

| Feature | RAG (Retrieval) | Fine-Tuning (Training) |
| :--- | :--- | :--- |
| **Analogy** | Open-book exam (Look up answers) | Memorization (Learn facts by heart) |
| **Knowledge Update** | Instant (Just add a new document) | Slow (Must re-train the model) |
| **Accuracy** | High (Cites specific sources) | Can hallucinate (Make things up) |
| **Cost** | Low (Vector DB is cheap) | High (GPU training is expensive) |

## 3. Real-World Example: "The Legal Assistant"
**Scenario:** A lawyer needs to know the specific penalty for a compliance breach in a 2024 regulation.

1.  **Ingestion:** The law firm uploads the new "2024 Compliance Act.pdf".
2.  **User Query:** "What is the penalty for Section 5 violations?"
3.  **Retrieval:** The system scans the PDF and finds Section 5, Paragraph 3: *"Violations result in a $50,000 fine."*
4.  **Generation:** The AI answers: *"According to Section 5, the penalty is a $50,000 fine."* (It cites the source).

## 4. Key Components
* **Vector Database:** (e.g., Pinecone, Milvus) Stores your data as numbers ("embeddings") for fast semantic searching.
* **Embeddings Model:** Translates text into numbers so the computer can understand "Apple" and "iPhone" are related.
* **Orchestrator:** (e.g., LangChain, LlamaIndex) The code that glues the database and the LLM together.
