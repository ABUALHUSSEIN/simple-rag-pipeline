# Simple RAG Pipeline in Python

This repository contains a simple, end-to-end **Retrieval-Augmented Generation (RAG)** pipeline built in Python using Hugging Face `transformers` and `sentence-transformers`.

The project demonstrates the core RAG concept: providing a language model with relevant context from a knowledge base before asking it to answer a question. It's like giving the model an "open-book exam."

## 🚀 Project Overview

This pipeline consists of two main components:

1.  **The Retriever 🔎**: A `sentence-transformer` model (`all-MiniLM-L6-v2`) that takes a user query, encodes it into a vector, and uses semantic search (cosine similarity) to find the most relevant document from a predefined knowledge base.

2.  **The Generator ✍️**: A `distilbert` question-answering model (`distilbert-base-cased-distilled-squad`) that takes the user's query and the context provided by the retriever to extract the precise answer from the context.

The script connects these two components: the output of the retriever becomes the input for the generator.

## ✨ How It Works

The process follows these steps:

1.  **Load Models**: The Retriever model is loaded onto the CPU, and the Generator model is loaded onto the GPU (if available) for faster inference.
2.  **Define & Encode Knowledge**: A simple list of strings acts as our "long-term memory" or knowledge base. The Retriever encodes these documents into numerical vectors (embeddings) for efficient searching.
3.  **User Query**: The user asks a question (e.g., "What is the capital of France?").
4.  **Retrieve Context**: The pipeline encodes the user's query into a vector and compares it against all the document vectors. The text of the most similar document is retrieved.
5.  **Generate Answer**: The retrieved text and the original query are passed to the Generator, which extracts the final answer.

## 🛠️ Technologies Used

*   **Python 3.x**
*   **PyTorch**: The backend deep learning framework.
*   **Hugging Face `transformers`**: For the question-answering pipeline (Generator).
*   **Hugging Face `sentence-transformers`**: For creating dense vector embeddings (Retriever).

###  Output
✅ Retriever model (MiniLM) loaded. 
✅ Generator model (DistilBERT) loaded.
   -> Running on GPU (Good!)
📚 Knowledge base created with 5 documents.
--- Task 1: Encoding Knowledge Base ---
✅ Success! Knowledge base has been encoded.
   -> Embedding shape: torch.Size([5, 384])

... [Other task outputs] ...

--- Task 4: Building the Full RAG Pipeline ---
Testing the full RAG pipeline...
Query: 'What is the capital of France?'
   -> Retrieved Context: 'The capital of France is Paris, which is known for the Eiffel Tower.'
   -> Final Answer: 'Paris'
✅ Success! Your RAG pipeline is working!

--- Another Test ---
Query: 'Who was the first person on the moon?'
   -> Retrieved Context: 'The first person to walk on the Moon was Neil Armstrong in 1969.'
   -> Final Answer: 'Neil Armstrong'
✅ Correctly answered the second question!
```

