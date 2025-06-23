# Wikipedia Research Assistant

A powerful AI-powered research assistant that helps users explore Wikipedia content through natural language interactions. This project uses Google's Gemini LLM, the Model Context Protocol (MCP), and LangGraph to create an interactive assistant that can search Wikipedia, retrieve article summaries, list section titles, and extract section content.

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Command Reference](#command-reference)
- [How It Works](#how-it-works)

## Overview

This Wikipedia Research Assistant provides an interactive interface for exploring Wikipedia content using natural language. It leverages:

- **Google Vertex AI**: Uses the Gemini 2.5 Flash model for advanced language understanding
- **Model Context Protocol (MCP)**: Creates a standardized interface for tools and resources
- **LangGraph**: Orchestrates the conversation flow between user, LLM, and tools
- **Wikipedia Python Library**: Accesses Wikipedia content programmatically

## Features

- **Natural Language Search**: Ask questions about any Wikipedia topic
- **Article Summaries**: Get concise summaries of Wikipedia articles
- **Section Navigation**: Explore article sections and get content from specific sections
- **Prompt Templates**: Use pre-defined prompts for common research tasks
- **Suggested Topics**: Access a list of suggested topics to explore
- **Interactive CLI**: Simple command-line interface for interacting with the assistant

## Architecture

The project uses a client-server architecture:

1. **Server (`mcp_server.py`)**: Provides tools to search and retrieve Wikipedia content
2. **Client (`client.py`)**: Connects to the server and creates an interactive interface using LangGraph and Vertex AI

### Available Tools
- `fetch_wikipedia_info`: Search Wikipedia and get article summaries
- `list_wikipedia_sections`: Get section titles from Wikipedia articles
- `get_section_content`: Retrieve content from specific article sections

## Requirements

- Python 3.9+
- Google Cloud Platform account with Vertex AI API enabled
- Wikipedia Python library
- MCP (Model Context Protocol) library
- LangGraph
- LangChain
- Google Cloud authentication set up on your machine

## Installation

1. **Clone the repository**:
   ```
   git clone <repository-url>
   cd WikipediaResearchAssistant
   ```

2. **Create and activate a virtual environment**:
   ```
   python -m venv .venv
   
   # On Windows
   .venv\Scripts\activate
   
   # On macOS/Linux
   source .venv/bin/activate
   ```

3. **Install dependencies**:
   ```
   pip install -r requirements.txt
   ```
   
4. **Set up Google Cloud Authentication**:
   ```
   # Install Google Cloud SDK if not already installed
   # https://cloud.google.com/sdk/docs/install
   
   # Authenticate with Google Cloud
   gcloud auth application-default login
   
   # Set your Google Cloud project
   gcloud config set project wikipedia-search-assistant
   ```

5. **Create a suggested_titles.txt file (optional)**:
   ```
   echo "Quantum Computing
   Artificial Intelligence
   Machine Learning
   Python (programming language)
   Natural Language Processing" > suggested_titles.txt
   ```

## Usage

1. **Make sure your virtual environment is activated**:
   ```
   # On Windows
   .venv\Scripts\activate
   
   # On macOS/Linux
   source .venv/bin/activate
   ```

2. **Run the assistant**:
   ```
   python client.py
   ```

3. **Interact with the assistant**:
   - Type natural language questions about Wikipedia topics
   - Use special commands (see Command Reference below)
   - Type 'exit', 'quit', or 'q' to exit

## Command Reference

The assistant supports several special commands:

- **General queries**: Just type your question about a Wikipedia topic
  ```
  You: Tell me about quantum computing
  ```

- **List available prompts**:
  ```
  You: /prompts
  ```

- **Run a specific prompt**:
  ```
  You: /prompt highlight_sections_prompt "Quantum Computing"
  ```

- **List available resources**:
  ```
  You: /resources
  ```

- **Access a specific resource**:
  ```
  You: /resource suggested_titles
  ```

- **Exit the assistant**:
  ```
  You: exit
  ```

## How It Works

1. The client starts the MCP server as a subprocess
2. The client loads tools from the server using the MCP protocol
3. User queries are sent to the Gemini LLM
4. The LLM decides which tools to use to answer the query
5. Tools access Wikipedia to retrieve relevant information
6. The LLM synthesizes the information into a natural language response
7. The response is displayed to the user