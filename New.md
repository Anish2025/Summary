# AI Agent Week 4.2 Agentic Tools and MCP Protocols

# Introduction

AI agents can effectively interact with their environment and perform tasks through standardization, specifically using the Minimum Context Protocol (MCP), and by leveraging tools, fine-tuning, collaboration, and prompt optimization.

# Core Pillars of Agent Systems

Agent systems are built upon four core pillars that are :

• **Prompt Engineering** (or Prompt Optimization): This is identified as one of the fundamental pillars. The course, at the moment, considers the direct instruction on prompt engineering to be largely covered, emphasizing the need to improve skills in this area.

• **Tools**: Tools are fundamental to the definition of an agent. An agent is an "autonomous reasoning entity" that interacts with an external environment. Tools serve as the "sensors and actuators" that allow an agent to observe and act upon its environment.

- Even a single agent requires at least two tools: one for sensing the environment and one for acting upon it. For example, an LLM acting as an agent needs tools like web search or a weather API to access external data (e.g., to answer "what's the weather today?")
- The effectiveness of an agent often stems from the variety and number of tools it can access.
- Tools are not limited to simple functions; they can also be complex, intelligent AI applications, and one agent can even treat another agent as a tool.
- The **Model Context Protocol (MCP)** is a significant effort to standardize how tools are created and accessed . This protocol aims to simplify communication between agents and tools by providing a "minimum viable framework" for exposing tools, resources, and prompts. It is designed to allow agents to discover and utilize tools without needing custom client-side code for each API.

    ▪ Within MCP, there are three primary resources: tools, resources, and prompts.

    -  **Prompts**: Can be exposed as a library, as crafting good prompts requires significant effort and they are valuable assets worth sharing. While this is considered the "least used part of MCP," it holds great value.

    - **Resources**: Often used for simple lookups or operations that return a result instantly, like exposing a weather API.

    - **Tools**: Generally involve more significant computation or actions, such as a Retrieval Augmented Generation (RAG) system that interprets search results and answers questions.

    ▪ The distinction between tools and resources can sometimes be a "sliding scale" and is not always a "watertight separation".

    ▪ The quality and clarity of the description provided for a tool, resource, or prompt within the MCP server are crucial. This description acts as a "prompt for the agent's consumption" and guides the agent on when and how to use the tool, especially when multiple tools have overlapping functionalities.

-  Various agentic frameworks like Crew AI and LangGraph exist, and they all incorporate tool frameworks. The course specifically mentions creating tools using Crew AI and MCP.

- Fast MCP (version V2) is recommended for creating MCP tools, as it represents a more mature and updated version compared to the official MCP SDK.

• **Fine-tuned Agents**: This pillar involves enhancing agent performance through fine-tuning. The two main methods for fine-tuning are supervised fine-tuning and reinforcement learning. Fine-tuning can be applied either to the agents themselves or to the collaboration mechanisms between agents.

• **Better Collaboration**: This is the fourth core aspect, emphasizing the importance of agents working together effectively. Just as with human teams, a project can fail if talented individuals (or agents) do not collaborate well.

The concept of tools and their standardization through protocols like MCP is critical, especially as it allows for a "distributed compute framework" where agents can treat other agents as tools, creating a "graph of tools". This standardization (like the historical shift from SOAP to REST) solves the "tower of babel problem" by enabling different systems to communicate seamlessly without extensive custom coding.

# Understanding Tools in Agentic Systems

In agentic systems,**tools are essential for agents to interact with and act upon the external environment**, functioning much like "sensors and actuators" in traditional agent definitions. An LLM agent, for example, needs tools like a web search or a weather API to access external data or functionalities.

Historically, there was a **"proliferation of agentic frameworks"**, each with its own tool framework, leading to a "mess" and a lack of interoperability. This situation was akin to the "Tower of Babel problem," where different frameworks couldn't easily communicate, requiring custom client-side code for each proprietary API.

To address this,**Anthropic developed the Model Context Protocol (MCP)**, described as a "minimum viable framework" or "minimum protocol" that is "completely unopinionated" and simple. MCP, which has the "spirit of REST," serves to "augment the context or make tools available" to the agent. Its **"wildfire" adoption**by companies like Google and OpenAI signifies a "massive migration" towards this standard.

