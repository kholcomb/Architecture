---
name: Tool Use
category: ai/llm
also-known-as: [Function Calling, Tool Calling]
tags: [function-calling, tools, actions, integration, extensibility]
parent: llm
related: [agent, prompt-chaining, service-layer]
source: https://github.com/denyspoltorak/metapatterns/wiki/Tool-Use
---

## Diagram

```mermaid
graph TD
    P[Prompt + Tool Schemas] --> LLM[LLM]
    LLM -->|tool_call: search("query")| EX[Tool Executor]
    EX -->|result: [...documents]| LLM
    LLM --> R[Final Response]
```

## Summary

Provides the LLM with a set of typed function signatures it can invoke during generation. When the model determines that a tool call is needed, it outputs a structured tool call (name + arguments); the calling system executes the function and returns the result to the model, which continues generation. Tool use extends the model's capabilities beyond text — it can query databases, call APIs, execute code, and interact with external systems.

## When To Use

- The LLM must interact with systems outside its context window (databases, APIs, file systems)
- Responses must incorporate real-time or dynamic data the model was not trained on
- Actions must be taken as part of a response (create a record, send a notification, run a calculation)

## When To Avoid

- The tool's output is deterministic and could simply be included in the prompt up front
- Tool calls have irreversible side effects without a Human-in-the-Loop checkpoint
- The model consistently misuses or misunderstands the tool — prompt engineering or schema clarity is needed first

## Pros and Cons

* Good, because the model's capabilities are extended without retraining — any API can become a tool
* Good, because tool schemas provide a typed interface that constrains what the model can request
* Bad, because the model may call tools incorrectly or hallucinate arguments — tool inputs must be validated before execution
* Bad, because tool execution introduces latency, side effects, and failure modes that the calling system must handle

## Evolutions

- **From:** LLM generation with no external action capability
- **To:** Agent (combine multiple tool calls in a reasoning loop); add Sandboxing for tools that execute arbitrary code (e.g., a code interpreter)
