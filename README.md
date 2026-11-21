# AI-Powered PDF Assistant

A Python-based PDF question-answering application built with **Retrieval-Augmented Generation (RAG)**. Users can upload PDF documents and ask questions in natural language. The application retrieves relevant passages from the document and passes them to Google's Gemini model to generate context-based answers.

> **Project status:** This repository is a modified learning project based on the [Ask to Zuzu — PDF Q&A Chatbot](https://github.com/aankitsharma/ask-to-zuzu-rag-chatbot). The original project is credited here. Before redistributing its source code, check the original author's permission and any applicable licence terms. Document your own changes in this repository.

## Features

- Upload one or more PDF documents.
- Extract text from PDFs using PyMuPDF.
- Split extracted text into overlapping chunks.
- Generate text embeddings using Google's Gemini embedding model.
- Store and search embeddings with FAISS.
- Retrieve relevant document chunks for a user's question.
- Generate an answer using Gemini with the retrieved text as context.
- Save and reload the FAISS index and text chunks to avoid processing the same documents again.

## Tech stack

| Component | Technology |
|---|---|
| Programming language | Python |
| User interface | Streamlit |
| LLM and embeddings | Google Gemini API |
| Vector search | FAISS |
| Text chunking | LangChain |
| PDF text extraction | PyMuPDF (`fitz`) |
| Environment configuration | `python-dotenv` |

## How it works

1. **PDF upload:** The user uploads one or more PDF files.
2. **Text extraction:** PyMuPDF extracts text from the uploaded documents.
3. **Chunking:** LangChain's `RecursiveCharacterTextSplitter` divides the text into smaller, overlapping chunks.
4. **Embedding generation:** Gemini converts each chunk into a numerical vector (embedding).
5. **Indexing:** FAISS stores the vectors so that similar content can be found efficiently.
6. **Question retrieval:** The user's question is embedded and FAISS retrieves the most relevant chunks.
7. **Answer generation:** Gemini receives the question and retrieved context and generates a response.

```text
PDF files
   |
   v
Extract text (PyMuPDF)
   |
   v
Split text into chunks (LangChain)
   |
   v
Generate embeddings (Gemini)
   |
   v
Store vectors (FAISS)
   |
   v
User asks a question
   |
   v
Retrieve relevant chunks (FAISS)
   |
   v
Generate a context-based answer (Gemini)
   |
   v
Display answer in Streamlit
```

## Project structure

```text
AI-Powered-PDF-Assistant/
├── app.py
├── utils/
│   ├── pdf_reader.py
│   ├── chunking.py
│   ├── embedding.py
│   ├── vector_store.py
│   ├── retriever.py
│   ├── storage.py
│   └── llm.py
├── step1_pdf_reader.py
├── step2_chunking.py
├── step3_embedding.py
├── step4_vector_store.py
├── step5_retriever.py
├── step6_rag.py
├── step7_build_index.py
├── step8_chat.py
├── requirements.txt
├── .env.example
└── sample.pdf
```

*This structure reflects the source README. Check the actual files in your local copy and update this section if the folder or filenames differ.*

## Getting started

### 1. Clone your repository

After creating your own GitHub repository, use its URL here:

```bash
git clone https://github.com/YOUR-GITHUB-USERNAME/YOUR-REPOSITORY-NAME.git
cd YOUR-REPOSITORY-NAME
```

### 2. Create and activate a virtual environment

**Windows:**

```bash
python -m venv .venv
.venv\Scripts\activate
```

**macOS / Linux:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure the Gemini API key

Create a `.env` file in the project root. Use the variable name expected by the application:

```env
GOOGLE_API_KEY=your_gemini_api_key_here
```

Get an API key from [Google AI Studio](https://aistudio.google.com/).

**Security:** Never commit `.env` or expose your API key. Ensure `.env` is listed in `.gitignore`. Keep `.env.example` as a template containing only a placeholder value.

### 5. Run the application

```bash
streamlit run app.py
```

Streamlit will print a local URL in the terminal, usually `http://localhost:8501`.

## Learning the RAG pipeline

The repository also includes individual scripts that demonstrate the pipeline in stages:

| Script | Concept |
|---|---|
| `step1_pdf_reader.py` | Extracting text from PDFs |
| `step2_chunking.py` | Splitting text into overlapping chunks |
| `step3_embedding.py` | Converting text into embeddings |
| `step4_vector_store.py` | Creating a FAISS vector index |
| `step5_retriever.py` | Finding relevant chunks |
| `step6_rag.py` | Combining retrieval and generation |
| `step7_build_index.py` | Building and saving the index |
| `step8_chat.py` | Querying the saved index from the terminal |

Run an individual script from the project root, for example:

```bash
python step1_pdf_reader.py
```

Check each script's code and required inputs before running it.

## Current limitations

- The application requires internet access to call the Gemini API.
- Gemini API availability, quotas and pricing depend on the account and current Google terms.
- Answers can still be incorrect or incomplete; retrieved context does not guarantee factual accuracy.
- Scanned PDFs may require OCR if they do not contain selectable text.
- The quality of retrieval depends on the extracted text, chunking settings and embedding model.

## Possible improvements

- Display the PDF page numbers or source passages used for each answer.
- Add conversation history for follow-up questions.
- Support DOCX and TXT files.
- Add validation for file type, file size and empty PDFs.
- Deploy the application using Streamlit Community Cloud.

## Author

**Prasanna Kumar Rout**

This is a learning and portfolio project. The original implementation that this work is based on is credited below. Add links to your GitHub profile and document the features you personally implement before presenting the project as your own modified work.

## Acknowledgements

- Original reference project: [Ask to Zuzu — PDF Q&A Chatbot](https://github.com/aankitsharma/ask-to-zuzu-rag-chatbot) by Aankit Sharma.
- [Google Gemini API](https://ai.google.dev/)
- [Streamlit](https://streamlit.io/)
- [FAISS](https://github.com/facebookresearch/faiss)
- [LangChain](https://www.langchain.com/)
- [PyMuPDF](https://pymupdf.readthedocs.io/)
