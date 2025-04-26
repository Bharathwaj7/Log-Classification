# 📄 Chat with PDF using Groq

description: >
  Interact with your PDF documents using a conversational AI powered by Groq's cutting-edge LLMs and Streamlit!  
  Built for document understanding, question answering, and real-time knowledge extraction. 🚀

overview:
  description: >
    This application allows users to upload one or more PDF files, automatically process the text inside them, and interact conversationally via a selected Groq-hosted Large Language Model (LLM).  
    It combines modern embeddings, local vector search (FAISS), and LLM-driven reasoning to answer your queries accurately. 📚

features:
  - Multi-PDF Upload: Upload one or several PDF documents at once for combined analysis. 📄
  - Dynamic Chunking: Automatically adjusts the text split size based on document size for optimized retrieval. 🔄
  - Embeddings-Based Search: Create vector representations of document chunks using Sentence Transformers. 🧠
  - Groq Model Selection: Choose from a wide range of high-performance Groq models for answering your queries. 🤖
  - First-Time Setup Auto-Install: Automatically installs missing Python packages if they aren't detected. ⚙️
  - Streamlit Interface: Clean, minimal, and interactive web UI for uploading files and chatting. 💻
  - Environment Configurable: Manage API keys and settings easily via `.env` files. 🔑

technical_stack:
  backend:
    - LangChain: Document loading, splitting, retrieval, and QA chains. 🔗
    - FAISS: High-performance local vector store for fast similarity search. ⚡
    - Sentence Transformers: Embedding generation via Hugging Face. 💬
    - PyPDF2: PDF parsing and text extraction. 📑
    - Groq API: Hosted LLM access for chat generation. 🌐
  frontend:
    - Streamlit: Real-time web UI for uploads, processing, and question answering. 🖥️
  infrastructure:
    - Python-dotenv: Environment variable management. 🛠️
    - Subprocess / pip Auto-Installer: First-time dependency management. 📦

getting_started:
  steps:
    - Clone the Repo: |
        git clone https://github.com/your-username/chat-with-pdf-using-groq.git
        cd chat-with-pdf-using-groq
    - Create & Activate Virtual Environment: |
        python3 -m venv venv
        source venv/bin/activate  # On Windows use: venv\Scripts\activate
    - Install Dependencies: |
        pip install -r requirements.txt
        (Or simply run the app and dependencies will auto-install.)
    - Set Environment Variables: |
        Create a .env file in the project root with your Groq API key:
        GROQ_API_KEY=your-groq-api-key-here
    - Run the App: |
        streamlit run app.py

models_supported:
  - qwen-qwq-32b
  - deepseek-r1-distill-llama-70b
  - gemma2-9b-it
  - compound-beta
  - compound-beta-mini
  - llama-3.1-8b-instant
  - llama3-70b-8192
  - meta-llama/llama-4-maverick-17b-128e-instruct
  - mistral-saba-24b
  - whisper-large-v3
  - allam-2-7b
  - and more... 🧑‍💻

how_it_works:
  - Upload PDFs: Users upload PDFs through the sidebar. 📂
  - Text Extraction: PyPDF2 extracts raw text from each page of the uploaded PDFs. 🔍
  - Chunk Splitting: Text is broken down using RecursiveCharacterTextSplitter based on document size. 🧩
  - Vector Embedding: Chunks are converted to vector embeddings via a pre-trained HuggingFace model (all-MiniLM-L6-v2). 🔢
  - FAISS Vector Store: The embedded chunks are stored locally using FAISS for efficient retrieval. 💾
  - Question Input: Users ask questions based on the uploaded documents. ❓
  - Contextual Retrieval: FAISS fetches the top relevant document chunks using semantic similarity. 🏃‍♂️
  - Answer Generation: Retrieved context is passed into the selected Groq LLM using a custom prompt for answering. 🧑‍🏫
  - Streaming Results: Answers are displayed back in real time on Streamlit. ⏱️

project_structure:
  chat-with-pdf-using-groq/:
    - app.py: Main Streamlit application 📝
    - faiss_index/: Saved FAISS index (created after processing PDFs) 📂
    - requirements.txt: Python dependencies 📑
    - .env: Environment variables (to be created) 🔐
    - README.md: Documentation (you are here) 📖
    - LICENSE: MIT License 📜

customization:
  - Add New Groq Models: Update the AVAILABLE_MODELS list in app.py with new model names. ⚙️
  - Change Embedding Models: Modify the get_embeddings() function to swap in different Sentence Transformer models. 🔄
  - Tune Prompt Templates: Edit the prompt_template inside make_qa_chain() to guide Groq LLMs differently. ✍️
  - Adjust Chunk Size Logic: Tweak compute_chunk_size() if you want different splitting heuristics based on your dataset. 🧳

performance_considerations:
  - Chunk Size Tuning: Large chunks may result in slower search but better context for answers. ⏳
  - Batch Inference: Consider batching multiple user queries if scaling is needed. 🗂️
  - GPU Deployment: If you embed very large PDFs, running on GPU machines speeds up HuggingFace models. 🖥️💨
  - Memory Management: FAISS saves indexes locally, enabling persistence between runs. 💾
  - Scaling Streamlit: Deploy Streamlit via services like Streamlit Sharing, AWS EC2, or Hugging Face Spaces for multi-user access. 🌍

license:
  description: "This project is licensed under the MIT License – see the LICENSE file for details. 📝"
