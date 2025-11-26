# AI-ML-Assignment-5-Implementing-a-Simple-Retrieval-Augmented-Generation-RAG-System
Victoria Salomon

## Overview
This project implements a simple Retrieval-Augmented Generation (RAG) system using a custom knowledge base (KB). The goal is to demonstrate how large language models (LLMs) can be grounded in external factual knowledge to reduce hallucinations and generate accurate answers. 

The pipeline consists of:

1. **Knowledge Base Creation** – a short text document containing relevant company policies and information.  
2. **Embedding & Indexing** – embedding KB chunks with a pre-trained Sentence Transformer and indexing them with FAISS.  
3. **Retrieval** – similarity search to find the most relevant KB chunks for a given query.  
4. **Generation** – answering queries using `t5-small`, conditioned on the retrieved context.

---

## Models Used
- **Embedding Model:** `sentence-transformers/all-MiniLM-L6-v2`  
- **Language Model:** `t5-small`  

---

## Knowledge Base
The KB contains 2–3 paragraphs on the company's training programs, remote work policies, and sustainability initiatives. Example chunk:

 > "The company provides training programs for career growth, including workshops on communication, leadership, and technical skills. Participation is voluntary but recommended for all employees to enhance skill development."

---

## Retrieval Process & Test Cases

| Test Case | Query | Retrieved Chunks | Model Answer | Notes |
|-----------|-------|-----------------|--------------|-------|
| Factual | What training programs does the company provide? | Training programs chunk, Sustainability chunk | Employees can attend workshops on communication, leadership, and technical skills. Participation is voluntary but recommended for all employees to enhance skill development. | Correctly answered using KB |
| Foil/General | Who founded the company? | Sustainability chunk | KB. Question: Who founded the company? | Not in KB; model could not generate answer |
| Synthesis | How many remote work days are allowed? | Remote work chunk, Sustainability chunk | Employees are eligible for remote work up to two days per week. Flexible hours are allowed with manager approval. | Combined info from multiple chunks |

---

## Analysis
- **Factual questions:** RAG successfully retrieved relevant context, enabling accurate answers.  
- **Foil/General questions:** When information was absent from KB, the system either returned incomplete or fallback answers. This highlights the importance of KB coverage.  
- **Synthesis questions:** The model effectively combined information from multiple retrieved chunks.  
- **Hallucination mitigation:** Using retrieved context significantly reduced unsupported or fabricated answers compared to raw LLM responses.  

---

## How to Run
1. Clone the repository.  
2. Activate your environment and install dependencies:

```bash
conda create -n rag-env python=3.11
conda activate rag-env
pip install torch transformers sentence-transformers faiss-cpu numpy pandas jupyter

## Launch the notebook:

jupyter notebook RAG_notebook.ipynb

Run each cell sequentially to load the KB, build embeddings, retrieve chunks, and generate answers.
