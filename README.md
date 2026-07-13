# 🤖 RAG Chatbot — Ask Questions from Your PDFs

[![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python&logoColor=white)](https://python.org)
[![Gradio](https://img.shields.io/badge/Gradio-6.20.0-orange?logo=gradio&logoColor=white)](https://gradio.app)
[![LangChain](https://img.shields.io/badge/LangChain-1.3.1-green?logo=langchain)](https://langchain.com)
[![Google Gemini](https://img.shields.io/badge/Google%20Gemini-API-yellow?logo=google&logoColor=white)](https://ai.google.dev)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Made with ❤️](https://img.shields.io/badge/Made%20with-❤️-red)](https://www.linkedin.com/in/rana-umer-05a9a9359/)

---

## 📌 Overview

**Stop scrolling through hundreds of PDFs.**  
This **RAG Chatbot** lets you upload any PDF and ask questions — it reads the document and gives you precise, context-aware answers in seconds.

<p align="center">
  <img src="https://media.giphy.com/media/3o7TKz6lqFm7XfeI4U/giphy.gif" width="300" alt="AI Robot reading documents"/>
</p>

> 🚀 Built with **LangChain**, **Google Gemini**, **ChromaDB**, and **Gradio** — deployed on **Hugging Face Spaces**.

---

## 🎯 Features

| Feature | Description |
|---------|-------------|
| 📄 **Upload Any PDF** | Drag & drop or click to upload. Supports any text-based PDF. |
| 🧠 **Smart Retrieval** | Uses **semantic search** to find the most relevant context from your document. |
| ⚡ **LLM-Powered Answers** | Generates answers using **Google Gemini 1.5 Flash** — fast and accurate. |
| 🗂️ **Intelligent Chunking** | Splits text with `RecursiveCharacterTextSplitter` for optimal context windows. |
| 🔍 **Similarity Search** | ChromaDB stores embeddings for lightning-fast retrieval. |
| 🖥️ **Clean Gradio UI** | Simple, intuitive, and responsive interface — no coding required for end-users. |
| ☁️ **Deployed on Cloud** | Hosted on **Hugging Face Spaces** for permanent availability. |

---

## 🧠 Architecture (Under the Hood)

Below is the data flow of the application — from PDF upload to answer delivery:

```
+-------------------+     +-------------------+     +-------------------+
|   User Uploads    | --> |   PDF Loader      | --> |   Text Splitter   |
|      PDF          |     |   (PyPDFLoader)   |     |   (Recursive)     |
+-------------------+     +-------------------+     +-------------------+
                                                          |
                                                          v
+-------------------+     +-------------------+     +-------------------+
|   Answer Output   | <-- |   RetrievalQA     | <-- |   Vector Store    |
|   (Gradio UI)     |     |   Chain           |     |   (ChromaDB)      |
+-------------------+     +-------------------+     +-------------------+
                                                          |
                                                          v
                                                +-------------------+
                                                |   Embeddings      |
                                                |   (Gemini)        |
                                                +-------------------+
```

**Step-by-step breakdown:**

1. **Upload** — User selects a PDF via Gradio's file uploader.
2. **Load** — `PyPDFLoader` extracts raw text from the PDF.
3. **Split** — `RecursiveCharacterTextSplitter` divides text into ~1000-character chunks (with 50-character overlap for context continuity).
4. **Embed** — Chunks are converted into numerical vectors using Google Gemini's `embedding-001` model.
5. **Store** — Vectors are stored in **ChromaDB**, a lightweight vector database.
6. **Query** — User asks a question; the retriever fetches the top-k semantically similar chunks.
7. **Generate** — The `RetrievalQA` chain passes the chunks + question to **Gemini 1.5 Flash** LLM, which generates a concise, context-aware answer.
8. **Display** — Answer is shown in the Gradio interface.

---

## 🎬 Demo Video

See the chatbot in action — upload a PDF and ask questions instantly.

<video controls autoplay loop muted playsinline width="100%" style="max-width: 800px; border-radius: 16px; box-shadow: 0 8px 30px rgba(0,0,0,0.2);">
  <source src="https://huggingface.co/spaces/Umer78786/RAG_Chatbot/resolve/main/demo.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

> *If the video doesn't load, you can also view it directly in the repository files.*

---

## 🛠️ Tech Stack

| Category | Tool |
|----------|------|
| **Backend** | Python 3.11 |
| **PDF Loader** | `PyPDFLoader` (langchain-community) |
| **Text Splitter** | `RecursiveCharacterTextSplitter` |
| **Vector Store** | ChromaDB |
| **Embeddings** | Google Gemini (`models/embedding-001`) |
| **LLM** | Google Gemini (`gemini-1.5-flash`) |
| **Orchestration** | LangChain + LangChain Classic |
| **Frontend** | Gradio |
| **Deployment** | Hugging Face Spaces (free tier) |

---

## 📦 Installation (Local)

Follow these steps to run the bot on your local machine:

```bash
# 1. Clone the repository
git clone https://github.com/yourusername/rag-chatbot.git
cd rag-chatbot

# 2. Create a virtual environment
python3.11 -m venv my_env
source my_env/bin/activate   # Linux/Mac
# my_env\Scripts\activate    # Windows

# 3. Install dependencies
pip install -r requirements.txt

# 4. Set your Google Gemini API key (get one from https://ai.google.dev)
export GOOGLE_API_KEY="your-api-key-here"   # Linux/Mac
# set GOOGLE_API_KEY=your-api-key-here      # Windows

# 5. Run the application
python app.py
```

> 🔒 **Security:** Never hardcode API keys in your code. Always use environment variables or platform secrets.

---

## 📁 Project Structure

```
rag-chatbot/
├── app.py                 # Main application logic
├── requirements.txt       # Python dependencies
├── README.md              # This documentation
├── demo.mp4               # Demo video
└── .gitignore
```

---

## 🐛 Troubleshooting

| Error | Solution |
|-------|----------|
| `ModuleNotFoundError: No module named 'langchain.chains'` | Install `langchain-classic` and update import to `from langchain_classic.chains import RetrievalQA` |
| `TypeError: Blocks.launch() got an unexpected keyword argument 'ssr'` | Remove `ssr=False`; use `ssr_mode=False` for Gradio 6 or just omit it. |
| `ValueError: GOOGLE_API_KEY environment variable not set!` | Set the API key as an environment variable or in Hugging Face Secrets. |
| `gradio-community` build conflict | Remove any pinned `gradio==...` from `requirements.txt`; let Hugging Face use its default version. |
| PDF upload fails | Ensure the PDF is not corrupted or password-protected. Try a smaller file first. |

---

## 🚢 Deployment (Hugging Face Spaces)

1. Go to [huggingface.co/spaces](https://huggingface.co/spaces) and create a new Space.
2. Select **"Gradio"** as the SDK.
3. Upload `app.py`, `requirements.txt`, `demo.mp4`, and this `README.md`.
4. In the **Settings** tab, add a **Repository Secret** named `GOOGLE_API_KEY` with your Gemini API key.
5. The Space will automatically build and deploy your app.

---

## 🤝 Contributing

Contributions are welcome! If you'd like to improve the project:

1. Fork the repository.
2. Create a new branch (`git checkout -b feature/improvement`).
3. Commit your changes (`git commit -m 'Add some improvement'`).
4. Push to the branch (`git push origin feature/improvement`).
5. Open a Pull Request.

---

## 📄 License

This project is distributed under the **MIT License**. See the `LICENSE` file for more details.

---

## 🙏 Acknowledgments

- [Google Gemini](https://ai.google.dev/) for providing the LLM and embedding models.
- [LangChain](https://langchain.com/) for the powerful orchestration framework.
- [Gradio](https://gradio.app/) for making UI development effortless.
- [Hugging Face](https://huggingface.co/) for the free hosting platform.

---

## 📬 Connect with Me

Feel free to reach out for collaboration, feedback, or just to say hi!

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/rana-umer-05a9a9359/)

---

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&height=100&section=footer"/>
</p>

> Built with ☕ and 💻 by [Rana Umer](https://www.linkedin.com/in/rana-umer-05a9a9359/)