MCP exposes three types of "resources" via an MCP server:

  • **Tool**: Often implies "heavyweight computation" or complex actions, potentially even intelligent AI applications or other agents.

   • **Resource**: Typically provides "instant result" or a "lookup" like a weather API. The distinction between tools and resources can be a "sliding scale".

   • **Prompt**: Allows for sharing a "library of prompts," recognizing that crafting good prompts is a valuable effort worth sharing.

Agents discover and decide which tool to use by **reading the quality of description** exposed by the MCP server, which acts as "prompts for the agent's consumption". Tools should ideally be **stateless functions** to ensure consistency. A key benefit of MCP is that it **eliminates the need for custom client-side coding** because agentic frameworks are designed to communicate with MCP. The recommended implementation for creating MCP tools and servers is to use the **latest V2 version of **`fastmcp`

# Agentic Frameworks

Agentic frameworks are evolving software structures designed to **facilitate the creation and operation of autonomous agents**. They represent an intermediate step in the development of a full "agentic operating system," a future where agents function akin to threads and processes in a traditional OS, although "we are not there yet".

Here's a breakdown of agentic frameworks from the sources:

• **Role in Agentic Systems**: Agentic frameworks are built to enable agents, which are defined as "autonomous reasoning entities that engage with an external environment". This engagement involves observing and acting upon the environment, a loop facilitated by components like tools, traditionally known as sensors and actuators.

• **Proliferation and Immaturity**: The agentic world has seen a **"whole proliferation of agentic frameworks"** such as Crew AI, LangGraph, and Agno. At present, these frameworks are described as having "different degrees of immaturity," indicating that the field is still evolving and "nobody has really figured it out" yet. Despite their nascent stage, they are practically useful for solving real-world problems.

• **Internal Tool Frameworks:** A significant characteristic of these early agentic frameworks is that **"all these agents have their tools framework"**. For example, Crew AI has its own tools framework where functions can be annotated or inherit from a base tools class. LangGraph also has its own approach. This led to a "mess" because each framework developed its "heavyweight opinionated frameworks" for tools, making interoperability difficult56. One company's tools could not easily engage with another's, requiring developers to write custom client-side code for each proprietary API or tool. This problem was likened to the "Tower of Babel" where everyone spoke different languages, hindering communication.

• **The Model Context Protocol (MCP) as a Standardization Solution**: To address the lack of standardization and interoperability, **Anthropic created the Model Context Protocol (MCP). MCP** is a "minimum viable framework" or "minimum protocol" that is "completely unopinionated" and simple, aiming to provide a common communication method for tools across different systems. Its "spirit of REST" allows it to be a more lightweight alternative to earlier, more burdensome protocols like SOAP in web services. MCP has gained **"wildfire" adoption** across the industry, with companies like Google and OpenAI adopting it, leading to a "massive migration" towards its use. The primary benefit of MCP is that it **eliminates the need for custom client-side coding** to integrate various tools. Instead, most agentic frameworks are now being designed to "know how to talk to MCP," making tool integration seamless without requiring manual coding for each tool.

• **Agent Decision-Making and Tool Discovery**: Agentic frameworks, by integrating tools via MCP, empower agents (which are "autonomous reasoners") to plan subtasks and decide which tools to utilize. Agents discover available tools by reading their **descriptions exposed by an MCP** server. The quality and clarity of these tool descriptions are paramount, acting as "prompts for the agent's consumption". This allows agents to understand when and how to use a tool, especially when faced with overlapping functionalities, and prevents them from bypassing useful tools.

• **Distributed Compute Framework**: MCP supports a vision where agentic systems operate within a **"distributed compute framework"** or a "graph of tools," much like a fabric of microservices. An MCP server can act as a proxy, calling other MCP servers or tools, enabling complex architectures where one agent might even treat another agent as a tool.

• **Current State of Integration**: While Crew AI had "very poor support for MCP" or "almost zero integration" at the time of the discussion, the overall trend is towards agentic frameworks becoming MCP compliant. Developers are encouraged to use the V2 version of `fastmcp` (an open-source project adopted by MCP) to create MCP tools and servers, which simplifies the process significantly

#  MCP (Model Context Protocol)

**The Model Context Protocol (MCP)** is a **minimum viable framework or protocol developed by Anthropic to standardize how agents interact with tools**. It aims to solve the "Tower of Babel problem" that arose from the "whole proliferation of agentic frameworks", each with its own "heavyweight opinionated frameworks" for tools.

