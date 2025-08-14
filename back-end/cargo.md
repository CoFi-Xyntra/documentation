---
description: Account Management
icon: tally-1
---

# Cargo

### `Cargo.toml`&#x20;

This file defines the metadata, compilation settings, and dependencies for the Rust backend canister.

***

#### **\[package]**

```toml
[package]
name = "backend"
version = "0.1.0"
edition = "2021"
```

* **`name`** — The name of the package, in this case `"backend"`.
* **`version`** — Current version of the package (`0.1.0`).
* **`edition`** — Rust edition being used (`2021`), which determines language features and compiler behavior.

***

#### **Library Configuration**

```toml
[lib]
crate-type = ["cdylib"]
path = "lib.rs"
```

* **`crate-type = ["cdylib"]`** — Compiles the crate as a C-compatible dynamic library, required for Internet Computer (IC) canisters.
* **`path`** — Specifies the entry point file for the library (`lib.rs`).

***

#### **Dependencies**

```toml
[dependencies]
candid = "0.10.13"
ic-cdk = "0.17.1"
ic-llm = "1.1.0"
```

* **`candid`** — Library for encoding and decoding Candid, the interface description language for the IC.
* **`ic-cdk`** — The Internet Computer Canister Development Kit, providing APIs to build canisters in Rust.
* **`ic-llm`** — A library for integrating large language model (LLM) functionalities within IC canisters.



