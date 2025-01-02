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




