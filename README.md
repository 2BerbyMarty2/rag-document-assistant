# RAG Document Assistant
## Overview

- This project is a **Retrieval-Augmented Generation (RAG)** assistant designed to answer questions about a specific corpus of documents. It uses modern language models and vector search to provide contextually-aware answers based on provided data, such as detailed YouTube video metadata.
  
---
## Video Metadata (Example Dataset)
- **Video ID:** `sl9QP3gcWOQ`
- **Title:** Israel and Lebanon agree to implement ceasefire if Hezbollah stops attacks | BBC News
- **Description:** Short-form video description extracted from source
- **Duration:** 181 seconds (3:01)
- **Upload Date:** 20260604
- **Tags & Category:** BBC, news, world news, breaking news
---
## Channel Information
- **Channel Name:** BBC News
- **Channel ID:** (available in metadata)
- **Subscriber Count:** (available in metadata)
- **Verification Status:** (available in metadata)
---
## Engagement Metrics
- View count
- Like count
- Comment count
---
## Available Media Formats
- Multiple video quality options
- Audio-only formats
- File types (MP4, WebM, M4A)
- Resolution and codec details
- Download/stream URLs
- Storyboard thumbnail data
---
## Project Features
- Efficient Data Ingestion: Processes and chunks documents for embedding
- Advanced Embeddings: Uses `sentence-transformers/all-MiniLM-L6-v2`
- Fast Retrieval: FAISS vector store for similarity search
- Instruction-Tuned LLM: `qwen3-0.6b-instruct` for strong RAG performance
- Interactive UI: Streamlit-based web interface
---
## Technology Stack
- LLM Framework: LangChain
- Large Language Model: `qwen3-0.6b-instruct`
- Embedding Model: `sentence-transformers/all-MiniLM-L6-v2`
- Vector Store: FAISS (CPU)
- UI Framework: Streamlit
- Core Libraries: openai, pypdf, python-dotenv
---
## Project Structure

(venv) ➜  rag_document_assistant git:(main) ✗ tree -L 2
.
├── README.md
├── data
│   ├── clean_transcripts
│   └── meta_data_video_info.json
├── data_archive
│   ├── data
│   ├── meta_data_video_info.json
│   ├── output
│   ├── playlist_data.json
│   ├── playlist_data_two.jsonl
│   ├── raw_data
│   └── video_metadata.json
├── embeddings
├── evaluation
├── generation
├── help.txt
├── ingestion
├── main.py
├── models
│   └── qwen3-0.6b-base
├── notebooks
│   ├── data_processing.ipynb
│   ├── embedding_sample.ipynb
│   ├── model_test_one.ipynb
│   ├── model_test_two.ipynb
│   └── tests
├── requirements.txt
├── retrieval
├── utils
├── vectorstore
└── venv

---
##  Getting Started
### 1. Prerequisites
- Python 3.8+
- Git
---
### 2. Installation
Clone the repository:
```bash
git clone https://github.com/2BerbyMarty2/rag-document-assistant.git
cd rag-document-assistant

Create and activate virtual environment:

python3 -m venv venv
source venv/bin/activate
# Windows: venv\Scripts\activate

Install dependencies:

pip install -r requirements.txt

⸻

## Configuration

Create a .env file:

OPENAI_API_KEY="your_openai_api_key_here"

⸻

## Usage
# Not implimented yet

1. Place source documents (PDFs, JSON metadata, text files) into data_bucket/
2. Run ingestion script (if applicable) to build vector store
3. Start the application:


⸻
```
### Example Metadata Format

{
  "id": "sl9QP3gcWOQ",
  "url": "https://www.youtube.com/watch?v=sl9QP3gcWOQ",
  "title": "Israel and Lebanon agree to implement ceasefire if Hezbollah stops attacks | BBC News",
  "channel": "BBC News",
  "upload_date": "20260604",
  "tags": ["bbc", "bbc news", "news", "world news", "breaking news"],
  "view_count": 31459,
  "description": "Israel and Lebanon have agreed to renew their fragile ceasefire..."
}

⸻

### LLM Generation Parameters

* max_new_tokens: controls output length
* max_length: total sequence limit (usually replaced by max_new_tokens)
* temperature: randomness of output
* do_sample: enables sampling
* top_k: limits candidate tokens
* top_p: nucleus sampling threshold
* repetition_penalty: reduces repetition
* num_return_sequences: number of outputs
* eos_token_id: stop token
* pad_token_id: padding token

Recommended Settings for RAG

* Low temperature (0.1–0.3) → factual responses
* max_new_tokens: 256–512
* top_p: ~0.9
* repetition_penalty: ~1.1

⸻

### Model Configuration

* Planned LLM: qwen3-0.6b-base
* Current LLM: qwen3-0.6b-instruct (better for instruction following)
* Embedding Model: sentence-transformers/all-MiniLM-L6-v2

---

* data/ → Active dataset storage including cleaned transcripts and metadata used by the RAG pipeline
* data_bucket/ → Raw and experimental data dumps (old datasets, scraped data, intermediate outputs)
* embeddings/ → Scripts and logic for converting text chunks into vector embeddings
* vectorstore/ → Stores vector database/index (FAISS or similar) for fast similarity search
* ingestion/ → Handles loading, cleaning, and preprocessing of raw data into structured chunks
* retrieval/ → Implements search logic to retrieve relevant document chunks using embeddings
* generation/ → LLM interface and prompt handling for generating final answers
* models/ → Local or external model wrappers (LLMs like Qwen, embedding models, etc.)
* evaluation/ → Scripts for testing retrieval quality and RAG response performance
* utils/ → Helper functions (logging, config handling, file utilities, etc.)
* notebooks/ → Experimental Jupyter notebooks for testing embeddings, models, and workflows

