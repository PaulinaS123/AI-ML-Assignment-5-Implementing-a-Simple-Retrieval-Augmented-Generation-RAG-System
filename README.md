# AI-ML-Assignment-5-Implementing-a-Simple-Retrieval-Augmented-Generation-RAG-System
Victoria Salomon

## Overview
This project implements a simple Retrieval-Augmented Generation (RAG) system using a custom knowledge base (KB). The goal is to demonstrate how large language models (LLMs) can be grounded in external factual knowledge to reduce hallucinations and generate accurate answers. 

The pipeline consists of:

1. **Knowledge Base Creation** – a short text document containing relevant company policies and information.  
2. **Embedding & Indexing** – embedding KB chunks with a pre-trained Sentence Transformer and indexing them with FAISS.  
3. **Retrieval** – similarity search to find the most relevant KB chunks for a given query.  
4. **Generation** – answering queries using `t5-small`, conditioned on the retrieved context.  