Here's a comprehensive breakdown of MCP:

• **Purpose and Analogy**
- MCP's core purpose is to **augment the context or make tools available to an agent**, which is an autonomous reasoning entity that engages with an external environment.

- It has been described as the **"USB for tools access"** or akin to "extension cards", providing a simple, unopinionated, and minimalistic standard.

- The goal is for agents to function similarly to how threads and processes operate in a traditional operating system, moving towards an "agentic operating system".

• **Problem it Solved (The "Tower of Babel")**

- Before MCP, each agentic framework (like Crew AI, LangGraph, Agno) developed its own internal "tools framework". This created a "mess" where one company's tools could not easily engage with another's, requiring developers to write custom client-side code for each proprietary API or tool.

- This situation was compared to the "Tower of Babel problem," where different systems couldn't communicate effectively.

• **Anthropic's Contribution and "Spirit of REST"**

- Anthropic created MCP as a **simple, "completely unopinionated"** protocol.

- It has the **"spirit of REST"**, contrasting with earlier, more "heavyweight" and "burdensome" protocols like SOAP in web services6. This means it focuses on simplicity and stateless interactions.

• **Resources Exposed via MCP Server**

- An MCP server exposes three types of "resources":

  • **Tool**: Often implies "heavyweight computation" or complex actions, potentially even intelligent AI applications or other agents.

   • **Resource**: Typically provides "instant result" or a "lookup" like a weather API. The distinction between tools and resources can be a "sliding scale and is not always a "watertight separation".

   • **Prompt**:Allows for sharing a "library of prompts". Crafting good prompts is a valuable effort, and MCP recognizes that "prompt is an asset" worth sharing and publishing. This is considered the "least used part of MCP but of great value".


• **Agent Tool Discovery and Usage**

- Agents discover and decide which tool to use by **reading the "quality of description"** exposed by the MCP server. These descriptions act as **"prompts for the agent's consumption"**, serving as "context of the tool".

- It is "vitally important" to document tools as clearly as possible, especially when agents have access to "lots of tools with overlapping functionality". Poor descriptions can lead agents to bypass useful tools.

- Agents are "autonomous reasoners" that plan subtasks and can lean upon tools to accomplish these subtasks. For example, an agent might use a weather tool to determine if a package will be delayed.

• **Stateless Functions**

- Tools should ideally be **stateless functions** to ensure consistency and prevent remembering previous interactions, much like REST APIs.

• **Elimination of Custom Client-Side Coding**

- A key benefit of MCP is that it **eliminates the need for custom client-side coding**.

- Instead of writing specific client code for each vendor's API, agentic frameworks are now designed to "know how to talk to MCP", enabling seamless tool integration.

- This is a "massive migration" that saves significant development time.

• **Adoption and Implementation**

- MCP has seen **"wildfire"** adoption across the industry936, with companies like **Google and OpenAI adopting it**. The "whole open source community adopted it", leading to a "massive migration".

- The recommended implementation for creating MCP tools and servers is to use the **latest V2 version of fastmcp**. Installing it is as simple as `uv add fast MCP42`.

- Creating a tool function in Python with `fastmcp` involves a simple annotation, such as `mcpto.tool.

• **Distributed Compute Framework Vision**

- MCP supports the vision of a **"distributed compute framework"** or a "graph of tools", similar to a fabric of microservices.

- An MCP server can act as a proxy, calling other MCP servers or tools. This allows for complex architectures where **one agent might even treat another agent as a tool**, further enabling distributed computation.

• **Current State of Integration and Challenges**

- While Crew AI had "very poor support for MCP" or "almost zero integration" in the past, the overall trend is towards agentic frameworks becoming MCP compliant.

- One challenge is handling multiple tools with the same functionality. While the agent can be explicitly told which tool to prefer, MCP itself is "silent on that front". Users sometimes use a proxy MCP server to expose only one tool for each job to their agent.

- API keys and configurations for tools are typically "baked into the tool" or managed via a config file, rather than being passed by the agent itself.


# Key Takeaways

- **MCP (Model Context Protocol)** standardizes how agents use tools, prompts, and resources.
- **Tools** act as actuators, enabling agents to perform actions like API calls.
- **FastMCP** allows easy tool creation with simple Python decorators.
- **Agents** can use other agents as tools, enabling composable, nested reasoning.
- **MCP** removes the need for custom client code, streamlining integration and discovery.
