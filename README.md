# Financial-Agent-using-Agentic-AI
# Multi-Agent AI System Using Phi-Agents, Groq, and Gemini

## Overview
This project utilizes a multi-agent AI system powered by **Phi-Agents**, integrating models from **Groq** and **Google Gemini** to perform web search and financial analysis tasks efficiently. 

## Features
- **Web Search Agent**: Searches the web for relevant information using **Groq's Llama 3.2-90B Vision Preview** model and **DuckDuckGo** as a search tool.
- **Finance AI Agent**: Fetches stock market data, analyst recommendations, company fundamentals, and news using **Groq's Llama 3.2-90B Vision Preview** model and **YFinanceTools**.
- **Multi-Agent System**: A collaborative AI system managed by **Google Gemini**, orchestrating the web search and finance agents to provide structured, informative responses.

## Installation
Ensure you have the required dependencies installed:
```sh
pip install phi-agent dotenv
```

## Setup
1. Clone this repository:
```sh
git clone https://github.com/your-repo/multi-agent-ai.git
cd multi-agent-ai
```
2. Install the required dependencies.
3. Create a `.env` file in the root directory and add:
```sh
GROQ_API_KEY=your_groq_api_key
```
4. Load the environment variables in your Python script:
```python
from dotenv import load_dotenv
import os
load_dotenv()
groq_api_key = os.getenv("GROQ_API_KEY")
```

## Usage
Run the script to retrieve financial insights and news about **NVDA (NVIDIA Corporation)**:
```sh
python main.py
```

## Implementation
```python
from phi.agent import Agent
from phi.model.groq import Groq
from phi.tools.yfinance import YFinanceTools
from phi.tools.duckduckgo import DuckDuckGo
from phi.model.google import Gemini

#
