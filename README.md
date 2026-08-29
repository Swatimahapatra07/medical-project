# 🩺 AI Medical Chatbot

An AI-powered Medical Chatbot that uses **Retrieval-Augmented Generation (RAG)** to provide context-based answers to medical questions. The application uses **Hugging Face embeddings, FAISS vector search, LangChain, and Groq LLM** to retrieve relevant medical information and generate answers through a Flask web interface.

---

## 📌 Project Overview

The **AI Medical Chatbot** is a web-based application designed to answer medical-related questions using information retrieved from a medical knowledge base.

Instead of directly asking the Large Language Model to generate an answer, the system first searches a medical document for relevant information. The retrieved information is then provided to the LLM as context to generate the final response.

The project follows a **Retrieval-Augmented Generation (RAG)** architecture.

### Basic Workflow

```text
Medical PDF
     ↓
Document Loading
     ↓
Text Splitting
     ↓
Hugging Face Embeddings
     ↓
FAISS Vector Database
     ↓
User Question
     ↓
Similarity Search
     ↓
Relevant Medical Context
     ↓
Groq LLM
     ↓
Generated Answer
     ↓
Flask Web Interface
```

---

## ✨ Features

- 🩺 Medical question-answering chatbot
- 📚 PDF-based medical knowledge retrieval
- 🔎 Semantic similarity search
- 🗄️ FAISS vector database
- 🤗 Hugging Face Sentence Transformer embeddings
- 🤖 Groq Large Language Model
- 🔗 Retrieval-Augmented Generation (RAG)
- 🌐 Flask-based web application
- 💬 Interactive chatbot interface
- 🧹 Clear chat functionality
- 📝 Application logging
- ⚠️ Custom exception handling
- 🔐 Environment-based API key management

---

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| Flask | Web application framework |
| LangChain | RAG and LLM application framework |
| LangChain Community | Document and vector store integrations |
| LangChain Hugging Face | Hugging Face embedding integration |
| Hugging Face | Text embeddings |
| Sentence Transformers | Semantic text representation |
| FAISS | Vector similarity search |
| Groq | Large Language Model API |
| PyPDF | PDF document processing |
| HTML | Web interface |
| CSS | User interface styling |
| python-dotenv | Environment variable management |

---

## 🧠 What is RAG?

**Retrieval-Augmented Generation (RAG)** combines information retrieval with Large Language Models.

In this project, the RAG pipeline works as follows:

1. The medical PDF is loaded.
2. The document is divided into smaller text chunks.
3. Each text chunk is converted into an embedding.
4. The embeddings are stored in a FAISS vector database.
5. When a user asks a question, the question is converted into an embedding.
6. FAISS searches for the most relevant information.
7. The retrieved context is passed to the Groq LLM.
8. The LLM generates the final answer based on the retrieved context.
9. The answer is displayed on the Flask web interface.

---

## 🏗️ System Architecture

```text
                    ┌──────────────────────┐
                    │     Medical PDF      │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │   Document Loader    │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │    Text Splitting     │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Hugging Face         │
                    │ Embedding Model      │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │    FAISS Vector      │
                    │      Database        │
                    └──────────┬───────────┘
                               │
                               │
                ┌──────────────┘
                │
                ▼
       ┌──────────────────────┐
       │    User Question     │
       └──────────┬───────────┘
                  │
                  ▼
       ┌──────────────────────┐
       │ Similarity Search    │
       │       FAISS          │
       └──────────┬───────────┘
                  │
                  ▼
       ┌──────────────────────┐
       │ Relevant Medical     │
       │       Context        │
       └──────────┬───────────┘
                  │
                  ▼
       ┌──────────────────────┐
       │      Groq LLM        │
       └──────────┬───────────┘
                  │
                  ▼
       ┌──────────────────────┐
       │   Generated Answer   │
       └──────────┬───────────┘
                  │
                  ▼
       ┌──────────────────────┐
       │   Flask Web UI       │
       └──────────────────────┘
```

---

## 📂 Project Structure

