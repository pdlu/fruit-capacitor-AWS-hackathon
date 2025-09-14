# 🍓🥑 Fruits Capacitor  
*Sacramento’s First AWS Hackathon Project*  

An **AI-powered fruit ripeness detection system** that classifies fruit images (starting with strawberries and avocados) and builds a scalable **knowledgebase for real-time freshness monitoring**. Designed with **AWS Bedrock, LangChain, ChromaDB, and Streamlit**, the system helps **farmers, distributors, and retailers** reduce waste and optimize crop quality.  

---

## ✨ Features  

- 📸 **Image-to-Text Classification**: Upload fruit images and generate embeddings for ripeness prediction  
- 🔍 **Intelligent Retrieval**: Vector-based similarity search using **ChromaDB** and AWS Bedrock embeddings  
- 💬 **Natural Language Q&A**: Ask ripeness-related questions (e.g., *“Is this avocado edible tomorrow?”*) and receive contextual answers  
- 📚 **Source Citations**: Results are explained with reference to processed data and documentation  
- 🌐 **Interactive Web Interface**: Simple **Streamlit app** for uploading images, asking questions, and managing data  
- 🔄 **Scalable Knowledgebase**: Extendable to other crops beyond strawberries and avocados  

---

## 🏗️ Architecture  
```mermaid
flowchart TD

    A[Fruit Image\n(Strawberry / Avocado)] --> B[Image-to-Text\n(ChatGPT)]
    B --> C[Text Extraction + Chunking]
    C --> D[Vector Embeddings\n(AWS Bedrock)]
    D --> E[ChromaDB]

    E --> F[Similarity Search]
    F --> G[Relevant Chunks]
    G --> H[AWS Bedrock LLM\n(RAG)]
    H --> I[Answer + Sources]

    subgraph User Interaction
        J[User Question] --> F
    end


```


---

## 🚀 Quick Start  

### Prerequisites  
- AWS Account with Bedrock access  
- Python 3.8+  
- AWS CLI configured or `.env` credentials  

### Installation  

Clone the repository:  
```bash
git clone <your-repo-url>
cd fruits-capacitor
```

Install dependencies:
```bash
pip install -r requirements.txt
```

Set up AWS credentials:
```aws configure```

or use .env:
```
AWS_ACCESS_KEY_ID=your_access_key  
AWS_SECRET_ACCESS_KEY=your_secret_key  
AWS_DEFAULT_REGION=us-west-2  
```

Enable AWS Bedrock models in the console:
```
amazon.titan-embed-image-v1 (for embeddings)
us.amazon.nova-micro-v1:0 (for Q&A)
```

Run the application:
```
streamlit run app.py
```

Open your browser at `http://localhost:8501`

## 📖 Usage Guide

### Upload Fruit Images

1. Navigate to the 📤 Upload Files tab

2. Upload .jpg or .png fruit images

3. Re-index knowledgebase to process embeddings

4. Ask Ripeness Questions

5. Use the 💬 Ask Questions tab

6. Enter natural language questions (e.g., “How many days until this banana spoils?”)

7. Receive AI-powered predictions with source explanations

### Manage Knowledgebase

Delete or re-index fruit data to refresh your database

### 🔧 Configuration

Update constants in `app.py`:
```python
AWS_BEDROCK_EMBEDDING_MODEL_ID = "amazon.titan-embed-image-v1"
AWS_BEDROCK_LLM_MODEL_ID = "us.amazon.nova-micro-v1:0"
AWS_REGION = "us-west-2"

chunk_size = 500
chunk_overlap = 50
```

### 📦 Dependencies

`requirements.txt:`
```shell
streamlit>=1.28.0
langchain>=0.1.0
langchain-community>=0.0.10
boto3>=1.34.0
chromadb>=0.4.0
Pillow>=10.0.0
python-dotenv>=1.0.0
```

### 🛠️ How It Works

#### Image Processing

* Image-to-Text: Fruit images are converted into textual descriptions using ChatGPT
* Embedding: Text is vectorized using AWS Bedrock Titan
* Storage: Vectors stored in ChromaDB for fast semantic search

#### Ripeness Question Answering

1. User queries are vectorized

2. Relevant fruit data chunks retrieved from ChromaDB

3. Context passed to AWS Bedrock LLM

4.  Model generates ripeness prediction + sources

### 🔒 Security Notes

    Documents/images processed locally before cloud inference

    AWS IAM roles should have least-privilege Bedrock access

    Consider data sensitivity when uploading real-world datasets

### 🚀 Deployment Options

    Local Development: Run with Streamlit

    AWS EC2: Deploy on cloud instance with IAM role

    Docker: Containerize and deploy

### Example Dockerfile:

FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
EXPOSE 8501
CMD ["streamlit", "run", "app.py", "--server.port=8501", "--server.address=0.0.0.0"]

### 🙏 Acknowledgments

    AWS Bedrock for embeddings + LLMs

    LangChain for orchestration

    ChromaDB for vector storage

    Streamlit for web UI

