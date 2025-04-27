# PDF Knowledge Assistant -> uses Multi Agent Rag (Phi)

A conversational AI assistant that helps you interact with information from PDF documents using natural language.

## Overview

This project creates an AI-powered chat interface that allows users to query a knowledge base built from PDF content. The assistant can answer questions about the content, provide insights, and maintain context throughout the conversation.

Key features:
- Natural language interaction with PDF-based knowledge
- Contextual understanding of follow-up questions
- Persistent conversation history
- Vector search for semantic understanding of document content

## Technical Components

- **AI Assistant**: Built using [phidata](https://github.com/phidata-public/phi) framework
- **Vector Database**: PostgreSQL with pgvector extension for semantic search
- **Knowledge Base**: PDF documents processed and embedded for efficient retrieval
- **API**: Groq API for large language model capabilities

## Prerequisites

- Python 3.8+
- Docker
- Groq API key (create one at [console.groq.com](https://console.groq.com))

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/yourusername/pdf-assistant.git
cd pdf-assistant
```

### 2. Create a virtual environment and install dependencies

```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### 3. Set up environment variables

Create a `.env` file in the root directory with the following:

```
GROQ_API_KEY=your_groq_api_key_here
```

### 4. Start the pgvector database

Run the following Docker command to start a PostgreSQL instance with pgvector extension:

```bash
docker run -d \
  -e POSTGRES_DB=ai \
  -e POSTGRES_USER=ai \
  -e POSTGRES_PASSWORD=ai \
  -e PGDATA=/var/lib/postgresql/data/pgdata \
  -v pgvolume:/var/lib/postgresql/data \
  -p 5532:5432 \
  --name pgvector \
  phidata/pgvector:16
```

### 5. Run the application

```bash
python pdf_assistant.py
```

## Usage

After starting the application, you can interact with the assistant through the command-line interface:

- Ask questions about the PDF content
- Request summaries or specific information
- The assistant will maintain context throughout your conversation

Example queries:
```
What topics are covered in the PDF?
Can you explain the first chapter?
What are the key points about [specific topic]?
```

## Command Line Options

- `--new`: Start a new conversation session
- `--user USER`: Specify a user identifier (default: "user")

Example:
```bash
python pdf_assistant.py --new --user john
```

## Customization

To use your own PDF documents:
1. Update the `urls` parameter in the `PDFUrlKnowledgeBase` constructor with URLs to your PDF files
2. Or modify the code to load local PDF files