```text
medical project/
│
├── app/
│   ├── application.py
│   │
│   ├── common/
│   │   ├── custom_exception.py
│   │   ├── logger.py
│   │   └── __init__.py
│   │
│   ├── components/
│   │   ├── data_loader.py
│   │   ├── embedding.py
│   │   ├── llm.py
│   │   ├── load_pdf.py
│   │   ├── retriever.py
│   │   ├── vector_store.py
│   │   └── __init__.py
│   │
│   ├── config/
│   │   ├── config.py
│   │   └── __init__.py
│   │
│   └── templates/
│       └── index.html
│
├── data/
│   └── Medical PDF
│
├── vectorstore/
│   └── db_faiss/
│       ├── index.faiss
│       └── index.pkl
│
├── .env
├── .gitignore
├── req.txt
├── setup.py
└── README.md
```

---

# ⚙️ How the Project Works

## 1. Medical Document Loading

The project uses a medical PDF as the primary knowledge source.

The document is loaded and prepared for further processing.

```text
Medical PDF
     ↓
PDF Loader
     ↓
Documents
```

---

## 2. Text Splitting

Large documents are divided into smaller chunks.

This makes it easier for the retrieval system to find the relevant information for a particular question.

The project uses text chunks with an overlap so that important information is not lost between chunks.

```text
Large Medical Document
          ↓
     Text Splitting
          ↓
 ┌────────┬────────┬────────┐
 │Chunk 1 │Chunk 2 │Chunk 3 │
 └────────┴────────┴────────┘
```

---

## 3. Hugging Face Embeddings

The project uses the Sentence Transformer model:

```text
sentence-transformers/all-MiniLM-L6-v2
```

The model converts text into numerical vectors.

For example:

```text
Medical Text
     ↓
Embedding Model
     ↓
Numerical Vector
```

These vectors allow the system to compare the semantic similarity between the user's question and the medical information.

---

## 4. FAISS Vector Database

The generated embeddings are stored in a **FAISS vector database**.

FAISS is used to perform efficient similarity searches.

When a user asks a question, the system searches the vector database for the most relevant medical information.

```text
User Question
      ↓
Question Embedding
      ↓
FAISS Similarity Search
      ↓
Relevant Medical Information
```

---

## 5. RetrievalQA Chain

The project uses LangChain to connect the retriever and the Large Language Model.

The overall process is:

```text
User Question
      ↓
Retriever
      ↓
Relevant Context
      ↓
Prompt
      ↓
Groq LLM
      ↓
Final Answer
```

The retrieved medical context is used to provide the LLM with information related to the user's question.

---

## 6. Groq LLM

The chatbot uses a Groq-hosted Large Language Model to generate responses.

The Groq API key is stored in the `.env` file and loaded through environment variables.

Example:

```text
GROQ_API_KEY=your_groq_api_key
```

The API key should never be written directly inside the Python source code or committed to GitHub.

---

## 7. Flask Web Application

Flask provides the web interface for the chatbot.

The application runs locally using:

```bash
python -m app.application
```

The application is available at:

```text
http://127.0.0.1:5000
```

---

# 🚀 Installation and Setup

## Prerequisites

Before running the project, make sure you have:

- Python 3.10 or higher
- VS Code
- Git
- Internet connection
- Groq API key

---

## 1. Clone the Repository

Clone the project from GitHub:

```bash
git clone https://github.com/Swatimahapatra07/medical-project.git
```

Move into the project directory:

```bash
cd medical-project
```

---

## 2. Create a Virtual Environment

Create a Python virtual environment:

```bash
python -m venv medical
```

Activate it on Windows:

```bash
medical\Scripts\activate
```

After activation, the terminal should show:

```text
(medical)
```

---

## 3. Install Dependencies

Install the required Python packages:

```bash
pip install -r req.txt
```

---

# 🔑 Configure the Groq API Key

Create a `.env` file in the root directory of the project.

```text
GROQ_API_KEY=your_groq_api_key
```

Replace `your_groq_api_key` with your actual Groq API key.

### Important

Do not upload `.env` to GitHub.

The `.gitignore` file should contain:

```gitignore
.env
```

---

# 📚 Add the Medical Dataset

The medical PDF should be placed inside:

```text
data/
```

For example:

```text
data/
└── medical_book.pdf
```

If the `data/` folder is excluded from GitHub, users who clone the repository must provide the required medical PDF themselves.

---

# 🗄️ Create the FAISS Vector Store

If the FAISS vector database is not included in the repository, create it from the medical PDF using the project's data-processing component.

Run:

```bash
python -m app.components.data_loader
```

