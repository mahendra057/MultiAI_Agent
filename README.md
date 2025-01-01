# Multi-AI-Agent_LangGraph

### LangChain Integration with AstraDB for Routing and Querying System

This project demonstrates how to integrate LangChain with AstraDB to create a sophisticated routing and querying system. The solution dynamically routes user queries to either a vector database or Wikipedia based on the context, providing efficient and relevant information retrieval.

---

## 🚀 Features and Workflow

### 1. **AstraDB Initialization**
- **Database Setup**: Establishes a connection to an AstraDB vector database using the `cassio` library.
- **Vector Storage**: Configures the `qa_mini_demo` table for storing and retrieving embeddings.

### 2. **Document Loading and Preprocessing**
- **Web Document Loading**: Utilizes `WebBaseLoader` to load documents from specified URLs.
- **Text Splitting**: Processes documents into manageable chunks using `RecursiveCharacterTextSplitter` with the `tiktoken` encoder for efficient vectorization and storage.

### 3. **Embeddings and Vector Database**
- **Embedding Creation**: Generates vector embeddings for text chunks using `HuggingFaceEmbeddings (all-MiniLM-L6-v2)`.
- **Vector Storage**: Stores the embeddings in AstraDB for fast similarity-based retrieval.

### 4. **Routing Logic**
- **RouterQuery Class**:
  - A `Pydantic` model to determine whether a query should be routed to the vector database or Wikipedia.
- **LLM Integration**:
  - Integrates a Groq-based LLM to dynamically decide routing.
  - Constructs a structured prompt to guide the LLM in determining whether to retrieve documents or search Wikipedia.

### 5. **Graph Workflow**
Built using `LangGraph`, the graph workflow orchestrates the query processing through the following nodes:

#### **Nodes**
- **`wiki_search`**: Fetches information from Wikipedia.
- **`retrieve`**: Retrieves relevant documents from the vector database.

#### **Routing**
- Dynamically routes queries based on the `question_router` output.
- Routes to either `wiki_search` or `retrieve` depending on the context of the question.

#### **Graph Compilation**
- Defines `START` and `END` nodes for the workflow.
- Dynamically decides the next node to process based on the routing logic.

### 6. **Running the Workflow**
- **Input**: A user-provided question, e.g., *"What is an agent?"*.
- **Process**:
  - Routes the query through the graph workflow.
  - Either retrieves a document from the vector database or fetches a Wikipedia summary.
- **Output**: Returns the relevant information from the selected path.

### 7. **Additional Features**
- **GraphState Class**:
  - Tracks the query (question), generated responses from the LLM, retrieved documents, and metadata.
- **Final Output**:
  - Displays the retrieved documents and their metadata (e.g., description).

---
