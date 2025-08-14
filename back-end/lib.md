---
description: Main Backend Canister Logic
icon: tally-4
---

# lib

### `lib.rs`&#x20;

This file defines the main entry points for the backend canister, including AI prompt/chat handling and simple account management.

***

#### **Imports**

```rust
use ic_cdk::update;
use ic_llm::{ChatMessage, Model};
mod account;
use ic_cdk::query;
```

* **`ic_cdk::update`** — Macro to mark a function as an update method (modifies state and requires consensus).
* **`ic_llm::{ChatMessage, Model}`** — Types from the `ic-llm` library for handling LLM interactions.
* **`mod account;`** — Imports the `account` module from `account.rs`.
* **`ic_cdk::query`** — Macro to mark a function as a query method (read-only, no state changes).

***

#### **Prompt Function**

```rust
#[update]
async fn prompt(prompt_str: String) -> String {
    ic_llm::prompt(Model::Llama3_1_8B, prompt_str).await
}
```

* **Purpose:** Sends a single prompt to the Llama 3.1 8B model and returns its response.
* **Input:** `prompt_str` — the prompt text.
* **Output:** AI-generated text as a `String`.
* **Type:** **Update** (asynchronous, since it interacts with an external model).

***

#### **Chat Function**

```rust
#[update]
async fn chat(messages: Vec<ChatMessage>) -> String {
    let response = ic_llm::chat(Model::Llama3_1_8B)
        .with_messages(messages)
        .send()
        .await;
    
    response.message.content.unwrap_or_default()
}
```

* **Purpose:** Sends a sequence of chat messages to the Llama 3.1 8B model, receiving a contextual response.
* **Input:** `messages` — a vector of `ChatMessage` objects representing conversation history.
* **Output:** Assistant’s reply as a `String`.
* **Logic:**
  1. Create a chat session with the chosen LLM model.
  2. Attach the provided conversation history.
  3. Send the request asynchronously.
  4. Return the assistant’s text content, or an empty string if no content is provided.

***

#### **Create Account Function**

```rust
#[ic_cdk::update]
fn create_account(address: String) -> String {
    account::create_account(address)
}
```

* **Purpose:** Adds a new account address to the backend state.
* **Input:** `address` — account identifier as a string.
* **Output:** Status message (`"Account created"` or `"Already exists"`).
* **Logic:** Delegates the creation logic to `account.rs`.

***

#### **Get Accounts Function**

```rust
#[query]
fn get_accounts() -> Vec<String> {
    account::get_accounts()
}
```

* **Purpose:** Retrieves the list of all stored account addresses.
* **Output:** Vector of strings representing account addresses.
* **Type:** **Query** (read-only, no state changes).
* **Logic:** Delegates retrieval to `account.rs`.

***

#### **Export Candid Interface**

```rust
// Export the interface for the smart contract.
ic_cdk::export_candid!();
```

* Generates and exports the `.did` Candid interface file automatically from the Rust code.
* Ensures the service definition matches the actual implemented methods.

***

If you want, I can now **merge the documentation for `lib.rs`, `account.rs`, and `backend.did`** into a single **backend developer guide** so the whole system is explained end-to-end — perfect for onboarding new developers. That way, your project will be fully self-documented.
