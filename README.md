# LangGraph
This repo is for knowing the fundamentals of langgraph

**Langchain Ecosystem**
![alt text](<Screen shots/mod 0/Screenshot 2025-01-05 230710-1.png>)

**LangGraph** is a library for building *stateful*, *multi-actor* applications with LLMs, used to *create agent and multi-agent workflows*. Compared to other LLM frameworks, it offers these core benefits: *cycles*, *controllability* and *persistence*. LangGraph allows you to define flows that involve cycles, essential for most agentic architectures differentiating it from the DAG based solutions.

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
### Core Concepts (Introduce Langgraph and build few generalist agent architecture)
1. Simple Graph
2. LangGraph Studio
3. Chain
4. Router
5. Agent
6. Agent with Memory
7. Intro to Deployment

### State & Memory (work with messages to exchange info with the agent, use of memory to save agents internal state)
1. State Schema
2. State Reducers
3. Multiple Schemas
4. Trim and Filter Messages
5. Chatbot with Summarizing Messages and Memory
6. Chatbot with Summarizing Messages and External Memory

### UX and Human_in_the_loop(to approve specific actions or review your agent's work)
1. Streaming
2. Breakpoints
3. Editing State and Human Feedback
4. Dynamic Breakpoints
5. Time Travel

### Building Your Assistant (to reproduce customizable knowledge outputs like reports or wikis or summaries)
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

https://github.com/langchain-ai/langchain-academy this can be useful


Notes:
1. One type of LLM Application that we can build is Agent. We can create Agents by allowing LLMs to determine the control flow of an application.
2. They can automate wide range of tasks that previously were impossible.
3. There are different scenarios based on which the development in Langgraph are happening. We might need an agent to always call specific tool first or to use different prompts based on its state. Langgraph is a framwork for building multi agent and agentic applications. Langgraph provide better precision and control into agentic workflows , thus making them suitable for complexity of real world systems.
4. Use python 3.11, this version is required for best compatibility with LangGraph
5. Set the LANGCHAIN_API_KEY and set LANGCHAIN_TRACING_V2=true
6. Set Openai api key and tavily api key
7. LangGraph Studio is only compatible with MacOS. 

# ---------------------------------------------------
Module 1:
How Agent work?
Several generic agent architectures
Common challenges faced by developers when building agents
Why building custom agents with domain specific workflows and why focus on high reliability is important

Langgraph models agent workflows as graphs
Langgraph core abstraction - state, nodes, edges + 
core component - tools, messages, memory
building graphs around the chat models 
ReAct agent architecture

Langgraph studio as desktop IDE - for building and debugging agentic applications

### Do I need to use LangChain to use LangGraph? What’s the difference? - No
LangGraph is an orchestration framework for complex agentic systems and is more low-level and controllable than LangChain agents.
LangChain provides a standard interface to interact with models and other components, useful for straight-forward chains and retrieval flows.

"low-level" means that LangGraph gives you more direct control over the individual components and steps involved in building an AI agent. It's like having the building blocks to assemble your own custom agent rather than using a pre-built one with limited customization options.

**LangChain Agents:** These are higher-level tools that provide a more streamlined and user-friendly way to create agents. They often come with pre-defined functionalities and structures, making them easier to use for common tasks. However, this can limit your flexibility if you need to create something very specific or complex.

**LangGraph:** This is a lower-level framework that gives you more granular control. You can define the individual steps, decision points, and interactions within your agent's workflow. This allows for greater customization and the ability to create more complex and unique agent behaviors.


### How is LangGraph different from other agent frameworks?
Other agentic frameworks can work for simple, generic tasks but fall short for complex tasks bespoke to a company’s needs. LangGraph provides a more expressive framework to handle companies’ unique tasks without restricting users to a single black-box cognitive architecture.

### Does LangGraph impact the performance of my app? - no overhead to the code
LangGraph will not add any overhead to your code and is specifically designed with streaming workflows in mind.

### Langgraph - free, open source

### How are LangGraph and LangGraph Cloud different?
LangGraph is a stateful, orchestration framework that brings added control to agent workflows. LangGraph Cloud is a service for deploying and scaling LangGraph applications, with a built-in Studio for prototyping, debugging, and sharing LangGraph applications. 

![image](<Screenshot 2025-01-05 230710-1.png>)

Many LLM App use control flow
START -> **STEP 1 -> LLM -> ..(WITH STEPS PRE/POST LLM CALL{tool calls, retrieval})..STEP N** -> END
                                               I
                                               V
                                             Chain

We can the LLM system that can pick their own control flow depending on the problem it faces

Chain -> fixed control flow set by developer. Example: A chain might be used to summarize a long document by first splitting it into chunks, then summarizing each chunk, and finally combining the summaries.
Agent -> LLM defined control flow. Example: An agent might be used to answer a complex question. It might decide to search the web, access a database, or use a calculator, depending on what's needed to answer the question.

Agent types -> Router (less control), Fully Autonomous(More control)
![image](<Screenshot 2025-01-05 232741-1.png>)

![image](<Screenshot 2025-01-05 233530-1.png>)

![image](<Screenshot 2025-01-05 233642-1.png>)

Langgraph helps to build agents that maintain reliability even when we increase the level of control that we give to the agent

**LangGraph** -> balances reliability with control

