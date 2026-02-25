Corrective RAG (CRAG) Implementation
This project demonstrates a step-by-step implementation of a Corrective Retrieval-Augmented Generation (CRAG) system. It progresses from a standard RAG pipeline to a sophisticated graph-based agent that evaluates retrieval quality and triggers corrective actions like web searches and query rewriting.

 Overview
Corrective RAG improves standard RAG by introducing a "Retriever Evaluator" node. This evaluator determines if the retrieved documents are relevant, irrelevant, or ambiguous. Based on this verdict, the system decides whether to:

Generate directly using internal knowledge.

Perform a web search to fill knowledge gaps.

Rewrite the query to optimize external search results.

 Project Structure
The implementation is broken down into six progressive Jupyter notebooks:

1_basic_rag.ipynb: Sets up the foundation using LangChain, FAISS, and OpenAI. It demonstrates the standard "Retrieve-and-Generate" flow.

2_retrieval_refinement.ipynb: Introduces Knowledge Refinement. It decomposes retrieved chunks into sentences, filters out irrelevant ones using an LLM, and recomposes a "refined context".

3_retrieval_evaluator.ipynb: Adds a Score-based Evaluator. Each document is assigned a relevance score (0.0 to 1.0). High scores lead to generation, while low scores trigger a fallback (simulated web search).

4_web_search_refinement.ipynb: Integrates Tavily Search. If internal documents are insufficient, the system fetches real-time data from the web and applies the refinement logic to the search results.

5_query_rewrite.ipynb: Adds Query Rewriting. Before performing a web search, an LLM optimizes the original user question into a keyword-based query optimized for search engines.

6_ambiguous.ipynb: Refines the Routing Logic. It handles "Ambiguous" retrieval results by combining the best internal documents with supplemental web search data to provide a balanced answer.

🛠️ Key Components
Vector Store: FAISS with OpenAI Embeddings (text-embedding-3-large).

LLM: GPT-4o-mini used for generation, evaluation, and query rewriting.

State Management: LangGraph handles the complex routing logic between retrieval, evaluation, and generation.

External Search: TavilySearchResults for real-time web grounding.

 Setup
Prerequisites:

Python 3.10+

OpenAI API Key

Tavily API Key (for notebooks 4-6)

Installation:

Bash
pip install langchain langchain-openai langgraph faiss-cpu pypdf tavily-python python-dotenv
Environment: Create a .env file and add your credentials:

Code snippet
OPENAI_API_KEY=your_openai_key
TAVILY_API_KEY=your_tavily_key
 Usage
The system is trained on the PDF books included in the documents/ folder. You can run any notebook sequentially to see how the system handles questions ranging from specific book content to recent AI news.
