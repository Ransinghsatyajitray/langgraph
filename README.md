# LangGraph
This repo is for knowing the fundamentals of langgraph

**Langchain Ecosystem**
![alt text](<Screen shots/mod 0/Screenshot 2025-01-05 230710-1.png>)

**LangGraph** is a library for building *stateful*, *multi-actor* applications with LLMs, used to *create agent and multi-agent workflows*. Compared to other LLM frameworks, it offers these core benefits: *cycles*, *controllability* and *persistence*. LangGraph allows you to define flows that involve cycles, essential for most agentic architectures differentiating it from the DAG based solutions.

![alt text](<Screen shots/LangGraph properties.png>)

Graph DB -> Nodes, relation between nodes (Edge)
            Graph Knowledge -> google search => RAG

![alt text](<Screen shots/NormalEdge_ConditionalEdge.png>)

Why LangGraph ?
1. **It simplifies the development** - development involves -> state management and agent coordination

                Agent 1: google search
Chatbot         Agent 2: wiki search
                Agent 3: vector search

We need to define workflow, logics

2. **Flexibility** : developers have the flexibility to define their own agent logic and communication protocols.This allows for highly customized applications tailored to specific use cases. Whether you need a chatbot that can handle various types of user requests or a multi-agent system that performs complex tasks, LangGraph provides that tools to build exactly what you need. It's all about giving you the power to create.


3. **Scalability** : Large scale multi agent application (it can handle high volume of interaction and complex workflows), there is an enterprise version and langchain are coming up with their own cloud.

4. **Fault Tolerance** : handle errors, fault tolerance mechanism (reliability)

![alt text](<Screen shots/Fault Tolerance.png>)

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
10. After creating the node , we compile the graph_builder
11. we can use IPython.display to show the mages.
12. create feasibility for user to enter the messages.

**Accessing LangSmith Key (This is same as Langchain key)**

![alt text](<Screen shots/for langgraph file/langsmith/Screenshot 2024-12-31 174049.png>)

![alt text](<Screen shots/for langgraph file/langsmith/Screenshot 2024-12-31 182803.png>)

![alt text](<Screen shots/for langgraph file/langsmith/Screenshot 2024-12-31 183008.png>)

--------------------------------------------------------------------------------------------------
### Core Concepts (Introduce Langgraph and build few generalist agent architecture)
1. Simple Graph
2. LangGraph Studio
3. Chain
4. Router
5. Agent
6. Agent with Memory
7. Intro to Deployment

![alt text](<Screen shots/MOD1_Router_and_tool_calling_agent.png>)

### State & Memory (work with messages to exchange info with the agent, use of memory to save agents internal state)
1. State Schema
2. State Reducers
3. Multiple Schemas
4. Trim and Filter Messages
5. Chatbot with Summarizing Messages and Memory
6. Chatbot with Summarizing Messages and External Memory

![alt text](<Screen shots/MOD2_Memory_LongRunningChat.png>)

### UX and Human_in_the_loop(to approve specific actions or review your agent's work)
1. Streaming
2. Breakpoints
3. Editing State and Human Feedback
4. Dynamic Breakpoints
5. Time Travel

![alt text](<Screen shots/MOD3_Streaming_Human_in_loop.png>)

### Building Your Assistant (to reproduce customizable knowledge outputs like reports or wikis or summaries)
1. Parallelization
2. Sub graphs
3. Map-reduce
4. Research Assistant

![alt text](<Screen shots/MOD4_Human_in_loop_parallelization_customization.png>)

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

![alt text](<Screen shots/chain_vs_agent.png>)

Chain -> fixed control flow set by developer. Example: A chain might be used to summarize a long document by first splitting it into chunks, then summarizing each chunk, and finally combining the summaries.
Agent -> LLM defined control flow. Example: An agent might be used to answer a complex question. It might decide to search the web, access a database, or use a calculator, depending on what's needed to answer the question.


Agent types -> Router (less control), Fully Autonomous(More control)
![alt text](<Screen shots/RouterAgent_vs_FullyAutonomousAgent.png>)

![alt text](<Screen shots/Agents-RouterVsFA.png>)

Langgraph helps to build agents that maintain reliability even when we increase the level of control that we give to the agent

**LangGraph** -> balances reliability with control

In many application we combine the developer intuition with LLM control. so that we can specify certain steps that we always wanted to be fixed.

![alt text](<Screen shots/Agent_is_control_flow_defined_by_LLM.png>)

