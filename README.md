# AI-Powered RAG Chatbot Using n8n

An AI-powered chatbot that answers questions from a credit appraisal policy document using Retrieval-Augmented Generation (RAG), Google Gemini, and n8n workflow automation.

##  Project Overview

This project demonstrates how to build a document-based AI chatbot using **n8n, Google Gemini, Google Drive, and a vector store**.

The chatbot allows users to ask questions about a Credit Appraisal Policy and Loan Eligibility Rules document in natural language. It retrieves relevant information from the uploaded document and uses Google Gemini to generate a clear, context-based response.

Instead of manually searching through lengthy policy documents, users can interact with the chatbot to understand important rules and eligibility conditions.

##  Problem Statement

Credit appraisal documents contain several rules related to loan eligibility, credit scores, loan-to-value ratios, repayment periods, and applicant age limits.

Finding specific information manually can be time-consuming. A general-purpose AI model may also provide answers that are not specific to the document.

This project addresses these challenges by combining document retrieval with AI-generated responses, helping users find relevant policy information more efficiently.

##  Key Features

- **Document ingestion:** Downloads a policy document from Google Drive.
- **Document processing:** Loads document content for indexing.
- **Semantic search:** Uses Google Gemini embeddings to represent document content as vectors.
- **Vector storage:** Stores document content in the n8n Simple Vector Store.
- **AI-powered responses:** Uses Google Gemini through an n8n AI Agent to answer questions.
- **Contextual retrieval:** Retrieves relevant document passages to support answers.
- **Conversational memory:** Uses Simple Memory to maintain context during a chat session.
- **Visual automation:** Connects the components through an n8n workflow without requiring a separately developed backend.

##  Technologies Used

| Technology | Purpose |
|---|---|
| n8n | Workflow automation and AI agent orchestration |
| Google Gemini | Generates natural-language answers |
| Google Gemini Embeddings | Converts text into vector representations |
| Google Drive | Stores and supplies the source document |
| Simple Vector Store | Stores indexed document content for retrieval |
| Default Data Loader | Loads document content for processing |
| Simple Memory | Maintains conversation context |
| Retrieval-Augmented Generation (RAG) | Grounds answers in retrieved document information |

##  How RAG Works in This Project

Retrieval-Augmented Generation combines information retrieval with AI-generated answers.

### 1. Document Ingestion

The user manually starts the ingestion workflow in n8n.

- The Google Drive node downloads the selected policy document.
- The Default Data Loader prepares the document content.
- Google Gemini Embeddings converts the text into vector representations.
- The Simple Vector Store stores the processed document content and embeddings.

### 2. Question Answering

When a user sends a message through the n8n chat interface:

- The AI Agent receives the question.
- The Google Gemini Chat Model processes the request.
- The vector-store retrieval tool searches for relevant document content.
- The retrieved content is provided to the AI Agent.
- Google Gemini generates a readable response based on the available context.
- Simple Memory helps maintain conversation context.

### Workflow Summary

**Google Drive → Document Loader → Gemini Embeddings → Simple Vector Store → Retrieval Tool → AI Agent → Chatbot Response**

The ingestion and chat stages are separate parts of the same n8n workflow.

##  Example Use Case

The reference document contains car loan and home loan eligibility rules.

Example questions include:

- What is the maximum LTV for a new electric passenger vehicle?
- What is the minimum bureau score required for a home loan?
- What is the maximum permitted FOIR for a home loan?
- What is the maximum loan tenure for a car loan?
- Summarize the key points in the uploaded policy document.

The chatbot retrieves relevant information from the document to help answer these questions. Answers should be checked against the original policy, especially when used for financial decisions.

##  How to Set Up the Project

### Prerequisites

- An n8n account or instance.
- A Google AI Studio API key with access to a supported Gemini model.
- A Google account with access to the source document in Google Drive.
- The exported n8n workflow JSON file from this repository.

### Step 1: Import the Workflow

1. Download `n8n-rag-chatbot.json` from this repository.
2. Open your n8n instance.
3. Open the workflow menu and select the option to import a workflow from a file.
4. Select the downloaded JSON file.
5. Review the imported nodes and their connections.

### Step 2: Configure Google Gemini

1. Open the Google AI Studio website: https://aistudio.google.com/
2. Create or access your API key.
3. In n8n, open the Google Gemini Chat Model node.
4. Create or select the appropriate Google Gemini API credential.
5. Enter your API key in the credential form and save it.
6. Select a supported Gemini chat model.

Configure the Google Gemini Embeddings node separately if it requires its own credential selection.

**Security note:** Never place your API key directly in this README or upload it to GitHub.

### Step 3: Configure Google Drive

1. Open the Download File node in n8n.
2. Create or select a Google Drive credential.
3. Complete the required Google authorization steps.
4. Select the policy document accessible to your Google account.
5. Confirm that the node can download the document successfully.

The original document may not be accessible to other users. They should configure their own Google Drive credentials and select a document they are authorized to use.

### Step 4: Verify the Embeddings and Vector Store

1. Confirm that the ingestion vector store uses the Google Gemini Embeddings node.
2. Confirm that the document loader is connected correctly.
3. Check that the chat retrieval tool uses the same compatible embedding configuration.
4. Execute the ingestion workflow.
5. Confirm that the nodes execute successfully before testing the chatbot.

### Step 5: Test the Chatbot

1. Open the chat panel in n8n.
2. Ask a question about the uploaded policy.
3. Verify that the AI Agent retrieves relevant information.
4. Compare the answer with the original document.
5. Test a question about information that the document does not contain.

##  Repository Structure

```text
n8n-rag-chatbot/
│
├── README.md
├── n8n-rag-chatbot.json
├── n8n_RAG_Chatbot_Documentation_With_Screenshot_Explanations.docx
└── screenshots/
    ├── workflow-overview.png
    ├── document-ingestion.png
    └── chatbot-response.png
```

The screenshot filenames above are examples. Use the actual filenames of the screenshots you upload. The workflow JSON, documentation, and screenshots should be included only after reviewing them for sensitive information.

##  Limitations

- The Simple Vector Store uses in-memory storage, so indexed data may be lost when the n8n instance restarts.
- The document may need to be ingested again after a restart.
- Retrieval quality depends on document structure, text extraction, embeddings, and retrieval settings.
- AI-generated answers can still contain errors and should be verified against the source document.
- The current workflow uses one AI Agent with a retrieval tool; it is not a multi-agent system.
- This is a demonstration project, not a production loan approval system.

##  Future Improvements

- Integrate a persistent vector database.
- Support multiple policy documents and file formats.
- Improve document chunking and retrieval quality.
- Add answer validation against retrieved passages.
- Expand automated testing and error handling.
- Introduce multiple coordinated agents if more complex agent-based processing is required.

##  Security Considerations

- Keep Google Gemini API keys and OAuth credentials private.
- Never upload credential exports or secrets to a public repository.
- Review the exported workflow JSON before sharing it.
- Do not publish confidential documents or personal financial information without authorization.
- Use human review and appropriate controls before applying policy information to real financial decisions.

##  Author

**Sadicsha Khandait**

MBA – Data Science and Data Analytics

Project: AI-Powered RAG Chatbot Using n8n

##  Disclaimer

This project is developed for educational and demonstration purposes. The chatbot provides information retrieved from a reference policy document and should not be treated as an independent authority for financial or loan approval decisions.
