
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

# Define agents
web_search_agent = Agent(
    name="Web Search Agent",
    role="Search the web for information",
    model=Groq(id="llama-3.2-90b-vision-preview", api_key=groq_api_key),
    tools=[DuckDuckGo()],
    instructions=["Always include sources"],
    show_tools_calls=True,
    markdown=True,
)

finance_agent = Agent(
    name="Finance AI Agent",
    model=Groq(id="llama-3.2-90b-vision-preview", api_key=groq_api_key),
    tools=[YFinanceTools(stock_price=True, analyst_recommendations=True, stock_fundamentals=True, company_news=True)],
    instructions=["Use tables to display the data"],
    show_tool_calls=True,
    markdown=True,
)

multi_ai_agent = Agent(
    model=Gemini(id="models/gemini-2.0-flash-exp"),
    team=[web_search_agent, finance_agent],
    instructions=["Always include sources", "Use tables to display the data"],
    show_tools_calls=True,
    markdown=True,
)

# Execute a query
multi_ai_agent.print_response("Summarize analyst recommendation and share the latest news for NVDA", stream=True)

#
