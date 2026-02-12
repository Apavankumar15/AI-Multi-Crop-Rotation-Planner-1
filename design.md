System Design Document
AI for Bharat Hackathon – Rural & Sustainability Track
 1. System Overview

The AI Multi-Crop Rotation Planner is a Retrieval-Augmented AI system designed to provide intelligent crop rotation recommendations for sustainable agriculture.

The system combines:

 A REST API backend
 A Vector Database (FAISS)
 Sentence Embedding Model
 Large Language Model (Llama 3 via Groq API)
 Structured JSON output

The architecture ensures context-aware, explainable, and scalable crop planning recommendations.



 2. High-Level Architecture

 System Flow

User Input
   ↓
Flask Backend API
   ↓
Query Construction
   ↓
FAISS Vector Retrieval
   ↓
Context + User Data → LLM (Llama 3)
   ↓
Structured JSON Response
   ↓
Client Output




 3. Architectural Components

 3.1 API Layer (Flask Backend)

Technology Used: Python + Flask

Responsibilities:

 Expose REST endpoint `/generate-plan`
 Accept JSON input
 Validate inputs
 Call AI reasoning module
 Return structured JSON response

This layer acts as the communication bridge between user and AI system.



 3.2 Knowledge Retrieval Layer (Vector Database)

Technology Used:

 FAISS (Facebook AI Similarity Search)
 Sentence Transformers

Responsibilities:

 Store agricultural domain knowledge
 Convert text documents into embeddings
 Perform similarity search
 Retrieve top relevant knowledge snippets

This ensures recommendations are grounded in agricultural facts instead of generic model memory.



 3.3 Embedding Model

Model Used: `all-MiniLM-L6-v2`

Purpose:

 Convert agricultural text documents into numerical vectors.
 Convert query into vector representation.
 Enable semantic similarity search.



 3.4 LLM Reasoning Layer

Model Used: Llama 3 via Groq API

Responsibilities:

 Analyze:

   Soil type
   Current crop
   Season
   Water availability
   Retrieved agricultural knowledge
 Generate structured output including:

   Recommended crops
   Soil benefit score
   Risk level
   Profit estimation
   Explanation

The LLM performs contextual reasoning using retrieved domain knowledge.



 3.5 Retrieval-Augmented Generation (RAG)

The system uses RAG to improve reliability and domain accuracy.

Process:

1. User input converted into query.
2. FAISS retrieves relevant agricultural knowledge.
3. Retrieved context is inserted into prompt.
4. LLM generates recommendation grounded in context.

This approach reduces hallucination and increases explainability.

 4. Data Flow Description

 Step 1: User Input
User provides:
 Soil type
 Current crop
 Season
 Water availability

 Step 2: Query Formation
System creates a structured query combining user parameters.
Example:
"Soil: Black, Crop: Rice, Season: Kharif"

 Step 3: Knowledge Retrieval

 Query is converted into embedding.
 FAISS searches nearest knowledge vectors.
 Top relevant agricultural facts are retrieved.

 Step 4: Prompt Construction
Prompt contains:
 Retrieved knowledge
 User inputs
 Required JSON output format

 Step 5: LLM Reasoning
Llama 3 processes prompt and generates structured recommendation.

 Step 6: JSON Parsing & Response
 Output is validated.
 Returned as structured JSON via Flask API.


 5. Technology Stack

| Layer                   | Technology            |
| -- |  |
| Backend                 | Python, Flask         |
| Vector DB               | FAISS                 |
| Embeddings              | Sentence Transformers |
| LLM                     | Llama 3 (Groq API)    |
| Data Format             | JSON                  |
| Development Environment | VS Code               |



 6. System Design Principles

 6.1 Modularity

Each component is isolated:
 API layer
 Retrieval layer
 AI reasoning layer
This allows easy upgrades.

 6.2 Scalability

System can scale by:
 Adding more agricultural documents
 Supporting multiple states
 Expanding crop types
 Integrating weather APIs


 6.3 Maintainability

 Clear folder structure
 Separated logic files
 Modular retrieval pipeline
 Structured output enforcement



 7. Security Considerations

 API keys stored using environment variables.
 No hardcoded credentials in repository.
 Structured input validation.



 8. Limitations (Current Version)

 Limited agricultural dataset.
 No live weather integration.
 Prototype stage UI.
 Focused on selected crop types.


 9. Future Enhancements

 Integration with weather APIs
 State-specific agricultural datasets
 Market price prediction
 Multilingual support
 Mobile app deployment
 Farmer feedback learning loop


 10. Conclusion

The AI Multi-Crop Rotation Planner demonstrates how Retrieval-Augmented AI systems can transform traditional farming practices into intelligent, sustainable decision-making systems.
The architecture is modular, scalable, and adaptable for nationwide deployment.