# **🧠 MCP Architecture Overview**

## **📌 What is MCP?**

- **MCP (Model Context Protocol)** is a **client-server architecture** designed to connect **LLM applications** to external data sources.
- It enables **communication** through structured messages and supports **tools**, **resources**, and **prompt templates**.

## **🏗️ Architecture Breakdown**

### **1. Key Components**

- **Client**: Interfaces with the server and invokes tools/resources.
- **Server**: Exposes capabilities via tools, resources, and prompts.
- **Host**: An application (e.g. Claude Desktop, Cursor) that contains multiple clients and maintains their connections.

### **2. Client-Server Relationship**

- 1:1 connection between client and server.
- Communication via **messages defined by the MCP protocol**.
- Clients live inside hosts; servers expose lightweight functionality.

## **⚙️ Primitives (Core Building Blocks)**

### **🧰 Tools**

- Functions invoked by clients (similar to POST).
- Used for **data retrieval, searching, updating**, etc.
- Example: ListTables for an SQLite server.

### **📂 Resources**

- **Read-only context or data** (similar to GET).
- Examples: DB records, PDFs, API responses.
- Can be accessed directly by clients without a tool call.

### **🧾 Prompt Templates**

- Predefined, reusable prompts stored on the server.
- Help abstract away prompt engineering from users.
- Dynamic data can be injected before execution.

## **🔁 Communication Flow**

### **💬 Message Exchange Process**

1. **Initialization**:
   - Client sends request.
   - Server responds and confirms via notification.
2. **Message Exchange**:
   - Requests, responses, and notifications are exchanged both ways.
3. **Termination**:
   - Connection ends cleanly after operations complete.

![image.png](attachment:f44285d5-2908-42b2-9e44-a9590daf8914:image.png)

## **🚚 Transports (Communication Methods)**

### **1. Standard I/O**

- Used locally.
- Client launches the server as a subprocess.

![image.png](attachment:6f7751b1-04d0-4ef8-b4f6-a48793530302:image.png)

### **2. HTTP + Server-Sent Events (SSE)**

- Used for **stateful** remote communication.
- Keeps a persistent connection open.

### **3. Streamable HTTP (Newer)**

- Supports **both stateful and stateless** communication.
- Recommended for future use.

![image.png](attachment:55dfe768-ddc9-45f6-9461-e988b48727d5:image.png)

![image.png](attachment:81ce7a4f-87cf-4843-b9f9-525ba42c1197:image.png)

## **🛠️ Server & Client Development**

### **✅ Tools**

- Defined via decorators.
- Schema auto-generated from function inputs/outputs.

### **📘 Resources**

- Defined with a URI and MIME type.
- Can be direct or templated (dynamic).

### **💬 Prompts**

- Defined with message templates.
- Users inject dynamic data before execution.

## **💡 Example Use Case**

- Claude Desktop connects to an SQLite MCP server.
- User can:
  - View tables.
  - Analyze product data.
  - Visualize using built-in tools.
  - Seed database with structured prompt templates.

## **🔄 Recap**

- **MCP enables modular, powerful AI applications** by structuring interactions between LLMs and external systems.
- Offers strong separation of concerns:
  - **Clients request**.
  - **Servers serve**.
  - **Hosts orchestrate**.
- Core tools: Tools, Resources, and Prompts.
