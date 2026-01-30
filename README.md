# Medical Chatbot

A sophisticated medical chatbot powered by Large Language Models (LLMs) and Retrieval-Augmented Generation (RAG). This chatbot provides concise and accurate answers to medical questions based on the content of a medical book.

## Project Overview

This project is a sophisticated medical chatbot designed to provide users with reliable and concise answers to their medical questions. Leveraging the power of Large Language Models (LLMs) and Retrieval-Augmented Generation (RAG), the chatbot uses a medical book as its knowledge base, ensuring that the information provided is accurate and contextually relevant. The chatbot is built with a modern tech stack that includes Flask for the backend, Pinecone for the vector store, and OpenAI's GPT-4o for the language model.

## Key Features

-   **Conversational AI:** Engage in a natural and intuitive conversation with the chatbot to get answers to your medical questions.
-   **Accurate & Contextual Answers:** The chatbot uses a medical book as its knowledge base, ensuring that the answers are not only accurate but also contextually relevant to the user's query.
-   **Concise Responses:** To ensure clarity and ease of understanding, the chatbot is programmed to provide answers in three sentences or less.
-   **Built with LangChain:** Leverages the power of the LangChain framework for building robust and scalable LLM applications.
-   **Dockerized Application:** The application is containerized using Docker, making it easy to set up and run in any environment.
-   **CI/CD Pipeline:** The project is configured with a CI/CD pipeline using GitHub Actions, which automates the process of building, testing, and deploying the application.
-   **Cloud Deployment:** The application is designed to be deployed on AWS, with the CI/CD pipeline configured to deploy the application on an EC2 instance.

## How to Use

To start a conversation, simply type your medical question in the chatbox and press "Send." The chatbot will then provide a concise and accurate answer based on its knowledge base.

## Architecture

The application follows a Retrieval-Augmented Generation (RAG) architecture:

1.  **Data Loading & Processing:** A medical book in PDF format is loaded and split into smaller text chunks.
2.  **Embedding & Indexing:** The text chunks are converted into vector embeddings using a Hugging Face model (`sentence-transformers/all-MiniLM-L6-v2`) and stored in a Pinecone vector store for efficient retrieval.
3.  **User Query:** The user asks a question through a Flask-based web interface.
4.  **Retrieval:** The user's query is converted into an embedding, and a similarity search is performed on the Pinecone index to retrieve the most relevant text chunks.
5.  **Generation:** The retrieved text chunks, along with the user's question and a system prompt, are passed to an OpenAI LLM (GPT-4o) to generate a human-like answer.
6.  **Response:** The generated answer is displayed to the user in the chat interface.

## Tech Stack

The project is built with a modern tech stack that includes:

-   **Backend:** Flask
-   **LLM:** OpenAI GPT-4o
-   **Orchestration:** LangChain
-   **Vector Store:** Pinecone
-   **Embeddings:** Hugging Face `sentence-transformers/all-MiniLM-L6-v2`
-   **Containerization:** Docker
-   **CI/CD:** GitHub Actions
-   **Deployment:** AWS (EC2, ECR)
-   **Libraries:**
    -   `langchain-pinecone`: for interacting with the Pinecone vector store
    -   `langchain-openai`: for interacting with the OpenAI API
    -   `python-dotenv`: for managing environment variables
    -   `PyPDF`: for loading PDF documents
    -   `Flask`: for building the web application

## Setup and Installation

### Prerequisites

-   Python 3.10
-   Conda (optional, but recommended)
-   Docker (optional)

### Steps

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/mo7amedatef/Medical_Chatbot.git
    cd Medical_Chatbot
    ```

2.  **Create a Conda environment (optional):**
    ```bash
    conda create -n medibot python=3.10 -y
    conda activate medibot
    ```

3.  **Install the dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Set up environment variables:**
    Create a `.env` file in the root directory and add your API keys:
    ```ini
    PINECONE_API_KEY="YOUR_PINECONE_API_KEY"
    OPENAI_API_KEY="YOUR_OPENAI_API_KEY"
    ```

5.  **Store data and create index:**
    Place your medical PDF book in the `data/` directory. Then, run the following command to process the data and store the embeddings in Pinecone:
    ```bash
    python store_index.py
    ```

6.  **Run the application:**
    ```bash
    python app.py
    ```
    The application will be available at `http://localhost:8080`.

### Running with Docker

1.  **Build the Docker image:**
    ```bash
    docker build -t medical-chatbot .
    ```

2.  **Run the Docker container:**
    ```bash
    docker run -p 8080:8080 --env-file .env medical-chatbot
    ```
    The application will be available at `http://localhost:8080`.

## Deployment

This project is configured for continuous integration and deployment (CI/CD) using GitHub Actions. The workflow automates the following steps:

1.  Builds a Docker image of the application.
2.  Pushes the Docker image to Amazon Elastic Container Registry (ECR).
3.  Deploys the application on an Amazon EC2 instance.

For more details, refer to the `.github/workflows/cicd.yaml` file.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contributing

Contributions are welcome! Please feel free to open an issue or submit a pull request.
