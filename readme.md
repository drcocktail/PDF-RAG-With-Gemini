# PDF Q&A System with Google Gemini API and ChromaDB

This repository provides a **Q&A application** that allows users to upload a PDF, parse its content, and query it in natural language. By combining the **Google Gemini API** for embeddings and content generation with **ChromaDB** for efficient text storage and retrieval, the system provides a seamless way to interact with static documents.

---

## Table of Contents
1. [Features](#features)  
2. [Libraries Used](#libraries-used)  
3. [Architecture](#architecture)  
4. [Installation](#installation)  
5. [Usage](#usage)  
6. [Challenges and Pitfalls](#challenges-and-pitfalls)  
7. [Safeguards for a Commercial Product](#safeguards-for-a-commercial-product)  
8. [Future Improvements](#future-improvements)  

---

## Features
- **PDF Parsing**: Extracts text from PDFs, processing page-by-page for modularity.
- **Semantic Search**: Leverages embeddings to identify relevant document passages based on user queries.
- **Dynamic Q&A**: Generates answers using **Google Gemini API** based on user queries and relevant document content.

---

## Libraries Used
### 1. **`google.generativeai`**
   - Used for generating **text embeddings** and natural-language responses.
   - Enables **semantic understanding** of the document and queries.

### 2. **`chromadb`**
   - A **vector database** for embedding storage and retrieval.
   - Offers scalability and fast similarity searches for document querying.

### 3. **`PyPDF2`**
   - A robust library for **extracting text from PDFs**.
   - Splits documents into manageable chunks (pages).

### 4. **`dotenv`**
   - Manages environment variables securely, ensuring API keys are not hardcoded.

---

## Architecture
The system consists of three main components:
1. **PDF Parsing**:
   - Extracts text from the PDF and organizes it page-by-page using `PyPDF2`.
   - Each page is stored as a document in the vector database (`ChromaDB`).

2. **Semantic Embedding and Storage**:
   - Text embeddings are generated using **Google Gemini API**.
   - These embeddings are stored in **ChromaDB** for similarity-based retrieval.

3. **Q&A Workflow**:
   - The user’s query is embedded using the same model and matched against stored embeddings in **ChromaDB**.
   - The most relevant passage is used as context for generating an answer via the **Google Gemini API**.

---

## Installation
### Prerequisites
1. Python 3.8 or higher.
2. Google Cloud account with **Gemini API** access.
3. Install the required libraries:
   ```bash
   pip install google-generativeai chromadb PyPDF2 python-dotenv
   ```

### Steps to Set Up
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/pdf-qna.git
   cd pdf-qna
   ```

2. Create a **`.env`** file in the root directory and add your Google API key:
   ```plaintext
   GOOGLE_API_KEY=your-google-api-key
   ```

3. Run the application:
   ```bash
   python main.py
   ```

---

## Usage
### Adding a PDF
1. If the database is empty, the system prompts you to upload a PDF:
   ```plaintext
   Enter the path to your PDF: example.pdf
   ```
2. The text is parsed and stored as embeddings in ChromaDB.

### Querying the PDF
- Ask questions in natural language, such as:
  ```plaintext
  Your question: What is discussed in the introduction?
  ```
- Receive an AI-generated answer and the relevant passage:
  ```plaintext
  Answer: The introduction outlines the importance of...
  Passage: In the introduction, the author discusses...
  ```

- Type `exit` to quit the program.

---

## Challenges and Pitfalls
### Major Challenges
1. **Handling Large PDFs**:
   - Large PDFs can overwhelm memory or processing capabilities.
   - Solution: Process and embed text page-by-page for modularity.

2. **Text Retrieval Accuracy**:
   - Embedding models may misinterpret queries or retrieve irrelevant passages.
   - Solution: Use high-quality embeddings and fine-tune retrieval parameters.

### Pitfalls
- **API Dependency**: Relies heavily on **Google Gemini API**, making it vulnerable to changes in service or pricing.
- **Limited Context Window**: Only retrieves one passage at a time, which might miss broader context.

---

## Safeguards for a Commercial Product
If this system were to be developed into a commercial product, the following safeguards would be critical:

### **1. Data Privacy**
- Encrypt PDF uploads and text data stored in databases.
- Ensure compliance with data privacy laws like GDPR and HIPAA for sensitive documents.

### **2. Query Moderation**
- Implement filters to prevent misuse of the system (e.g., inappropriate or malicious queries).

### **3. Rate Limiting**
- Restrict API calls to prevent excessive usage or abuse, reducing costs and ensuring system availability.

### **4. Backup and Failover**
- Use backup databases and failover mechanisms to ensure reliability in case of server or service downtime.

### **5. User Authentication**
- Require users to authenticate before using the system to maintain security and track usage.

---

## Future Improvements
1. **FAISS Integration**:
   - Use FAISS for faster and more scalable vector searches, improving performance on large datasets.

2. **LangChain Framework**:
   - Streamline interaction logic with LangChain’s **prompt engineering** and **chained workflows**.

3. **Multi-Passage Retrieval**:
   - Retrieve multiple relevant passages for more comprehensive answers.

4. **Web Interface**:
   - Build a web app with frameworks like Flask or React for better user experience.

5. **Mobile Support**:
   - Extend the system to support mobile platforms for on-the-go document querying.

---

This project demonstrates the potential of combining cutting-edge AI tools with efficient storage solutions to unlock static document content. Engineers and developers are encouraged to fork the repository, experiment, and contribute to the system’s growth!