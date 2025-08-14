---
description: Architecture & Logic
icon: '2'
---

# Back-end

### Backend Overview&#x20;

The backend is designed as a lightweight, modular canister running on the Internet Computer.\
Its main purpose is to **combine AI-powered conversations** with **simple account management**, all wrapped in a clean and extendable architecture.

#### **Core Ideas**

* **AI Interaction Layer**\
  Powered by the `ic-llm` library, the backend can handle both **single prompts** and **multi-message chats** using the Llama 3.1 model. This makes it easy to build interactive, context-aware experiences without external AI servers.
* **Account Management Layer**\
  A simple but functional in-memory system keeps track of unique account addresses. This demonstrates how user-related data can be stored and retrieved efficiently on the IC.

#### **Architecture at a Glance**

1. **`lib.rs`** — The central entry point.\
   Defines the public methods the frontend can call, such as sending AI prompts, managing conversations, and handling account operations.
2. **`account.rs`** — A focused module for account creation and retrieval.\
   Uses a lightweight in-memory state to keep the logic clear and maintainable.
3. **`backend.did`** — The Candid interface.\
   Describes the data structures and public methods so the frontend and other canisters know exactly how to communicate with the backend.
4. **`Cargo.toml`** — The project manifest.\
   Lists dependencies (`ic-cdk`, `ic-llm`, `candid`) and sets up the backend to compile as a canister.

#### **How It Works in Practice**

* The frontend connects to the backend via Candid.
* When a user interacts:
  * **For AI**: The backend sends their prompt or conversation history to the LLM and returns the AI’s reply.
  * **For accounts**: The backend adds or retrieves addresses in its state.
* All responses are immediate, with no need for an external database in this version.