How it works:

a. Step 1 completes its task: This could be anything, like retrieving information from a database or summarizing a document.
b. LLM analyzes the output: The LLM examines the results from Step 1 and determines the best course of action.
c. LLM decides what Step 2 should do: Based on its analysis, the LLM "tells" Step 2 what to do. This could involve choosing a different action altogether, modifying the original plan, or proceeding as initially intended.

In essence, the LLM acts as the brain of the agent, providing the intelligence and decision-making capabilities needed to transform a simple, linear chain into a dynamic and adaptive agent.

![alt text](<Screen shots/Agent-llm_between_steps.png>)

![alt text](<Screen shots/Agent-llm_between_steps_equals_Edge_between_nodes.png>)

Nodes can be considered as steps in the application like tool call, retrieval step and edges are the connectivity between the nodes.

Pillars that help langgraph achieve maintaining reliability even when we increase the level of control that we give to the agent.  ->   persistence, streaming, human in the loop, controllability.  

![alt text](<Screen shots/reliability_control_curve_persistance_streaming_humaninloop_controlibility.png>)

**Simple Graph**
It has Normal Edge and Conditional Edge.
The state is a dictionary.
Node : Each node will overwrite the value of graph state with something new.
Edges: Connect the nodes. we give some condition to choose node 2 or 3

Nodes -> update the state
Conditional Edge -> which node to go to next.
Graph construction -> It consist of initializing the state graph (the blue print) then adding nodes and edges for knowing the next nodes to follow.

**Agent initial functions for nodes and edges stage**
![alt text](<Screen shots/Agent_Node_Edge_Blueprint.png>)

**Agent Blueprint stage**
![alt text](<Screen shots/SimpleGraphBluePrint.png>)

**Agent invoking stage**
![alt text](<Screen shots/Compile and Invoke.png>)

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

![alt text](<Screen shots/Human_AI_System_Tool_Message.png>)


**Tools**
It is another way of using chatmodel.
It is required in cases where we want to connect with external tools like api that requires particular payload to run.
We need to see how can we use messages as graph state
-> we define the MessageState class which is of type dictionary and has one key named messages which stores list of messages
![alt text](<Screen shots/Tool_flowchart_concept.png>)


![alt text](<Screen shots/bind tool.png>)

**Reducer** -> annotate + add_message
-> one challenge is from previous discussion that we over write the value of key "messages" from state update, Here we dont want that (overwriting), we want to append to that list every time the chat model produces the output so that full history of conversation is preserved. => This gives the idea of **reducers function.**


![alt text](<Screen shots/Why_reducer_is_necessary.png>)

We have built in MessageState, which has builtin message key and add_messages reducer.

**Router**
Router return either a tool call or return a natural language response based on chatmodel response to the input.
conditional_edge tool condition is used for selecting the edge to follow.

![alt text](<Screen shots/router with tool call and without tool call_01.png>)

**Agent**
A small change is required to change the router into generic agentic application. 
message -> invoke the model -> if it shows the tool -> return the message to the user


But what if we take the message and put it back to the model -> this is the ReAct architecture
Act (model call to tool) -> pass the tool output back to the model -> reason, model decides what to do next

![alt text](<Screen shots/Agent-llm_between_steps.png>)

The model will continue to call the tool in loop till it finds the solution where it can send natural language response.

**Please note the langchain key and langsmith key are same**


**LangSmith**
Gives the access to tracing and evaluation.

![alt text](<Screen shots/for langgraph file/langsmith/Langchain_project_tracing.png>)

![alt text](<Screen shots/for langgraph file/langsmith/Screenshot 2025-01-02 171025.png>)

**Agent with Memory**
ReAct = Act + Observe + Reason

Check pointers used to save the graph state after each step which gives memory
MemorySaver - an in memory key-value store for Graph State.
Every step in our graph will write a checkpoint which contains the step of the graph at that point. And these checkpoints can be associated together to form a thread.

we have a new parameter named config that stores the thread in invoke which essentially store the checkpoint info that serves to thread when collected.

![alt text](<Screen shots/Checkpoint_trace_flowchart.png>)

![alt text](<Screen shots/Checkpoint_trace_flowchart_simple.png>)

**checkpoint with trace**
![alt text](<Screen shots/Checkpoint_trace_agent_with_memory.png>)
It can recognise "that" from previous execution

In Langgraph studio when we compile we dont need checkpointer because studio is backed by Langgraph api which has its own persistance layer (which is postgres behind the scene)


