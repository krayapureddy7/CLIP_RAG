# RAG — Multimodal Retrieval-Augmented Generation

Short summary
- This repository implements a multimodal RAG prototype that extracts text and images from a PDF, creates embeddings (CLIP / transformers), stores them in a vector store, and performs retrieval + generation in a notebook-driven workflow.
- Primary interactive work is in the notebook: [multimodal_rag.ipynb](multimodal_rag.ipynb). See that file for end-to-end code and experiments.

Quick links
- Code entrypoint: [main.py](main.py) — contains [`main()`](main.py).
- Notebook: [multimodal_rag.ipynb](multimodal_rag.ipynb)
- Project config: [pyproject.toml](pyproject.toml)
- Python deps (text): [requirements.txt](requirements.txt)
- Sample PDF used: [Q1_2025-26_Fact_Sheet.pdf](Q1_2025-26_Fact_Sheet.pdf)
- Environment vars: [.env](.env) (do NOT commit real secrets)
- Other repo files: [.gitignore](.gitignore), [.python-version](.python-version), [uv.lock](uv.lock)

Requirements
- Python >= 3.10 (see [.python-version](.python-version))
- Dependencies listed in [pyproject.toml](pyproject.toml) and [requirements.txt](requirements.txt). Typical libs used in notebook:
  - langchain / langchain-core / langchain-community
  - transformers, torch
  - pymupdf (fitz), pillow
  - scikit-learn, numpy

Setup (recommended)
1. Create a venv and activate:
   python -m venv .venv
   Windows: .venv\Scripts\activate
   macOS/Linux: source .venv/bin/activate

2. Install dependencies:
   pip install -r requirements.txt
   or
   pip install -e .
   (See [pyproject.toml](pyproject.toml) for the declared dependencies.)

3. Add secrets to `.env` (DO NOT commit). Example:
   GOOGLE_API_KEY=YOUR_GOOGLE_API_KEY_HERE

Run
- For a minimal run:
  - Open and run the notebook [multimodal_rag.ipynb](multimodal_rag.ipynb) in Jupyter / VS Code.
- The repository contains a tiny script entrypoint:
  - [main.py](main.py) — run with:
    python main.py

What the notebook does (high level)
- Opens a PDF with PyMuPDF (fitz) and extracts text and images.
- Uses a CLIP/transformers model for multimodal embeddings.
- Splits text into chunks using a text splitter (in-notebook variable).
- Builds a vector store (FAISS via [langchain_community.vectorstores.FAISS] in the notebook).
- Performs cosine-similarity retrieval and then uses a chat / LLM layer for generation.

Files and purpose
- [main.py](main.py) — tiny script / example entrypoint (function [`main()`](main.py)).
- [multimodal_rag.ipynb](multimodal_rag.ipynb) — primary implementation and explorations.
- [Q1_2025-26_Fact_Sheet.pdf](Q1_2025-26_Fact_Sheet.pdf) — sample PDF used in the notebook.
- [pyproject.toml](pyproject.toml) — project metadata and dependencies.
- [requirements.txt](requirements.txt) — installation convenience.
- [.env](.env) — local environment variables (API keys). Keep private.
- [.gitignore](.gitignore) — ignores venv, caches, etc.
- [.python-version](.python-version) — target Python version used for the project.

Notes and best practices
- Keep API keys out of version control. Use `.env` locally and add it to `.gitignore`.
- The notebook contains model downloads and may require GPU / sufficient RAM for large models.
- If you plan to productionize, replace in-notebook experimentation with modular Python modules and unit tests.

Where to go next
- Inspect [multimodal_rag.ipynb](multimodal_rag.ipynb) to see how documents are parsed, how embeddings are created, and how retrieval is performed.
- Convert heavy notebook cells into reusable Python modules if you want CLI / service usage.