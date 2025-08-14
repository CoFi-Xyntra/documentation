---
description: Account Management Module
icon: tally-2
---

# account

### `account.rs`&#x20;

This module provides a simple in-memory account management system using Rust, intended for use in a backend running on the Internet Computer (IC) or a similar environment.

***

#### **Imports and Type Definitions**

```rust
use std::collections::HashSet;
type Address = String;
```

* **`HashSet`** is used to store account addresses without duplicates.
* **`Address`** is defined as a type alias for `String`, representing a user’s account address.

***

#### **State Structure**

```rust
#[derive(Default)]
struct State {
    accounts: HashSet<Address>,
}
```

* **`State`** holds the current set of accounts in memory.
* **`#[derive(Default)]`** automatically generates a default constructor for the `State` struct, initializing `accounts` as an empty set.

***

#### **Thread-local State**

```rust
thread_local! {
    static STATE: std::cell::RefCell<State> = std::cell::RefCell::new(State::default());
}
```

* **`thread_local!`** ensures that each thread has its own copy of the state, which is required for safe mutable access in a concurrent environment.
* **`RefCell`** allows interior mutability, meaning the `State` can be modified even when it is behind an immutable reference.

***

#### **Create Account Function**

```rust
pub fn create_account(address: String) -> String {
    STATE.with(|s| {
        let mut state = s.borrow_mut();
        if state.accounts.contains(&address) {
            return "Already exists".into();
        } else {
            state.accounts.insert(address);
            return "Account created".into();
        }
    })
}
```

* **Purpose:** Adds a new account address if it doesn’t already exist.
* **Logic:**
  1. Borrow the state mutably.
  2. Check if the given address is already in the set.
  3. If it exists, return `"Already exists"`.
  4. If not, insert it into the set and return `"Account created"`.
* This function could be exposed as an **update method** in an IC canister (the `#[ic_cdk::update]` attribute is currently commented out).

***

#### **Get Accounts Function**

```rust
pub fn get_accounts() -> Vec<String> {
    STATE.with(|s| {
        s.borrow().accounts.iter().cloned().collect()
    })
}
```

* **Purpose:** Returns a list of all registered account addresses.
* **Logic:**
  1. Borrow the state immutably.
  2. Convert the `HashSet` of addresses into a `Vec<String>`.
  3. Return the vector to the caller.

***

####
