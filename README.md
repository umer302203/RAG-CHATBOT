# 🤖 RAG Chatbot — Ask Questions from Your PDFs

[![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python&logoColor=white&style=for-the-badge)](https://python.org)
[![Gradio](https://img.shields.io/badge/Gradio-4.44.0-orange?logo=gradio&logoColor=white&style=for-the-badge)](https://gradio.app)
[![LangChain](https://img.shields.io/badge/LangChain-0.2.11-green?logo=langchain&style=for-the-badge)](https://langchain.com)
[![IBM Watsonx](https://img.shields.io/badge/IBM%20Watsonx-API-purple?logo=ibm&logoColor=white&style=for-the-badge)](https://www.ibm.com/watsonx)
[![Hugging Face](https://img.shields.io/badge/🤗-Spaces-yellow?style=for-the-badge)](https://huggingface.co)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)
[![Made with ❤️](https://img.shields.io/badge/Made%20with-❤️-red?style=for-the-badge)](https://www.linkedin.com/in/rana-umer-05a9a9359/)

---

<p align="center">
  <img src="https://media.giphy.com/media/3o7TKz6lqFm7XfeI4U/giphy.gif" width="350" alt="AI Robot reading documents"/>
  <br>
  <i>Your personal document assistant — powered by AI</i>
</p>

---

## 📌 What is This?

**Stop scrolling through hundreds of pages.**  
This **RAG Chatbot** lets you upload any PDF document and ask questions — it reads the document and gives you **precise, context-aware answers** in seconds.

Whether it's research papers, legal documents, technical manuals, or business reports — just upload and ask.

> 🚀 Built with **LangChain**, **IBM Watsonx**, **ChromaDB**, and **Gradio**.

---

## 🎬 Live Demo

Watch the chatbot in action — upload a PDF and ask questions instantly.

<div align="center">
  <iframe src="https://www.linkedin.com/embed/feed/update/urn:li:ugcPost:7482365771642429440?compact=1" height="450" width="100%" frameborder="0" allowfullscreen="" title="Embedded post" style="max-width: 600px; border-radius: 12px; box-shadow: 0 8px 30px rgba(0,0,0,0.2);"></iframe>
</div>

> *The video shows the complete flow: PDF upload → question → answer generation.*

---

## 🎯 Features

| Icon | Feature | Description |
|:----:|---------|-------------|
| 📄 | **Upload Any PDF** | Drag & drop or click to upload. Supports any text-based PDF. |
| 🧠 | **Smart Retrieval** | Uses **semantic search** (ChromaDB + embeddings) to find the most relevant context. |
| ⚡ | **LLM-Powered Answers** | Generates answers using **IBM Watsonx** model (`mistralai/mistral-medium-2505`). |
| 🗂️ | **Intelligent Chunking** | Splits text with `RecursiveCharacterTextSplitter` for optimal context windows. |
| 🔍 | **Similarity Search** | ChromaDB stores embeddings for lightning-fast retrieval. |
| 🖥️ | **Clean UI** | Simple, intuitive, and responsive interface — no coding required for end-users. |
| 🔒 | **Secure** | API keys stored as environment variables — never hardcoded. |

---

## 🧠 Architecture (How It Works)

```
╔═══════════════════════════════════════════════════════════════════════════╗
║                      🧠 RAG CHATBOT ARCHITECTURE                         ║
╚═══════════════════════════════════════════════════════════════════════════╝

   ┌─────────────┐    ┌─────────────┐    ┌─────────────────┐
   │  📄 Upload   │    │  📖 PDF     │    │  ✂️ Text        │
   │    PDF File  │───▶│   Loader    │───▶│   Splitter      │
   │   (Gradio)   │    │(PyPDFLoader)│    │  (Recursive)    │
   └─────────────┘    └─────────────┘    └────────┬────────┘
                                                    │
                                                    ▼
   ┌─────────────┐    ┌─────────────┐    ┌─────────────────┐
   │  💬 Answer   │    │  🔗 QA      │    │  🗄️ Vector      │
   │   Display    │◀───│   Chain     │◀───│   Store         │
   │   (Gradio)   │    │(RetrievalQA)│    │  (ChromaDB)     │
   └─────────────┘    └─────────────┘    └────────┬────────┘
                                                    │
                                                    ▼
                                            ┌─────────────────┐
                                            │  🧮 Embedding   │
                                            │    Model        │
                                            │  (IBM Watsonx)  │
                                            └─────────────────┘
```

### Data Flow — Step by Step

| Step | Component | What It Does |
|:----:|-----------|--------------|
| **1** | **Gradio UI** | User uploads a PDF file via drag & drop. |
| **2** | **PyPDFLoader** | Extracts raw text from the PDF document. |
| **3** | **RecursiveCharacterTextSplitter** | Splits text into ~1000-character chunks (with 50-character overlap for context). |
| **4** | **IBM Watsonx Embedding** | Converts each chunk into a numerical vector (`ibm/granite-embedding-278m-multilingual`). |
| **5** | **ChromaDB** | Stores vectors in a lightweight vector database for fast similarity search. |
| **6** | **Retriever** | When user asks a question, it fetches the top-k semantically similar chunks. |
| **7** | **RetrievalQA Chain** | Passes the relevant chunks + user question to the LLM. |
| **8** | **IBM Watsonx LLM** | Generates a concise, context-aware answer (`mistralai/mistral-medium-2505`). |
| **9** | **Gradio UI** | Displays the answer to the user. |

---

## 🛠️ Tech Stack

| Category | Tool | Badge |
|----------|------|-------|
| **Backend** | Python 3.11 | ![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python) |
| **PDF Loader** | PyPDFLoader (langchain-community) | ![LangChain](https://img.shields.io/badge/LangChain-Community-green) |
| **Text Splitter** | RecursiveCharacterTextSplitter | ![LangChain](https://img.shields.io/badge/LangChain-Splitter-orange) |
| **Vector Store** | ChromaDB | ![ChromaDB](https://img.shields.io/badge/ChromaDB-1.5.9-yellow) |
| **Embeddings** | IBM Watsonx (`ibm/granite-embedding-278m-multilingual`) | ![IBM](https://img.shields.io/badge/IBM-Watsonx-purple) |
| **LLM** | IBM Watsonx (`mistralai/mistral-medium-2505`) | ![IBM](https://img.shields.io/badge/IBM-Watsonx-purple) |
| **Orchestration** | LangChain + langchain-ibm | ![LangChain](https://img.shields.io/badge/LangChain-0.2.11-green) |
| **Frontend** | Gradio | ![Gradio](https://img.shields.io/badge/Gradio-4.44.0-orange) |

---

## 📦 Project Structure

```
rag-chatbot/
│
├── 📄 app.py                 # Main application code
│   ├── 🔐 IBM Watsonx LLM
│   ├── 🧮 IBM Watsonx Embeddings
│   ├── 📖 PDF Loader
│   ├── ✂️ Text Splitter
│   ├── 🗄️ ChromaDB Vector Store
│   ├── 🔗 RetrievalQA Chain
│   └── 🖥️ Gradio UI
│
├── 📦 requirements.txt       # Python dependencies
├── 📖 README.md              # This documentation
├── 🎬 demo.mp4               # Demo video
└── 🔒 .gitignore
```

---

## 🚀 How to Use — Step by Step

### Prerequisites

| Requirement | Details |
|-------------|---------|
| **Python** | 3.11 or higher |
| **IBM Cloud Account** | Free tier available at [IBM Cloud](https://cloud.ibm.com/) |
| **IBM Watsonx API Key** | Generate from [IBM Watsonx](https://dataplatform.cloud.ibm.com/) |

### Step 1: Clone the Repository

```bash
git clone https://github.com/yourusername/rag-chatbot.git
cd rag-chatbot
```

### Step 2: Create Virtual Environment

```bash
python3.11 -m venv my_env
source my_env/bin/activate   # Linux/Mac
# my_env\Scripts\activate    # Windows
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 4: Set IBM Watsonx Credentials

```bash
# Linux/Mac
export IBM_API_KEY="your-api-key-here"
export IBM_PROJECT_ID="skills-network"

# Windows
set IBM_API_KEY=your-api-key-here
set IBM_PROJECT_ID=skills-network
```

> 🔒 **Important:** Never hardcode credentials in your code. Always use environment variables or platform secrets.

### Step 5: Run the Application

```bash
python app.py
```

### Step 6: Interact with the App

1. Open your browser and go to `http://localhost:7860`
2. Upload a PDF file (drag & drop or click to upload)
3. Type your question in the textbox
4. Click **Submit** — get your answer in seconds!

---

## 📄 Code Walkthrough

### 1. Import Libraries

```python
from ibm_watsonx_ai.foundation_models import ModelInference
from ibm_watsonx_ai.metanames import GenTextParamsMetaNames as GenParams
from ibm_watsonx_ai.metanames import EmbedTextParamsMetaNames
from langchain_ibm import WatsonxLLM, WatsonxEmbeddings
from langchain.text_splitter import RecursiveCharacterTextSplitter
from langchain_community.vectorstores import Chroma
from langchain_community.document_loaders import PyPDFLoader
from langchain.chains import RetrievalQA
import gradio as gr
```

### 2. Initialize LLM (IBM Watsonx)

```python
def get_llm():
    model_id = 'mistralai/mistral-medium-2505'
    parameters = {
        GenParams.MAX_NEW_TOKENS: 256,
        GenParams.TEMPERATURE: 0.5,
    }
    watsonx_llm = WatsonxLLM(
        model_id=model_id,
        url="https://us-south.ml.cloud.ibm.com",
        project_id="skills-network",
        params=parameters,
    )
    return watsonx_llm
```

**What This Does:**  
Creates a connection to IBM Watsonx and loads the Mistral Medium model.  
- `MAX_NEW_TOKENS: 256` — limits response length to 256 tokens
- `TEMPERATURE: 0.5` — balances creativity vs. determinism (lower = more deterministic)

### 3. Load PDF Document

```python
def document_loader(file):
    loader = PyPDFLoader(file.name)
    loaded_document = loader.load()
    return loaded_document
```

**What This Does:**  
Takes the uploaded PDF file path and loads its content as text using `PyPDFLoader`.

### 4. Split Text into Chunks

```python
def text_splitter(data):
    text_splitter = RecursiveCharacterTextSplitter(
        chunk_size=1000,
        chunk_overlap=50,
        length_function=len,
    )
    chunks = text_splitter.split_documents(data)
    return chunks
```

**What This Does:**  
- Divides the document into chunks of ~1000 characters
- Overlaps chunks by 50 characters to maintain context continuity
- This is critical for retrieving relevant passages

### 5. Embeddings (IBM Watsonx)

```python
def watsonx_embedding():
    embed_params = {
        EmbedTextParamsMetaNames.TRUNCATE_INPUT_TOKENS: 3,
        EmbedTextParamsMetaNames.RETURN_OPTIONS: {"input_text": True},
    }
    watsonx_embedding = WatsonxEmbeddings(
        model_id="ibm/granite-embedding-278m-multilingual",
        url="https://us-south.ml.cloud.ibm.com",
        project_id="skills-network",
        params=embed_params,
    )
    return watsonx_embedding
```

**What This Does:**  
Uses IBM's Granite multilingual embedding model to convert text chunks into numerical vectors.

### 6. Vector Database (ChromaDB)

```python
def vector_database(chunks):
    embedding_model = watsonx_embedding()
    vectordb = Chroma.from_documents(chunks, embedding_model)
    return vectordb
```

**What This Does:**  
- Takes the text chunks
- Generates embeddings using the embedding model
- Stores them in ChromaDB for similarity search

### 7. QA Chain

```python
def retriever_qa(file, query):
    llm = get_llm()
    retriever_obj = retriever(file)
    qa = RetrievalQA.from_chain_type(
        llm=llm, 
        chain_type="stuff", 
        retriever=retriever_obj, 
        return_source_documents=False
    )
    response = qa.invoke(query)
    return response['result']
```

**What This Does:**  
- Takes the user's question
- Finds relevant chunks using the retriever
- Sends chunks + question to the LLM
- Returns the generated answer

### 8. Gradio UI

```python
rag_application = gr.Interface(
    fn=retriever_qa,
    allow_flagging="never",
    inputs=[
        gr.File(label="Upload PDF File", file_types=['.pdf'], type="filepath"),
        gr.Textbox(label="Input Query", lines=2, placeholder="Type your question here...")
    ],
    outputs=gr.Textbox(label="Output"),
    title="RAG Chatbot",
    description="Upload a PDF document and ask any question."
)

rag_application.launch(server_name="0.0.0.0", server_port=7860, share=True)
```

**What This Does:**  
Creates a web interface where users can upload PDFs, ask questions, and see answers.

---

## 🐛 Troubleshooting

| Error | Cause | Solution |
|-------|-------|----------|
| **`401 Unauthorized`** | Invalid IBM API key | Check your API key and ensure it's correct. Regenerate if needed. |
| **`Model ibm/slate-125m... not supported`** | Wrong embedding model name | Use `ibm/granite-embedding-278m-multilingual` (already fixed in code). |
| **`File not found`** | PDF path incorrect | Ensure the file exists and path is correct. |
| **`Gradio share link not working`** | Expired share link | Use `share=True` for temporary link, but it expires after 72 hours. |
| **`ModuleNotFoundError: No module named 'langchain.chains'`** | Wrong LangChain version | Use `langchain==0.2.11` (specified in requirements). |

---

## 📋 Requirements (`requirements.txt`)

```
gradio==4.44.0
jinja2==3.1.2
fastapi==0.110.0
starlette==0.36.3
huggingface_hub==0.23.5
ibm-watsonx-ai==1.1.2
langchain==0.2.11
langchain-community==0.2.10
langchain-ibm==0.1.11
chromadb==0.4.24
pypdf==4.3.1
pydantic==2.9.1
```

---

## 🚢 Deployment (Optional — Hugging Face Spaces)

1. Go to [huggingface.co/spaces](https://huggingface.co/spaces)
2. Click **"Create new Space"**
3. Select **"Gradio"** as the SDK
4. Upload:
   - `app.py`
   - `requirements.txt`
   - `README.md`
   - `demo.mp4`
5. In **Settings > Repository Secrets**, add:
   - `IBM_API_KEY`
   - `IBM_PROJECT_ID` (usually `skills-network`)
6. The Space will auto-build and deploy.

---

## 🤝 Contributing

Contributions are welcome! Here's how:

1. **Fork** the repository
2. Create your feature branch (`git checkout -b feature/awesome`)
3. Commit your changes (`git commit -m 'Add awesome feature'`)
4. Push to the branch (`git push origin feature/awesome`)
5. Open a **Pull Request**

---

## 📄 License

This project is distributed under the **MIT License** — free to use, modify, and distribute.

---

## 🙏 Acknowledgments

| Resource | Purpose |
|----------|---------|
| [IBM Watsonx](https://www.ibm.com/watsonx) | LLM and Embeddings |
| [LangChain](https://langchain.com/) | Orchestration framework |
| [Gradio](https://gradio.app/) | Web UI |
| [ChromaDB](https://www.trychroma.com/) | Vector database |
| [Hugging Face](https://huggingface.co/) | Hosting platform |

---

## 📬 Connect with Me

Feel free to reach out for collaboration, feedback, or just to say hi!

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/rana-umer-05a9a9359/)

---

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&height=150&section=footer&fontSize=30&fontColor=white&text=RAG%20Chatbot"/>
</p>

> Built with ☕ and 💻 by [Rana Umer](https://www.linkedin.com/in/rana-umer-05a9a9359/)
