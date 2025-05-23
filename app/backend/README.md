# Backend Application Documentation

This document provides an overview of the backend application for the Azure Search OpenAI Demo.

## Overview

The backend application is a Python-based web server built with the Quart framework that provides a REST API for the chat application. It integrates several Azure services including Azure OpenAI, Azure AI Search, and Azure Storage to provide intelligent search and chat capabilities.

## Architecture

The application follows a modular architecture with the following key components:

- **Main Application (`main.py`)**: Entry point that initializes the application and loads environment variables
- **Core Application (`app.py`)**: Contains route handlers and core application logic
- **Approaches**: Different implementation strategies for handling chat and search functionality:
  - `ChatReadRetrieveReadApproach`: Handles multi-turn conversations in `/chat`
  - `RetrieveThenReadApproach`: Used for single-turn Q&A in `/ask`
  - `ChatReadRetrieveReadVisionApproach`: Handles vision-based chat capabilities
  - `RetrieveThenReadVisionApproach`: Handles vision-based Q&A

## Key Features

1. **Authentication and Authorization**
   - Supports Azure AD authentication
   - Configurable access control for documents
   - Optional unauthenticated access mode

2. **Chat and Q&A Capabilities**
   - Multi-turn conversation support
   - Single-turn question answering
   - Vision-based chat and Q&A
   - Support for streaming responses

3. **Content Management**
   - User file upload support
   - Document processing and indexing
   - Support for various file formats

4. **Integration Features**
   - Azure OpenAI integration for chat and embeddings
   - Azure AI Search for document retrieval
   - Azure Blob Storage for file storage
   - Azure Cognitive Services for vision capabilities

## API Endpoints

- `/chat`: Handle multi-turn conversations
- `/ask`: Handle single-turn questions
- `/chat/stream`: Stream chat responses
- `/upload`: Handle file uploads
- `/delete_uploaded`: Delete uploaded files
- `/list_uploaded`: List uploaded files
- `/config`: Get application configuration

## Configuration

The application is highly configurable through environment variables. Key configuration areas include:

1. **Azure Services Configuration**
   - `AZURE_STORAGE_ACCOUNT`: Storage account name
   - `AZURE_STORAGE_CONTAINER`: Storage container name
   - `AZURE_SEARCH_SERVICE`: Search service name
   - `AZURE_SEARCH_INDEX`: Search index name

2. **OpenAI Configuration**
   - `OPENAI_HOST`: OpenAI host type (azure/local)
   - `AZURE_OPENAI_SERVICE`: Azure OpenAI service name
   - `AZURE_OPENAI_CHATGPT_MODEL`: Model for chat
   - `AZURE_OPENAI_EMB_MODEL_NAME`: Model for embeddings

3. **Authentication Configuration**
   - `AZURE_USE_AUTHENTICATION`: Enable/disable authentication
   - `AZURE_SERVER_APP_ID`: Server application ID
   - `AZURE_CLIENT_APP_ID`: Client application ID

4. **Feature Flags**
   - `USE_GPT4V`: Enable vision capabilities
   - `USE_VECTORS`: Enable vector search
   - `USE_USER_UPLOAD`: Enable file uploads

## Logging and Monitoring

The application includes comprehensive logging and monitoring capabilities:

- Default log level: INFO for application logs
- Configurable through `APP_LOG_LEVEL` environment variable
- Azure Application Insights integration when configured
- OpenTelemetry instrumentation for monitoring

## Development

To run the application locally:

1. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

2. Set up environment variables (use azd or .env file)

3. Run the development server:
   ```bash
   python -m gunicorn main:app
   ```

## Error Handling

The application implements comprehensive error handling:
- HTTP error responses with appropriate status codes
- Structured error responses in JSON format
- Authentication and authorization error handling
- File upload and processing error handling

## Security Features

- Azure AD integration
- Configurable document access control
- Support for private endpoints
- CORS configuration for frontend integration

## Best Practices

The application implements several best practices:
- Clean separation of concerns
- Configuration through environment variables
- Comprehensive error handling
- Structured logging
- Integration with Azure monitoring services
