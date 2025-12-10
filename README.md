# 📦 MCP Filesystem & Fetch Servers — Claude Desktop Integration

This repository contains a complete setup for running Model Context Protocol (MCP) servers inside Claude Desktop, including:

* A fully working Filesystem MCP Server

* A custom Python-based Fetch MCP Server

* A Windows-compatible npx wrapper to avoid path errors

* Templates, documentation, and examples for generating project tree structures and high-level technical documentation

This project shows how to extend Claude Desktop so it can browse local directories, read files, and interact with your machine through custom MCP tools.


## 🚀 Features

### 🔹 Filesystem MCP Server

Allows Claude Desktop to:

* List folders

* Read file contents

* Generate tree structures

* Assist with documentation, code inspection, and analysis

### 🔹 Custom Fetch MCP Server

A Python server that handles custom fetch or processing logic.
Useful for:

* Fetching external API data

* Resolving assets

* Automating project-specific tasks

### 🔹 Windows Path Compatibility

Includes a simple npx-wrapper.cmd to fix the Windows "C:\Program Files" breaking the filesystem MCP server.

### 🔹 Documentation Tools

Examples and templates for:

* Generating a directory tree

* Producing high-level technical documentation

* Organizing project files for LLM-assisted analysis

## 📁 Project Structure

```
mcp-project/
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


## 🛠️ Setup Instructions

### 1️⃣ Install Python Dependencies

```
pip install -r requirements.txt
```

Requires Python 3.10+.

### 2️⃣ Install Node.js (for filesystem MCP server)

Download from:
https://nodejs.org/

Node.js 18+ is recommended.

### 3️⃣ (Windows Only) Fix npx Path Issues

If Claude Desktop fails to run the Node-based filesystem server, use the included wrapper:

tools/npx-wrapper.cmd
```
@"C:\Program Files\nodejs\npx.cmd" %*
```

This ensures npx works even when installed in a folder with spaces.

### 4️⃣ Configure Claude Desktop

Copy the provided template:
```
claude_config_template.json
```

into your Claude Desktop config directory:
```
C:\Users\<YOUR_USERNAME>\AppData\Roaming\Claude\claude_desktop_config.json
```

Modify the paths inside the file to match your system.

## 🧪 Usage
### 📂 Generate a Tree Structure

Inside Claude Desktop, run:
```
Show me the tree structure of this project.
```

or specify a path:
```
Generate a directory tree for this folder.
```

Claude will read files using the Filesystem MCP server and produce a structured output.

## 📘 Generate High-Level Technical Documentation

Ask Claude:
```
Analyze this project and generate high-level technical documentation.
```

Claude will use the MCP server to read files and produce a detailed technical_documentation.md.

## 🔍 Why This Project Exists

This repository demonstrates how to:

* Integrate Claude Desktop with local system tools

* Use MCP servers to enhance AI workflows

* Automate documentation and project introspection

* Handle Windows-specific Node.js path issues reliably

It serves as a starter template for developers exploring the full power of Model Context Protocol.

## 🤝 Contributing

Contributions, improvements, or additional MCP modules are welcome.

## 📄 License

MIT License.
