---
description: Candid Interface Definition
icon: tally-3
---

# backend



### `backend.did`

This file defines the Candid interface for the backend canister.\
It specifies **data types** and **service methods** so that clients (frontend or other canisters) can interact with the backend.

***

#### **Type Definitions**

**AssistantMessage**

```did
type AssistantMessage = record {
  content : opt text;
  tool_calls : vec ToolCall;
};
```

* Represents a message from the assistant (e.g., an AI system).
* **`content`** — Optional text content of the message.
* **`tool_calls`** — A list of tools/functions the assistant is requesting to call.

***

**ChatMessage**

```did
type ChatMessage = variant {
  tool : record { content : text; tool_call_id : text };
  user : record { content : text };
  assistant : AssistantMessage;
  system : record { content : text };
};
```

* Represents a message in a conversation.
* **`tool`** — A tool response containing `content` and the `tool_call_id` that triggered it.
* **`user`** — A message sent by the user.
* **`assistant`** — A message from the assistant, including optional content and tool calls.
* **`system`** — A message from the system, usually containing instructions or context.

***

**FunctionCall**

```did
type FunctionCall = record {
  name : text;
  arguments : vec ToolCallArgument;
};
```

* Represents a call to a specific function.
* **`name`** — Name of the function to execute.
* **`arguments`** — List of named arguments passed to the function.

***

**ToolCall**

```did
type ToolCall = record {
  id : text;
  function : FunctionCall;
};
```

* Represents a request to execute a tool or function.
* **`id`** — Unique identifier for this tool call.
* **`function`** — Details of the function to be executed.

***

**ToolCallArgument**

```did
type ToolCallArgument = record {
  value : text;
  name : text;
};
```

* Represents a single argument for a tool call.
* **`name`** — Name of the argument.
* **`value`** — Value of the argument.

***

#### **Service Definition**

```did
service : {
  chat : (vec ChatMessage) -> (text);
  create_account : (text) -> (text);
  get_accounts : () -> (vec text) query;
  prompt : (text) -> (text);
}
```

**Methods**

1. **`chat`**
   * **Input:** A list of `ChatMessage` objects representing the conversation history.
   * **Output:** A `text` response from the assistant.
   * **Purpose:** Handles conversational interactions between the user and the assistant.
2. **`create_account`**
   * **Input:** `text` (account address).
   * **Output:** `text` status message (`"Account created"` or `"Already exists"`).
   * **Purpose:** Adds a new account address to the backend’s account list.
3. **`get_accounts`** (**query method**)
   * **Input:** None.
   * **Output:** A vector of `text` values, each representing an account address.
   * **Purpose:** Retrieves all registered accounts without modifying state.
4. **`prompt`**
   * **Input:** `text` prompt.
   * **Output:** `text` response.
   * **Purpose:** Sends a single prompt to the assistant and returns its reply, without passing a full chat history.

