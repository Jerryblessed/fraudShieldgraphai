# FraudShield Graph AI

## Inspiration
Fraudulent transactions in finance and e-commerce have led to significant financial losses. Traditional fraud detection methods struggle with complex patterns, making graph-based AI an innovative solution.

## What it does
FraudShield Graph AI analyzes financial transactions using graph-based analytics and AI to detect fraudulent behavior. It identifies suspicious activity, unusual patterns, and connections between fraudulent accounts, providing real-time alerts to administrators via Telegram.

## How we built it
- **Database:** ArangoDB for storing financial transaction data in a graph structure.
- **Graph Analysis:** NetworkX and cuGraph for fraud pattern detection. A sample dataset (`G_nx = nx.karate_club_graph()`) was used to demonstrate how fraud detection can be performed using graph analytics.
- **AI Integration:** GPT-4o via LangChain for querying and interpreting fraud risks.
- **Frontend & Alerts:** Telegram bot and a web-based UI for real-time monitoring.

## Architectural Diagram
```
                     +-------------------+
                     |  User Transaction |
                     +---------+---------+
                               |
                               v
                     +-------------------+
                     |  ArangoDB (Graph) |
                     +---------+---------+
                               |
                               v
       +--------------------------------------+
       |       Graph Processing Engine       |
       |  (NetworkX / cuGraph)               |
       +---------+--------------------------+
                 |
                 v
       +---------------------------+
       |  AI Query Processing (LLM) |
       |  (GPT-4o via LangChain)    |
       +---------+-----------------+
                 |
                 v
       +-------------------------+
       |  Alerts & Visualization |
       |  (Telegram Bot / Web UI) |
       +-------------------------+
```

## Challenges we ran into
- **Data Complexity:** Graph relationships can be vast, requiring optimized query performance.
- **Scalability:** Processing large-scale financial transactions efficiently.
- **Real-time Processing:** Balancing AI-based analysis with speed for immediate fraud alerts.

## Accomplishments that we're proud of
- Successfully integrating **graph-based fraud detection** with **real-time AI insights**.
- Implementing **GPU-accelerated** fraud analysis for efficiency.
- Building a **Telegram bot** to notify admins about detected fraud cases.

## What we learned
- How to leverage **cuGraph for large-scale fraud detection**.
- Optimizing **ArangoDB queries** for quick retrieval and processing.
- AI-driven anomaly detection can significantly enhance traditional fraud prevention systems.

## What's next for FraudShield Graph AI
- **Expanding integrations** with financial institutions and e-commerce platforms.
- **Enhancing AI models** to improve fraud prediction accuracy.
- **Adding a web dashboard** for deeper fraud case analysis and reporting.
- **Improving real-time processing** with further GPU optimizations.

## Getting Started
To get started with FraudShield Graph AI, run the following steps in a Jupyter Notebook or Google Colab:

### Open in Colab
[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Jerryblessed/fraudShieldgraphai/blob/main/fdetect.ipynb)

### Installation
```sh
pip install networkx nx_arangodb cugraph-cu12 cudf-cu12 openai langchain_community python-telegram-bot matplotlib langgraph langchain_openai nx-arangodb[llm]
```

### Running the Project
```python
import os
import networkx as nx
import nx_arangodb as nxadb
import cudf
import cugraph as cg
import openai
from openai import AzureOpenAI
import matplotlib.pyplot as plt
from telegram import Bot

# Set up environment variables
os.environ["DATABASE_HOST"] = "https://tutorials.arangodb.cloud:8529"
os.environ["DATABASE_USERNAME"] = "your_username"
os.environ["DATABASE_PASSWORD"] = "your_password"
os.environ["DATABASE_NAME"] = "your_database"

api_base = "https://your-openai-instance.openai.azure.com/"
api_key = "your_api_key"
api_version = "2023-06-01-preview"

TELEGRAM_BOT_TOKEN = "your_telegram_bot_token"
TELEGRAM_CHAT_ID = "your_chat_id"
```

### Graph Initialization
```python
bot = Bot(token=TELEGRAM_BOT_TOKEN)

def send_telegram_message(message):
    """Send a message to Telegram chat."""
    bot.send_message(chat_id=TELEGRAM_CHAT_ID, text=message)

# Load a sample graph and persist it to ArangoDB
G_nx = nx.karate_club_graph()
G_adb = nxadb.Graph(name="GraphRAG")
G_adb.add_edges_from(G_nx.edges(data=True))
send_telegram_message("✅ Graph successfully initialized in ArangoDB.")
```

### Graph Analysis
```python
def analyze_graph_cugraph(G_nx):
    """Convert to cuGraph for GPU acceleration, fallback to CPU if no CUDA."""
    try:
        cu_df = cudf.DataFrame(list(G_nx.edges(data=True)), columns=["src", "dst", "weight"])
        G_cg = cg.Graph()
        G_cg.from_cudf_edgelist(cu_df, source="src", destination="dst", edge_attr="weight")
        send_telegram_message("⚡ Graph successfully analyzed using cuGraph (GPU-accelerated).")
        return G_cg
    except Exception as e:
        send_telegram_message(f"⚠️ GPU not available or error using cuGraph: {e}. Falling back to NetworkX.")
        return G_nx
```

### Querying with GPT-4o
```python
from langchain_community.chat_models import ChatOpenAI
from langchain.prompts import ChatPromptTemplate

llm = ChatOpenAI(model_name="gpt-4o", openai_api_key=api_key, openai_api_base=api_base)

def query_graph(prompt):
    chat_prompt = ChatPromptTemplate.from_messages([
        ("system", "You are an AI assistant specializing in graph analytics."),
        ("user", "{prompt}")
    ])
    response = llm.invoke(chat_prompt.format_messages(prompt=prompt))
    send_telegram_message(f"📡 User Query: {prompt}\n🤖 AI Response: {response}")
    return response
```

## Running the Interactive Session
```python
while True:
    user_query = input("Ask a graph-related question: ")
    if user_query.lower() in ["exit", "quit"]:
        send_telegram_message("🔴 Graph interaction session ended.")
        print("Goodbye!")
        break
    response = query_graph(user_query)
    print("AI Response:", response)
```

## Contributing
We welcome contributions to enhance FraudShield Graph AI. Please submit issues and pull requests on our GitHub repository.

## License
This project is licensed under the MIT License - see the LICENSE file for details.

---
This README provides a structured overview of the project, how to install and run it, and how users can interact with the system using AI-powered fraud detection through graphs. 🚀

