# LangGraph
The repo is for knowing the fundamentals of langgraph

LangGraph is a library for building stateful, multi-actor applications with LLMs, used to create agent and multi-agent workflows. Compared to other LLM frameworks, it offers these core benefits: cycles, controllability and persistence. LangGraph allows you to define flows that involve cycles, essential for most agentic architectures differentiating it from the DAG based solutions.

Graph DB -> Nodes, relation between nodes
            Graph Knowledge -> google search => RAG

Why LangGraph ?
1. **It simplifies the development** - development incolves -> state management and agent coordination

                Agent 1: google search
Chatbot         Agent 2: wiki search
                Agent 3: vector search

We need to define workflow, logics

2. **Flexibility** : develops have the flexibility to define their own agent logic and communication protocols.This allows for highly customized applications tailored to specific use cases. Whether you need a chatbot that can handle various types of user requests or a multi-agent system that performs complex tasks, LangGraph provides that tools to build exactly what you need. It's all about giving you the power to create.


3. **Scalability** : Large scale multi agent application (it can handle high volume of interaction and complex workflows), there is an enterprise version and langchain are coming up with their own cloud.

4. **Fault Tolerance** : handle errors, fault tolerance mechanism (reliability)


START NODE -> CHATBOT (LLM) {defination} -> END

Langgraph also create everything in the form of graph where we have nodes

Langsmith is used to track the interaction with the llm

Create an API key
To log traces and run evaluations with LangSmith, you will need to create an API key to authenticate your requests. Currently, an API key is scoped to a workspace, so you will need to create an API key for each workspace you want to use.

To create either type of API key head to the Settings page, then scroll to the API Keys section. Then click Create API Key.

https://smith.langchain.com/o/218834cf-5e1a-50ea-8422-eff98cabb30e/settings


langgraph - 
a. provide controllable cognitive architecture for any task.
b. It is designed for human agent collaboration
c. deploy agents at scale, monitor carefully iterate boldly

--------------CODE--------------

1. We would be needing GROQ api key, Langsmith api key (for tracking)
2. beside this we need to create environment for langchain_api_key (same as langsmith api key), langchain traching v2 which is true and langchain project name
3. we use chatgroq and any mode associated with groq
4. we start building chatbot using Langgraph
   a. from langgraph.graph import StateGraph which help in managing the state, START and END which indicate the start and END of the node, which actually shows the flow of the entire chatbot.
   The StateGraph keeps on changing based on some parameters. Thus we use from langgraph.graph.message import add_messages , it means when the state of the agent will keep on changing the messages. 
5. We create our own class for state management. The messages is of type annotated, it is of list type, the add_messages is responsible for adding the messages to the list and not overwrite them
6. we define the graph_builder.
7. Now we have to define the chatbot function which takes parameter as state (current message) and based on the messages/user queries the llm will get invoked
8. This chatbot need to be added to graph builder. graph_builder.add_node("chatbot",chatbot)
9. To get the flow we use graph_builder.add_edge(START,"chatbot") and graph_builder.add_edge("chatbot",END)
10. After creating the node , we ccompile the graph_builder
11. we can use IPython.display to show the mages.
12. create feasibility for user to enter the messages.

--------------------------------------------------------------------------------------------------
### Core Concepts 
1. Simple Graph
2. LangGraph Studio
3. Chain
4. Router
5. Agent
6. Agent with Memory
7. Intro to Deployment

### State & Memory
1. State Schema
2. State Reducers
3. Multiple Schemas
4. Trim and Filter Messages
5. Chatbot with Summarizing Messages and Memory
6. Chatbot with Summarizing Messages and External Memory

### UX and Human_in_the_loop
1. Streaming
2. Breakpoints
3. Editing State and Human Feedback
4. Dynamic Breakpoints
5. Time Travel

### Building Your Assistant
1. Parallelization
2. Sub graphs
3. Map-reduce
4. Research Assistant

### Long-Term-Memory
1. Short Vs Long Term Memory
2. LangGraph Store
3. Memory Schema + Profile
4. Memory Schema + Collection
5. Build an Agent with Long Term Memory

### Deployment
1. Deployment Concepts
2. Creating a Deployment
3. Connecting to a Deployment
4. Double Texting
5. Assistants