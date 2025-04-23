# CV Search Engine with Mistral & RAG

This project sets up a simple yet powerful semantic search engine for a CV, leveraging a local language model (Mistral) with Retrieval-Augmented Generation (RAG). The goal is to allow users to ask natural language questions about a PDF CV and get meaningful, context-aware answers.

# Pipeline Overview

*PDF Text Extraction* : The CV PDF is read using Python's fitz (PyMuPDF) library to extract the full text content.

*Text Chunking*: The raw text is split into smaller, coherent chunks using LangChain’s RecursiveCharacterTextSplitter.
Splits occur around natural language boundaries (e.g., periods, newlines). A 30-character overlap between chunks ensures that important edge information is not lost and remains searchable.

*Vectorization*:Each chunk is transformed into a dense vector using the all-MiniLM-L6-v2 model from SentenceTransformers. These embeddings represent the semantic content of each chunk.

*FAISS Indexing*: Vectors are stored in a FAISS flat index using Euclidean (L2) distance. During retrieval, the input query is also vectorized and compared against all stored embeddings. The top 3 most relevant chunks are returned based on similarity.

*LLM Response Generation with Mistral*: The retrieved chunks are sent to a locally hosted Mistral model via Ollama. The system constructs a prompt by combining the retrieved context with the user's question. Mistral generates a playful, informative answer based on the provided information.

📚 Example Use Case

Question: "Where did Koonstantina study?"→ Output: "She studied at Aristotle University, diving deep into linguistics and English literature. Scholar vibes!"

# Tech Stack

Text Extraction: PyMuPDF (fitz)
Text Splitting: LangChain
Embeddings: SentenceTransformers (all-MiniLM-L6-v2)
Vector Search: FAISS (Flat Index, L2 distance)
Language Model: Mistral (served locally via Ollama)

# Features

Zero external API calls
Runs fully locally
Playful, conversational tone in answers
Code ready to scale or adapt to other documents
#  Getting Started

Clone this repo
Install requirements: pip install -r requirements.txt

Run the notebook

Ask questions about your CV like a boss 🤓

Feel free to extend this to other document

