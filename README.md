# 🤖 LangChain AI Chatbot with Gemini, Calculator & Weather Tools

A simple AI chatbot built with **LangChain**, **Google Gemini**, and **OpenWeather API**. The chatbot can:

* 💬 Maintain conversation history
* 🧮 Perform mathematical calculations
* 🌦️ Retrieve real-time weather information
* 🔧 Use LangChain Tool Calling Agent architecture

---

## Features

### 1. Conversational AI

Powered by Google's Gemini model through `langchain-google-genai`.

* Supports natural language conversations
* Maintains chat history using memory
* Uses tool-calling capabilities automatically

---

### 2. Calculator Tool

The chatbot can solve arithmetic expressions.

**Example:**

User:

```text
What is 25 * 18 + 7?
```

Assistant:

```text
457
```

---

### 3. Weather Tool

The chatbot can retrieve real-time weather information from OpenWeather API.

**Example:**

User:

```text
What is the weather like in Hanoi?
```

Assistant:

```text
The current weather in Hanoi is 30.2°C with heavy rain.
```

---

## Project Structure

```text
project/
│
├── chatbot.py
├── .env
├── requirements.txt
└── README.md
```

---

## Technologies Used

* Python 3.10+
* LangChain
* LangChain Classic
* Google Gemini
* OpenWeather API
* Requests
* python-dotenv

---

## Installation

### Clone Repository

```bash
git clone https://github.com/your-username/langchain-weather-chatbot.git

cd langchain-weather-chatbot
```

### Create Virtual Environment

Windows:

```bash
python -m venv .venv

.venv\Scripts\activate
```

Linux/Mac:

```bash
python -m venv .venv

source .venv/bin/activate
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

---

## Environment Variables

Create a `.env` file in the root directory:

```env
GOOGLE_API_KEY=your_google_api_key

OPENWEATHER_APIKEY=your_openweather_api_key
```

---

## Required APIs

### Google Gemini API

Get API key from:

https://ai.google.dev/

---

### OpenWeather API

Get API key from:

https://openweathermap.org/api

---

## Agent Architecture

```text
User
 │
 ▼
Agent Executor
 │
 ├── Calculator Tool
 │
 ├── Weather Tool
 │
 ▼
Gemini LLM
 │
 ▼
Response
```

---

## Available Tools

### Calculator

```python
@tool("calculator")
def calc(expression: str) -> str:
    return str(eval(expression))
```

Used for:

* Addition
* Subtraction
* Multiplication
* Division
* Mathematical expressions

---

### Weather Tool

```python
@tool
def get_weather(city: str) -> str:
```

Uses:

```text
OpenWeather API
```

Returns:

* Weather description
* Current temperature

---

## Conversation Memory

The chatbot currently uses:

```python
ConversationBufferMemory
```

Example:

```python
memory = ConversationBufferMemory(
    return_messages=True,
    memory_key="chat_history"
)
```

### Important Note

`ConversationBufferMemory` has been deprecated in newer versions of LangChain.

Future migration options:

* `create_agent()`
* Short-term memory
* LangGraph Checkpointing
* Store API

Reference:

https://docs.langchain.com/oss/python/langchain/short-term-memory

---

## Example Usage

```python
chat("What is 15 * 8?")
```

Output:

```text
120
```

---

```python
chat("What is the weather like in Hanoi?")
```

Output:

```text
The current weather in Hanoi is 30.2°C with heavy rain.
```

---

## Future Improvements

* Replace deprecated memory implementation
* Add web search tool
* Add Wikipedia tool
* Add vector database memory
* Add Retrieval-Augmented Generation (RAG)
* Add Streamlit user interface
* Add FastAPI backend
* Add Docker support
* Add LangGraph workflow

---

## Known Limitations

### Calculator

Current implementation uses:

```python
eval()
```

This is not recommended for production environments because it may execute arbitrary code.

Safer alternatives:

* numexpr
* sympy
* LLMMathChain replacement
* custom parser

---

### Memory

Current memory implementation is deprecated and should be migrated to newer LangChain memory systems.

---

## Sample Interaction

```text
User:
What is the weather like in Hà Nội?

Agent:
Invoking get_weather...

Tool:
Current weather in Hà Nội:
heavy intensity rain, 30.26°C

Assistant:
The current weather in Hà Nội is 30.26°C with heavy rain.
```

---

## License

MIT License

Feel free to fork, modify, and contribute.