**Deployment**
Once I have everything ready in notebook how can i put it in production.
LangGraph - creation of agent
LangGraph API - API hosted via langgraph cloud, bundles the graph code.
Langgraph Cloud - allow github repo, monitoring, tracing, documentation, accessible via URL
LangGraph Studio - locally or cloud deployment
LangGraph SDK - Programmatically interact with langgraph graph


Testing Locally

Testing in Cloud 
![alt text](<Screen shots/LangGraph_Cloud01.png>)

![alt text](<Screen shots/LangGraph_Cloud02.png>)

![alt text](<Screen shots/LangGraph_Cloud03.png>)

![alt text](<Screen shots/LangGraph_Cloud04.png>)

![alt text](<Screen shots/LangGraph_Cloud05.png>)

![alt text](<Screen shots/LangGraph_Cloud06_URL.png>)

![alt text](<Screen shots/LangGraph_Cloud07.png>)


## Module 2
End users expect the agentic application to remember previous interactions
eg. chatbots

LangGraph give you control on memory in applications
We will see how the persistence is added to graph.
**How we can manage the high token usage in case of memory/persistence -> filtering , trimming, summarization**
DIAGRAM

**databases used in memory**
internal - key, value
external - postgres and sqlite
DIAGRAM

**State**
agent with memory = act + observe + reason + persist state
DIAGRAM


**Schema**
Defines the structure and type of data that our graph will use. 

#### TypedDict
We often use TypedDict which is recommended (dictionary where type of variables)
![alt text](<Screen shots/schema typeddict.png>)


![alt text](<Screen shots/schema typeddict01.png>)

We feed the TypedDict class to the StateGraph
DIAGRAM


NODE + EDGE + A(STATE_OBJECT -> StateGraph) + add node to A + build logic for connecting nodes (edges) {add_edge or add_conditional_edge(based on some function)}
DIAGRAM

#### DataClassState
![alt text](<Screen shots/schemaDataClassState.png>)

![alt text](<Screen shots/node defn and invoking with TypeDict_typing vs DataClassState_dataclass.png>)

#### Pydantic
This does the data check which type dict and data class state were not doing
![alt text](<Screen shots/typedict vs dataclassstate vs pydantic.png>)



**State Reducers**

They specify how state update are done on specific keys.
by default when we do any update, we overwrite the values of the state key, we cant update the same shared state key as it become ambiguous as to which state to keep. we get invalid update error there

![alt text](<Screen shots/Without using reducer(annotated + add).png>)

![alt text](<Screen shots/using the reduced using add and annotated.png>)


the add just append value to the list.

There might be cases where the type of the value entered to the invoke might be different (like none type). This motivated the use of Custom Reducers.

**Custom Reducers**

![alt text](<Screen shots/Motivation for using custom reducer.png>)
There might be scenarios where the entries to invoke are of different type for those scenarios we use custom reducers.

**Messages**
MessagesState is a shortcut to work on messages (AI + Human + System + Tools) specifically during chat type interactions.

**MessagesState**

**CustomMessagesState**

**ExtendedMessagesState**

![alt text](<Screen shots/CustomMessagesState and motivation for using ExtendedMessageState.png>)

The CustomMessagesState and ExtendedMessagesState are same but its easier to use ExtendedMessagesState.

**add_messages reducer**

![alt text](<Screen shots/add_messages as a reducer.png>)

**overwriting the value with appending with id argument**

![alt text](<Screen shots/overwriting the value while appending in a reducer when using id arg in (AI, Human)Messages.png>)

**Removing messages**

