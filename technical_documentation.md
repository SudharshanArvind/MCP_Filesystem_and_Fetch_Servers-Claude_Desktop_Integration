# 📘 Technical Documentation

## MCP Filesystem & Fetch Servers — Claude Desktop Integration

## 1. Overview

This project provides a complete setup for running Model Context Protocol (MCP) servers inside Claude Desktop, enabling powerful local-system integrations such as:

* Browsing your computer’s filesystem

* Reading project files

* Generating tree structures

* Producing high-level documentation

* Running custom Python MCP servers (e.g., fetchers, utilities, or automation tools)

The repository also includes Windows-friendly configurations and wrappers that fix path-related issues commonly encountered when using Node-based MCP tools.

## 2. System Architecture

The project consists of three main components:

### 2.1 Filesystem MCP Server

* Provided by: @modelcontextprotocol/server-filesystem

* Executed through npx

* Allows Claude Desktop to:

    * Access directories

    * Read files

    * Provide contextual analysis over project structures

A custom wrapper (tools/npx-wrapper.cmd) ensures the server works correctly on Windows environments where C:\Program Files\nodejs\npx.cmd may break due to spaces in the path.

### 2.2 Fetch MCP Server (Custom Python Server)

Located under:
```
src/fetch/server.py
```

This server is built using the mcp or fastmcp Python libraries.
It allows Claude Desktop to:

* Perform external HTTP requests

* Retrieve remote project data

* Act as a general-purpose extension point for custom backend logic

This MCP server communicates with Claude using JSON-RPC over standard input/output.

### 2.3 Client Integration (Claude Desktop)

Claude is configured to communicate with both servers using a file named:
```
claude_desktop_config.json
```

For safety, the repo contains only a template:
```
claude_config_template.json
```

Users replace template values with their local machine paths.

## 3. Directory Structure

Below is the recommended structure included in this repository:
```
mcp-project/
│
│
├── tools/
│   └── npx-wrapper.cmd
│
├── docs/
│   ├── tree_structure.txt
│   └── technical_documentation.md
│
├── claude_config_template.json
├── requirements.txt
└── README.md
```

Each folder serves a dedicated purpose:

* src/ → MCP servers

* tools/ → OS helpers

* docs/ → Generated documentation

* configuration → Safe templates for Claude integration

## 4. Installation Requirements
### 4.1 Python

* Version: 3.10+

* Dependencies installed via:
```
pip install -r requirements.txt
```

### 4.2 Node.js

* Version: 18+

* Required for filesystem MCP server

* Installed from: https://nodejs.org/

### 4.3 Claude Desktop

* Required for local MCP integrations

* Automatically loads MCP servers defined in claude_desktop_config.json

## 5. How the MCP Servers Work

### 5.1 Filesystem Server (Node.js)

Claude launches the server using:
```
npx -y @modelcontextprotocol/server-filesystem <PATH>
```

The server:

* Watches a directory

* Responds to Claude's requests

* Returns file lists and file contents

The included wrapper:
```
tools/npx-wrapper.cmd
```

ensures that this command executes correctly even if Node is installed in a path with spaces.

### 5.2 Fetch MCP Server (Python)

Executed with:
```
python server.py
```

This server typically defines:

* Endpoints

* Tools (fetch, get, resolve)

* Optional parameters

* Custom logic for remote or local operations

Claude communicates through standard I/O using the MCP protocol.

## 6. Using the Project

### 6.1 Generating a Tree Structure

In Claude Desktop:
```
Show me the tree structure of this project.
```

Claude will use the filesystem MCP server to traverse the directory and generate a hierarchical view.

Tree outputs can be saved into:
```
docs/tree_structure.txt
```
### 6.2 Generating High-Level Documentation

Ask Claude:
```
Analyze this project and generate high-level technical documentation.
```

Claude will read files through MCP and produce documentation like this file.

### 6.3 Using the Fetch Server

Typical interactions include:

* Fetching external URLs

* Querying APIs

* Processing or transforming JSON data

* Auto-fetching related resources for your project

You can extend the fetch server by adding Python functions and exposing them as MCP tools.

## 7. Extending the Project

You can easily add more servers, such as:

* A Git MCP server (interact with repositories)

* A Database MCP server

* A Custom File Processing MCP server

* A Local Search MCP server (indexing your documents)

Each server simply needs to be added under src/ and mapped inside the Claude config.

## 8. Common Issues & Fixes (Windows)

### 8.1 “Server disconnected”

Most common cause:
npx is inside C:\Program Files\... and Claude cannot run it.

Solution: Use the included wrapper:

npx-wrapper.cmd

### 8.2 “not recognized as an internal or external command”

Cause: Incorrect paths in Claude config.

Fix: Update:
```
"command": "C:/Users/<USERNAME>/npx-wrapper/npx.cmd"
```
### 8.3 httpx dependency conflicts

Avoid mixing versions of:

* fastmcp (requires newer httpx)

* mcp-server-fetch (uses older httpx)

Use the compatible versions included in requirements.txt.

## 9. Conclusion

This repository demonstrates a fully working implementation of Model Context Protocol integration with Claude Desktop, providing:

* Local filesystem access

* Custom Python-based MCP tools

* Windows compatibility enhancements

* Automated project documentation workflows

It serves as a practical template for anyone building powerful local AI tooling using Claude and MCP.

## 10. Author & Contributions

Contributions, extensions, and improvements are welcome.
Feel free to fork and create your own MCP servers based on this foundation.
