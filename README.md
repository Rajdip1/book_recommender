**Project Overview**

 - **Name**: Book Recommender (semantic + emotion-aware)
 - **Description**: A semantic book recommender that combines document embeddings and emotion signals to surface emotionally relevant book recommendations. The project includes a Gradio dashboard (`dashboard.py`), data CSVs used for recommendations, and several Jupyter notebooks for exploration and modeling.

<img width="1919" height="819" alt="Screenshot 2025-12-05 174452" src="https://github.com/user-attachments/assets/bd0f26ce-24aa-40a9-8c4c-36680a1289e8" />
<img width="1919" height="822" alt="Screenshot 2025-12-05 174541" src="https://github.com/user-attachments/assets/010e0e28-9062-4c6a-b873-b269f0a9f196" />
<img width="1919" height="826" alt="Screenshot 2025-12-05 174525" src="https://github.com/user-attachments/assets/10b37b26-02a0-4e6d-9238-2220a2a7b232" />


**Key Files**
- `dashboard.py`: Gradio app that runs a semantic recommender using HuggingFace sentence embeddings and a Chroma vector DB.
- `books_with_emotions.csv`, `books_with_categories.csv`, `cleaned_books.csv`: Datasets used by the project.
- `tagged_description.txt`: Text data used to build the embedding index.
- Notebooks: `data-exploration.ipynb`, `sentiment-analysis.ipynb`, `text-classification.ipynb`, `vector-search.ipynb` — for EDA and model experiments.

**Requirements**
- Use the provided `requirements.txt` to install Python dependencies:

```
python -m venv .venv
; .\.venv\Scripts\Activate.ps1
; pip install -r requirements.txt
```

**Running the Dashboard**

1. Ensure the virtual environment is active (see above).
2. If you rely on any environment variables, add them to a `.env` file in the repo root. `dashboard.py` calls `load_dotenv()`.
3. Start the app:

```
python dashboard.py
```

The dashboard uses a HuggingFace sentence-transformer (`sentence-transformers/all-MiniLM-L6-v2`) to compute embeddings and builds a Chroma vector store from `tagged_description.txt`. The app loads `books_with_emotions.csv` to provide metadata and emotional signals.

**Notebooks**
- Use the notebooks for exploration and to reproduce preprocessing, sentiment analysis, and vector search experiments. They contain the data-cleaning and modeling steps used to generate the datasets.

**Models Used**
- `sentence-transformers/all-MiniLM-L6-v2` — used via `HuggingFaceEmbeddings` (LangChain) to compute sentence embeddings for semantic search and the Gradio dashboard (`dashboard.py` and `vector-search.ipynb`).
- `bhadresh-savani/distilbert-base-uncased-emotion` — used with `transformers.pipeline("text-classification")` in `sentiment-analysis.ipynb` to infer emotions/sentiment from book descriptions.
- `typeform/distilbert-base-uncased-mnli` — used with `transformers.pipeline("zero-shot-classification")` in `text-classification.ipynb` for zero-shot topic/class labeling.

**Datasets & Outputs**
- The CSV files in the repo are the primary inputs for the dashboard. `tagged_description.txt` is used to build the vector index.

**Troubleshooting**
- If you get import errors for any `langchain_*` or community imports, verify package names on PyPI. The project imports community LangChain modules (e.g., `langchain_community`, `langchain_text_splitters`, `langchain_chroma`); if an import fails, try installing `langchain-community`, `langchain-text-splitters`, and `chromadb`.
- If embedding downloads fail, ensure you have internet access or have the model cached with `sentence-transformers`.