![alt text](<Screen shots/removing messages (here we are removing the 2 recent most messages.png>)

after this if we use add_messages(messages, delete_messages) we can see the messages removed by the reducer

#### Multiple Schema
Typically graph nodes communicate with single schema meaning single input and output.

There might be scenarios where there would be interactions within modes whose output wont necessarily be available to end user

**PrivateState**

![alt text](<Screen shots/PrivateState.png>)

![alt text](<Screen shots/PrivateState01.png>)

**Input/Output Schema**
This specifically define what we want in input and what we want in output. These are basically filter on overall state.

![alt text](<Screen shots/Using inputstate and outputstate as filter to stategraph.png>)

**Trim and Filter Messages**
Handling messages with chatbots is difficult in some cases.
for filtering in RemoveMessage we remove all the messages except some recent ones

**filtering=MessagesState + RemoveMessage**

![alt text](<Screen shots/removing older messages and keeping recent onces Filtering.png>)

**trimming**
we can trim the messages based on specific number of tokens
![alt text](<Screen shots/trimming.png>)

we use trim_messages , we have parameter like strategy and allow_partial

**ChatBot with summarizing Messages and External Memory**
We use LLM to produce running summary of the conversation
![alt text](<Screen shots/summary in MessageState.png>)

Define the node called call model -> It get the summary if it is present it add to the messages if not then grab what is there in the messages then invoke the model
![alt text](<Screen shots/summary.png>)

We also create summarize conversation node, if there is summary then it is added to the new summary prompt. we nuse the remove messages trick to keep only the latest ones.
![alt text](<Screen shots/summarize messages node.png>)

We add a conditional edge that will help us to know whether to summarize or continue.


We know the state is transient and limited to single graph execution => multi turn conversation difficult => we use checkpointer
![alt text](<Screen shots/compiling the graph with check pointer.png>)

![alt text](<Screen shots/summarize graph.png>)

![alt text](<Screen shots/Summary + memory.png>)

**Chatbot with summarizing messages and external memory**
For the above examples the persistence(due to in memory checkpointer) is valid till the notebook is in existence.
The overall token usage is reduced when we do summarization of chat messages => feasibility for long running conversations.

sqlite and postgres - external storage

sqlite - small , light and very small db, good starting point for external db checkpointers

![alt text](<Screen shots/In memory to external -sqlite.png>)

Langgraph has its own builtin persistence layer.
The persistence layer in case of the Langgraph is postgres

## Module 3 : UX and Human in the loop
How to combine agent with Human = Human in the loop
In many cases we need human approval before agent take an action.

**Streaming**
In LangGraph there are 2 methods for streaming - stream and astream (sync and async)

![alt text](<Screen shots/Accumulated full state is populated.png>)

steaming modes -> updates and values

![alt text](<Screen shots/streaming with updates and values.png>)

**Streaming tokens**
astream_events methods the events that comes out is a dictionary with few different keys(event, name, data and metadata)

Streaming allow us to emit graph state in each step.

**Breakpoints**
Human in loop
approve certain steps - some tools are sensitive so we have to allow it first for agent to execute those kind of action.

Approval
Debugging -to reproduce prior issues and to know future onces
Editing - modify state with human in the loop

we use interrupt_before and interrupt_before to make use of it. 

![alt text](<Screen shots/concept checkpoint thread snapshot.png>)

When we run the stream and pass None then we remit the current state and then execute the next nodes.
We can stop the graph at any node we can then continue by passing None with thread id to pick back up from the current state of the graph.

We can also pass the interrupt before in the client api(we get from langgraph ide) runs and not only using the code.

![alt text](<Screen shots/Approval step in the ide.png>)

**Editing State and Human**
Edit the graph state once it is stopped.
The break points also give the opportunities to modify the graph state once it is stopped.
update_state

![alt text](<Screen shots/Human in loop.png>)

![alt text](<Screen shots/Human in loop01.png>)

![alt text](<Screen shots/Human in Loop03.png>)


In Studio I can add manually add interrupts in the graph.

![alt text](<Screen shots/Manually adding interrupt in Studio.png>)

**Awaiting user input**
We can put break point, edit the graph state at a given break point.
Here we will see how to explicitly get user input to modify the state. => we can do this by providing a dummy node, which is basically a no operation node that will accept user feedback and inject it into a graph at a particular point.

*Dummy node in human feedback*
![alt text](<Screen shots/dummy node as human feedback node.png>)

**Dynamic Breakpoint**
Graph to interrupt itself. eg . stay on the graph if you meet certain condition.
NodeInterrupt

![alt text](<Screen shots/NodeInterrupt.png>)


**Time Travel**
LangGraph feature to support debugging by viewing, replaying and even forking from past states.-> this is callectively called time travel

browsing history -> get_state -> this give info on current state for a particular thread.

history of every state -> get_state_history (1st state is the current state, the last one would be the START node)

![alt text](<Screen shots/Get state history.png>)

**Replay**
We can replay our agent from any of the prior steps.
![alt text](<Screen shots/replaying.png>)

If we pass checkpoint id with thread id, in that case the graph will start from a particular check point.(using this we can rewind/replay(model knows it has executed in the past) from any checkpoint within the thread)
If we pass just the thread id, it will just pass the current state.

Its fast as we are just replaying and not rexecute from the human input.

**Forking**















