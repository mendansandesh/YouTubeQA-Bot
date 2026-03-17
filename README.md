# 🎬 YouTubeQA-Bot 🎤

> AI-powered Question Answering Bot over Movie Transcripts using RAG (Retrieval-Augmented Generation)

YouTubeQA-Bot is a production-ready, Dockerized AI system that lets users ask natural language questions about movie plots or scenes. It uses vector databases and Large Language Models (LLMs) to answer contextually using actual **movie transcripts**.

## 🎬 Demo(< 1min)

![Project Demo](assets/project.gif)

---

## 🔍 Key Features

- 🎞️ Ingests and indexes full movie transcripts
- 🧠 Uses **RAG (Retrieval-Augmented Generation)** pipeline with OpenAI/GPT models
- 🔎 Semantic search using `ChromaDB` + `FAISS`
- 🐳 Fully Dockerized with `Dockerfile` and `docker-compose.yaml`
- 🧪 Modular design — easy to plug in new LLMs or datasets
---
## Architecture
<img width="2531" height="697" alt="youtubeQ A_bot" src="https://github.com/user-attachments/assets/d6933c4e-d145-4c3d-b0c1-a3519d811baa" />


---
## 🧰 Tech Stack

| Component                      | Technology / Library                   |
|--------------------------------|----------------------------------------|
| Language & Runtime             | Python 3.10+                           |
| Deployment / Containerization  | Docker                                 |
| Transcript Loader              | `youtube_transcript_api`               |
| Chunking & Embedding           | HuggingFace's `all-MiniLM-L6-v2`       |
| Vector DB                      | Chroma DB                              |

---
## 📁 Project Structure

```
youtubeqa_bot/
├── app.py # Entry point for the bot
├── ui_streamlit.py # UI - Entry point for the bot
├── Dockerfile # Docker setup
├── docker-compose.yaml # Multi-container orchestration
├── requirements.txt # Python dependencies
├── chroma_db/    # Persisted Chroma vector database files  
├── vectorstore/  # Chroma indexer logic (manages embedding storage & retrieval)
├── transcript/ # Raw movie transcript files
├── rag/ # RAG pipeline implementation
└── README.md # This file
```

---

## ⚙️ How to Run the Project

### This project can be run in two ways:
1. Streamlit UI (ui_streamlit.py) – interactive web interface (recommended)
2. CLI mode (app.py) – quick terminal-based usage

The Docker-based setup is the easiest and most reliable way to run the project.

### Docker-Based Setup (Recommended)
#### Prerequisites
- Docker Desktop (or Docker Engine + Docker Compose v2)
- Git

### Step 1: Clone the Repository
```bash
git clone https://github.com/<your-username>/YouTubeQA-Bot.git
cd YouTubeQA-Bot
```

### Step 2: Build Docker Images (One Time Only)
You need to build the Docker image only once, or again if requirements.txt or Dockerfile changes.
```bash
docker compose build
```

### Step 3: Run 
#### Option A: Run with Streamlit UI (Recommended)
Start the interactive Streamlit UI:
```bash
docker compose up streamlit --no-build
```
Open your browser at:
```bash
http://localhost:8501
```
From the UI you can:
- Enter a YouTube Video ID
- Load and index the transcript
- Ask questions about the video
- See answers stream in real time

To stop the UI:
```bash
Ctrl + C
docker compose down
```

#### Option B: Run in CLI Mode (Terminal)
For quick testing without a UI:
```bash
docker compose up app --no-build
```
Or run a one-off command with arguments:
```bash
docker compose run --rm app python app.py <YOUTUBE_VIDEO_URL> "<QUESTION>"
```
---
## Cleanup
Stop and remove all running containers:
```bash
docker compose down
```
---
🧠 How It Works
1. Parses and indexes movie transcripts into a Chroma vector store.
2. User asks a question — e.g., "Why Chris Gardner shirt was dirty?"
3. Relevant transcript chunks are retrieved via vector similarity.
4. These chunks + the user query are passed to the LLM (GPT) to generate the answer.
Answer is returned to the user via CLI or API.

---
⚠️ Current Limitations

- Answers are grounded in retrieved transcript chunks
- High-level questions like “Summarize the entire video” are limited by chunk-based retrieval
- Timestamp-based jumping is planned but not yet enabled

---
🔮 Future Enhancements

- Video-level summarization
- Timestamp-aware answers with clickable YouTube links
- Multi-video comparison
- Improved semantic retrieval and reranking

---
🤝 Contributing

Pull requests are welcome. Please open issues to discuss improvements or bugs.

---
📜 License

MIT License – feel free to use, fork, and modify.

📫 Contact

Made by Sandesh Mendan
Project inspired by movie nerds + LLMs ✨
