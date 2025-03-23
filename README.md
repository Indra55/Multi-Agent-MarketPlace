# AgentMesh

A flexible framework for creating and managing networks of specialized AI agents that can work together on complex business tasks.

## Overview

The Multi-Agent Connector allows you to:

- Create networks of specialized AI agents
- Define and manage task workflows between agents
- Support multiple business domains (Corporate, Marketing)
- Handle complex dependencies between tasks
- Integrate with external tools and APIs

## Features

- **Dynamic Agent Network Creation**: Build and modify agent networks at runtime
- **Domain-Specific Agents**:
  - Corporate Agents (Meeting Summarizer, Email Manager, etc.)
  - Marketing Agents (SEO Optimizer, Post Creator, etc.)
- **Task Management**:
  - Sequential task execution
  - Dependency handling
  - PDF document processing
  - Web scraping capabilities
- **API Integration**:
  - RESTful API endpoints
  - Flask-based web server
  - CORS support
- **Extensible Architecture**:
  - Easy to add new agent types
  - Configurable task definitions
  - Flexible output formats

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd multi-agent-connector
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Set up environment variables:
```bash
cp .env.example .env
# Edit .env with your API keys
```

## Requirements

- Python 3.12+
- Flask
- crewai
- crewai-tools
- langchain
- And other dependencies listed in requirements.txt

## Project Structure

```
Agents/
├── agent_definitions/    # Agent type definitions
│   ├── corporate_agents/
│   └── marketing_agents/
├── task_definitions/     # Task type definitions
│   ├── corporate_tasks/
│   └── marketing_tasks/
├── agents.py            # Agent factory classes
├── tasks.py            # Task factory classes
├── api.py             # API implementation
├── app.py            # Flask web server
├── main.py          # Core network logic
└── task_utils.py   # Utility functions
```

## Usage

### Starting the Server

```bash
python app.py
```

The server will start on `http://localhost:4000`

### Creating an Agent Network

```python
from main import CrewNetwork

# Create a network
network = CrewNetwork()

# Add agents
network.add_agent_node("summarizer", "meeting_summarizer", "corporate")
network.add_agent_node("email_manager", "smart_email_manager", "corporate")

# Add tasks
network.add_task_node(
    "summarize_meeting",
    "meeting_summarization",
    "summarizer",
    params={"meeting_text": "Meeting content..."}
)

# Run the network
crew = network.build_crew()
result = crew.kickoff()
```

### API Endpoints

- `POST /networks`: Create a new agent network
- `GET /agents/types`: Get available agent types
- `GET /tasks/types`: Get available task types
- `PUT /networks/<network_id>`: Update network configuration
- `POST /networks/<network_id>/run`: Execute network tasks

## Testing

Run the test suite:

```bash
python test_domain_factories.py
python test_pdf_workflow.py
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