The process will perform:

```text
Medical PDF
     ↓
Load Documents
     ↓
Split Documents
     ↓
Generate Embeddings
     ↓
Create FAISS Index
```

The vector database will be generated under:

```text
vectorstore/
```

---

# ▶️ Run the Application

After completing the setup, run:

```bash
python -m app.application
```

You should see:

```text
Running on http://127.0.0.1:5000
```

Open your browser and visit:

```text
http://127.0.0.1:5000
```

The Medical Chatbot interface will open.

---

# 💬 Example Questions

You can ask questions such as:

```text
What is diabetes?
```

```text
What are the symptoms of anemia?
```

```text
What causes hypertension?
```

```text
What are the symptoms of asthma?
```

```text
What is the treatment for common cold?
```

The chatbot retrieves relevant information from the medical knowledge base and generates a response using the LLM.

---

# 🧪 Logging and Exception Handling

The project includes logging functionality to monitor application operations.

Logging is implemented using:

```text
app/common/logger.py
```

Custom exception handling is implemented using:

```text
app/common/custom_exception.py
```

The application logs important operations such as:

```text
Loading vector store
Initializing Hugging Face embedding model
Loading FAISS
Loading Groq LLM
Creating QA chain
Processing user queries
```

---

# 🔐 Security

The project uses environment variables to protect sensitive information.

The Groq API key is stored in:

```text
.env
```

and accessed through the application configuration.

### Never commit:

```text
.env
```

to GitHub.

If an API key is accidentally uploaded to GitHub, revoke or rotate the key immediately.

---

# 🚫 Git Ignore

The project uses a `.gitignore` file to prevent unnecessary and sensitive files from being uploaded.

Recommended `.gitignore`:

```gitignore
# Virtual Environments
medical/
venv/
env/

# Python Cache
__pycache__/
*.pyc

# Environment Variables
.env

# Data and Vector Stores
vectorstore/
data/

# Logs
logs/

# Code Runner temporary files
tempCodeRunnerFile.py
```

---

# ⚠️ Important Note About `data/` and `vectorstore/`

The current `.gitignore` excludes:

```text
data/
vectorstore/
```

Therefore, these directories will not be uploaded to GitHub.

After cloning the repository, the user will need to:

1. Add the required medical PDF to `data/`.
2. Generate the FAISS vector database.
3. Run the Flask application.

This keeps the GitHub repository smaller and avoids uploading the source medical document unnecessarily.

---

# 🩺 Medical Disclaimer

This project is developed for **educational and demonstration purposes only**.

The chatbot does not replace professional medical advice, diagnosis, or treatment.

Information provided by the chatbot should not be considered a medical diagnosis.

For medical concerns, users should consult a qualified healthcare professional.

In an emergency, contact the appropriate emergency medical service.

---

# 🔮 Future Improvements

The following features can be added in future versions:

- Improve the chatbot UI
- Add conversation memory
- Add document/source citations
- Retrieve multiple relevant documents
- Support multiple medical PDFs
- Allow users to upload their own documents
- Add authentication and user accounts
- Add streaming responses
- Add multilingual support
- Add voice input and output
- Improve retrieval accuracy
- Add automated testing
- Add evaluation metrics for RAG responses
- Add hallucination detection
- Deploy the application to a cloud platform
- Use a production WSGI server for deployment

---

# 📈 Learning Outcomes

This project demonstrates practical knowledge of:

- Python
- Natural Language Processing
- Generative AI
- Retrieval-Augmented Generation
- Large Language Models
- Vector Databases
- Semantic Search
- Text Embeddings
- LangChain
- Hugging Face
- FAISS
- Groq API
- Flask
- Environment Variables
- Exception Handling
- Application Logging

---

# 👩‍💻 Author

**Swati Mahapatra**

B.Tech – Computer Science and Engineering  
Artificial Intelligence & Machine Learning

---

# ⭐ Project Summary

```text
AI Medical Chatbot
       │
       ├── Flask
       │
       ├── LangChain
       │
       ├── Hugging Face Embeddings
       │
       ├── FAISS Vector Database
       │
       ├── Groq LLM
       │
       └── RAG
       
              ↓
       
Context-Based Medical Question Answering
```

---

## 📌 Project Type

**Artificial Intelligence / Generative AI / NLP / RAG Project**
