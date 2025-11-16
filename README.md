# ADK Visual Builder

A **no-code** visual interface for building and managing AI agents using Google's Agent Development Kit (ADK). Build complex multi-agent systems through an intuitive drag-and-drop interface without writing any YAML or code.

![ADK Visual Builder - No Code Interface](.images/adk-no-code-builder.png)

*The ADK Visual Builder provides a complete no-code interface for building and managing AI agents*

## Google ADK Visual Builder

The ADK Visual Agent Builder (available in ADK v1.18.0+) provides a powerful no-code interface for building and managing agents. [Learn more about v1.18.0 features](https://github.com/google/adk-python/releases/tag/v1.18.0)

![ADK Visual Builder Demo](.images/adk-visual-agent-builder-demo.gif)

*Watch the ADK Visual Builder in action - build agents visually with drag-and-drop!*

![Google ADK Visual Builder Overview](.images/Google-ADK-Visual-Builder.gif)

*Complete overview of the ADK Visual Builder no-code interface*

## Table of Contents

- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Setup](#setup)
- [Google ADK Visual Builder](#google-adk-visual-builder)
  - [Step 1: Start the Web Server](#step-1-start-the-web-server)
  - [Step 2: Access the Web UI](#step-2-access-the-web-ui)
  - [Step 3: Create or Edit Agents](#step-3-create-or-edit-agents)
  - [Step 4: Use Gemini Assistant (Optional)](#step-4-use-gemini-assistant-optional)
  - [Step 5: Add Tools](#step-5-add-tools)
  - [Step 6: Add Sub-Agents](#step-6-add-sub-agents)
  - [Step 7: Add Callbacks](#step-7-add-callbacks)
- [Agent Types](#agent-types)
- [Demo: Financial Agent Example](#demo-financial-agent-example)
  - [Financial Agent Demo](#financial-agent-demo)
- [Understanding the `tmp` Directory Structure](#understanding-the-tmp-directory-structure)
  - [Why This Structure Exists](#why-this-structure-exists)
- [Resources](#resources)

## Project Structure

This repository contains agent configurations organized by subagents wise each yaml generated from visual builder:

```
.
├── financial_agent/          # Financial data agents
│   ├── root_agent.yaml       # Main orchestrator agent
│   ├── company_orchestrator.yaml
│   ├── current_share_price_agent.yaml
│   ├── earnings_call_agent.yaml
│   ├── final_aggregator_agent.yaml
│   ├── financial_data_orchestrator.yaml
│   ├── key_financials_agent.yaml
│   ├── latest_news_agent.yaml
│   ├── latest_news_on_ticker_agent.yaml
│   ├── parallel_data_gatherer.yaml
│   ├── ten_k_summary_agent.yaml


```

## Getting Started

### Prerequisites

- Python 3.13+
- **ADK version 1.18.0 or higher** (required for Visual Builder features)

**Note**: The ADK Visual Builder is available starting from ADK v1.18.0. Make sure you have this version or later installed to use the no-code visual interface.

### Setup

1. Create and activate a virtual environment:
```bash
python3 -m venv .venv
source .venv/bin/activate
```

2. Install ADK:
```bash
pip install google-adk
```

3. Verify ADK is installed:
```bash
adk --help
```

### Step 1: Start the Web Server

```bash
adk web
```

This starts a FastAPI server with a web UI for visually building and editing agents.

### Step 2: Access the Web UI

Open your browser and navigate to the URL shown in the terminal (typically `http://localhost:8000` or similar).

### Step 3: Create or Edit Agents

**Creating New Agents:**
1. Click the **"+"** button next to the agent dropdown to create a new agent in builder mode
   
   ![Create Agent in Builder Mode](.images/create-agent-builder-mode.png)
   
   *Click the "+" button to create a new agent in builder mode - no code required!*

2. Use the visual interface to design workflows, configure settings, and test your agent

**Editing Existing Agents:**
1. Select the agent from the dropdown menu
2. Click the **pencil/edit icon** next to the agent dropdown
   
   ![Edit Agent in Builder Mode](.images/edit-agent-builder-mode.png)
   
   *Click the edit icon to modify an existing agent - all changes are made visually!*

3. Modify workflows, tools, sub-agents, and callbacks through the visual interface
4. Test changes in real-time with the integrated chat
5. Changes are saved to the `tmp` directory as drafts - publish when ready

### Step 4: Use Gemini Assistant (Optional)

The Visual Builder includes a **Gemini Assistant** panel that helps you build agents using natural language.

![Gemini Assistant in Visual Builder](.images/adk-visual-builder-prompt.png)

*The Gemini Assistant helps you build agents through natural language conversation - completely no-code!*

**Example prompt:**
```
Build a multi-agent financial analysis system where the user provides a company ticker or symbol and primary orchestration agent should be Sequential Agent which should run several agents in parallel, with each agent responsible for one task:
Fetch the current share price
Generate a 10-line summary of the latest 10-K
Extract key financial metrics (EBITDA, EPS, net revenue, etc.)
Produce an earnings call summary
Retrieve latest news highlights
After all agents complete their tasks, an Aggregator agent should combine all outputs into a single, clean, well-structured report. Use Gemini 2.5 Flash as the LLM and google_search as the built-in tool for data retrieval.
```

The assistant will automatically generate all YAML configuration files for you!

### Step 5: Add Tools 

Click the **"+"** button next to "Tools" to add:

1. **Function Tool**: Custom Python functions
2. **Built-in Tool**: Pre-built tools (google_search, EnterpriseWebSearch, VertexAISearchTool, FilesRetrieval, load_memory, url_context, etc.)
3. **Agent Tool**: Other agents that can be invoked as tools

![ADK Visual Builder - Built-in Tools](.images/adk-visual-builder-build-intools.png)

*The "Add Built-in Tool" dialog showing available built-in tools organized by category*

### Step 6: Add Sub-Agents

1. Locate the "Sub Agents" section
2. Click the "+" button to add a new sub-agent
3. Choose from: LLM Agent, Sequential Agent, Loop Agent, or Parallel Agent

### Step 7: Add Callbacks

1. Locate the "Callbacks" section
2. Click the "+" button to add a new callback
3. Select the callback type (Before/After Agent, Before/After Model, Before/After Tool)
4. Configure and save

**You never need to manually create or edit YAML files** - the Visual Builder handles everything for you!

## Agent Types

The Visual Builder supports these agent types:

- **LlmAgent**: Single LLM-based agent for straightforward tasks
- **SequentialAgent**: Executes sub-agents one after another in sequence
- **ParallelAgent**: Executes sub-agents simultaneously for improved performance
- **LoopAgent**: Iterates over sub-agents with loop control logic
- **WorkflowAgent**: Complex workflow orchestration with conditional logic

All agent types can be created and configured entirely through the Visual Builder interface - no YAML editing required!

## Demo: Financial Agent Example

This repository includes a **demo implementation** of a comprehensive multi-agent system for gathering financial information about companies. This serves as an example of what you can build using the ADK Visual Builder.

### Financial Agent Demo
A comprehensive multi-agent system for gathering financial information about companies. The system includes:

- **Root Company Orchestrator**: Primary orchestrator that validates company tickers and coordinates data gathering
- **Company Orchestrator**: Validates and resolves company information
- **Current Share Price Agent**: Retrieves real-time stock prices
- **Earnings Call Agent**: Fetches earnings call transcripts and summaries
- **Key Financials Agent**: Gathers key financial metrics and ratios
- **Latest News Agent**: Retrieves recent news about companies
- **10-K Summary Agent**: Extracts and summarizes 10-K filing information
- **Financial Data Orchestrator**: Coordinates financial data collection
- **Parallel Data Gatherer**: Efficiently gathers multiple data points in parallel
- **Final Aggregator Agent**: Aggregates and formats final results


## Understanding the `tmp` Directory Structure

When using the ADK Visual Builder web UI, you'll notice a `tmp` directory structure like:

```
agent_name/
├── root_agent.yaml          # Published/production version
└── tmp/
    └── agent_name/
        └── root_agent.yaml   # Draft/staging version
```

### Why This Structure Exists

The ADK Visual Builder uses a **draft/staging pattern**:

- **`tmp/{agent_name}/`**: Temporary staging area where changes are saved while editing in the web UI
- **`{agent_name}/`**: Production area containing the published/final version

This allows you to:
- Make changes without immediately affecting the production agent
- Cancel changes and restore from the main directory
- Have a clear separation between draft and published versions

**Note**: The `tmp` directory is automatically created by the web UI when you edit agents. You can safely ignore it or exclude it from version control if desired.

## Resources

- [ADK Python v1.18.0 Release Notes](https://github.com/google/adk-python/releases/tag/v1.18.0) - Includes Visual Agent Builder features
- [ADK Python GitHub Repository](https://github.com/google/adk-python)

