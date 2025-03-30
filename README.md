# AnyActions: Developing Your AI Agents with Seamless Tool Integration

> Tool usage empowers your LLM agents to interact with external applications via RESTful APIs calls. They are usually either used to do data retrieval (e.g. search a flight schedule) or take action in another application (e.g. file a JIRA ticket).

AnyActions helps you build LLM agents with external tools (web search, check calendar, etc) and manage tool usage authentication easier and faster. 

```python
from anyactions import ActionHub
hub = ActionHub()

# Set up your tool with a single line
tools = hub.tools(["serpapi_google_search"])

# Call LLMs
response = openai.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "What is the weather in Tokyo next week?"}],
    tools=tools,
)
```

## What Makes AnyActions Different?

- **No More Boilerplate**: Focus on agent logic, not API integration
- **Local API Management**: All authentication stored securely on your own environment, not third-party servers
- **Full Code Ownership**: Tool implementations are downloaded to your environment for further customization
- **Custom Tool Creation**: Generate and deploy custom tools on demand

## Core Features

- **ActionHub**: Central management for tool discovery, authentication, and execution
- **Retriever**: Auto-discover existing tools in project directory or generate new ones on demand
- **Actor**: Seamlessly parse LLM decisions and execute appropriate actions
- **Local API Key Management**: Secure handling of credentials on your development device

## Getting Started

`python >= 3.10`

```bash
pip install anyactions
```

For detailed SDK setup instructions, see [AnyActions-SDK/README.md](AnyActions-SDK/README.md)

## Technical Design

ActionHub
- The central orchestrator for tool management, authentication, and execution
- Handles API key CRUD operations with secure local storage
- Manages tool schemas and contexts for LLM integration

Retriever
- Retrieve available tools from AnyActions database
- For unavailable tools, request our AnyActions agent to generate tool usage context and tool functions for you

Actor
- Parse LLM responses for tool usage
- One-to-one client for executing tool functions based on parsed LLM responses

##### Notes
We named with the term `action` based on the [OpenAI convention](https://platform.openai.com/docs/actions/introduction). In Anthropic's documentation, it is equivalent to `tool`. However, we realized that OpenAI also conflates the term `tool` with `action`. They are the same concept in our SDK.

## Acknowledgements
- [Swarm](https://github.com/openai/swarm)
