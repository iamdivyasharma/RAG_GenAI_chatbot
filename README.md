
## RAG-based Question Answering System

## Project Overview

This project builds a conversational chatbot using a Retrieval-Augmented Generation (RAG) system. The chatbot allows users to upload Excel files containing event, hotel, and restaurant data. Users can then ask questions about the data, and the system will retrieve relevant information and generate human-like responses using a large language model (LLM) from Hugging Face. The project utilizes FAISS for fast and efficient document retrieval and Streamlit to create a user-friendly web interface.

## Features

- **Conversational AI**: The system provides natural language responses to user queries.
- **Excel File Processing**: Upload event and hotel/restaurant data in Excel format.
- **Data Retrieval with FAISS**: Fast document search using FAISS vector stores.
- **Hugging Face Integration**: The chatbot generates answers based on the Llama-3 model from Hugging Face.
- **Contextual Responses**: The system answers user queries based on the uploaded data, including dates, event details, and hotel/restaurant information.

## Key Components

### Hugging Face Endpoint Initialization
A Hugging Face Large Language Model (LLM) is used for generating responses. The project initializes this LLM using an API token and repository ID from Hugging Face. The model, `Meta-Llama-3-8B-Instruct`, generates concise and relevant responses based on the retrieved data.

### File Upload and Processing
The system allows users to upload two Excel files:
1. **Event Data**: Contains information about upcoming events.
2. **Hotel & Restaurant Data**: Contains details about nearby hotels and restaurants.

These files are processed by reading their content into data frames. Each row in the data frames is converted into a document, where all columns are concatenated into a single string. These documents are then combined into a single list for further processing.

### Document Storage in FAISS Vector Store
After processing the uploaded data, the documents are embedded using a pre-trained sentence transformer model (`sentence-transformers/all-MiniLM-L6-v2`). The embeddings are then stored in a FAISS vector store, which allows for efficient document retrieval based on query similarity.

### Query Handling and Response Generation
Once the documents are embedded and stored, the chatbot can handle user queries. A prompt template is used to guide the LLM in generating relevant responses. The template ensures that the chatbot answers based on the available data and does not generate fabricated information. The user's query is processed, and the system retrieves the most relevant documents from the vector store. These documents are then used to generate a response via the LLM.

### User Interaction with Streamlit
The project is deployed using Streamlit, providing an easy-to-use web interface. Users can:
- Upload Excel files containing event, hotel, and restaurant data.
- Ask questions about the data (e.g., "What events are happening on July 28, 2024?").
- View a history of their queries and the chatbot's responses.

Streamlit handles the user inputs and displays the conversation history in real-time.

### Chat History Management
To make the user experience smoother, the chatbot stores and displays the entire conversation history, allowing users to scroll through past queries and responses within the session.

## Installation and Setup

### Prerequisites
- Python 3.8+
- npm (for localtunnel)

### Steps to Run the Application
1. Clone the repository:
   ```bash
   git clone https://github.com/your-repository-link.git
   ```

2. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Start the Streamlit application:
   ```bash
   streamlit run RAG_app.py --server.port 8081
   ```

4. Use Localtunnel to expose the application:
   ```bash
   npx localtunnel --port 8081
   ```

## Future Improvements

- Add support for other file formats (e.g., CSV, JSON).
- Enhance model performance by fine-tuning the LLM with domain-specific data.
- Enable multi-user sessions with persistent chat history.