In many application we combine the developer intuition with LLM control. so that we can specify certain steps that we always wanted to be fixed.

![image](<Screenshot 2025-01-05 234147-1.png>)

How it works:

a. Step 1 completes its task: This could be anything, like retrieving information from a database or summarizing a document.
b. LLM analyzes the output: The LLM examines the results from Step 1 and determines the best course of action.
c. LLM decides what Step 2 should do: Based on its analysis, the LLM "tells" Step 2 what to do. This could involve choosing a different action altogether, modifying the original plan, or proceeding as initially intended.

In essence, the LLM acts as the brain of the agent, providing the intelligence and decision-making capabilities needed to transform a simple, linear chain into a dynamic and adaptive agent.


![image](<Screenshot 2025-01-05 234810-1.png>)

Nodes can be considered as steps in the application like tool call, retrieval step and edges are the connectivity between the nodes.

Pillars that help langgraph achieve maintaining reliability even when we increase the level of control that we give to the agent.  ->   persistence, streaming, human in the loop, controllability.  

![image](<Screenshot 2025-01-06 000112-1.png>)

![image](<Screenshot 2025-01-06 000421-1.png>)

**Simple Graph**
It has Normal Edge and Conditional Edge.
The state is a dictionary.
Node : Each node will overwrite the value of graph state with something new.
Edges: Connect the nodes. we give some condition to choose node 2 or 3

Nodes -> update the state
Conditional Edge -> which node to go to next.
Graph construction -> It consist of initializing the state graph (the blue print) then adding nodes and edges for knowing the next nodes to follow.

**Langgraph Studio**
1. We have requirements.txt file - has the pkgs
2. python scripts
3. .env file - stores the api keys

We can load the studio folder as a project in Langgraph studio.(from mac os only)
we need docker running


**Chain**
With nodes and edges, here we include the concept of chains like below within langgraph
a. Chat messages
b. Chat models
c. Binding Tools
d. Executing tool calls

Chat messages -> The chat models interact with the messages.
we can define a chat model, pass list of messages, get the ai messages back out with some content and meta data

**Tools**
It is another way of using chatmodel.
It is required in cases where we want to connect with external tools like api that requires particular payload to run.
We need to see how can we use messages as graph state
-> we define the MessageState class which is of type dictionary and has one key named messages which stores list of messages
![alt text](<Screenshot 2025-01-06 142531-1.png>)

![alt text](<bind tool-1.png>)

**Reducer** -> annotate + add_message
-> one challenge is from previous discussion that we over write the value of key "messages" from state update, Here we dont want that (overwriting), we want to append to that list every time the chat model produces the output so that full history of conversation is preserved. => This gives the idea of **reducers function.**

![alt text](<Screenshot 2025-01-06 135208-1.png>)

![alt text](<Screenshot 2025-01-06 141901-1.png>)

We have built in MessageState, which has builtin message key and add_messages reducer.

**Router**
Router return either a tool call or return a natural language response based on chatmodel response to the input.
conditional_edge tool condition is used for selecting the edge to follow.

**Agent**
A small change is required to change the router into generic agentic application. 
message -> invoke the model -> if it shows the tool -> return the message to the user

![alt text](<Screenshot 2025-01-06 151957-1.png>)

![alt text](<Screenshot 2025-01-06 155050-1.png>)

But what if we take the message and put it back to the model -> this is the ReAct architecture
Act (model call to tool) -> pass the tool output back to the model -> reason, model decides what to do next

The model will continue to call the tool in loop till it finds the solution where it can send natural language response.

Please note the langchain key and langsmith key are same


**LangSmith**
Gives the access to tracing and evaluation.

**Agent with Memory**
ReAct = Act + Observe + Reason

Check pointers used to save the graph state after each step which gives memory
MemorySaver - an in memory key-value store for Graph State.
Every step in our graph will write a checkpoint which contains the step of the graph at that point. And these checkpoints can be associated together to form a thread.

we have a new parameter named config that stores the thread in invoke which essentially store the checkpoint info that serves to thread when collected.

![alt text](<Screenshot 2025-01-06 183901-1.png>)

In Langgraph studio when we compile we dont need checkpointer because studio is backed by Langgraph api which has its own persistance layer (which is postgres behind the scene)

![alt text](<Screenshot 2025-01-06 185455-1.png>)


![alt text](<Screenshot 2025-01-06 190617-1.png>)

**Deployment**
Once I have everything ready in notebook how can i put it in production.
LangGraph - creation of agent
LangGraph API - API hosted via langgraph cloud, bundles the graph code.
Langgraph Cloud - allow github repo, monitoring, tracing, documentation, accessible via URL
LangGraph Studio - locally or cloud deployment
LangGraph SDK - Programmatically interact with langgraph graph


Testing Locally
![alt text](<the url is locally running api-1.png>)
Testing in Cloud 
    
![alt text](<Screenshot 2025-01-06 203951-1.png>)
![alt text](<Screenshot 2025-01-06 204020-1.png>)
![alt text](<Screenshot 2025-01-06 204100-1.png>)
![alt text](<Screenshot 2025-01-06 204134-1.png>)
![alt text](<Screenshot 2025-01-06 204219-1.png>)
![alt text](<Screenshot 2025-01-06 204327-1.png>)









