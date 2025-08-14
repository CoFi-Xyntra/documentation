---
description: 'To compile and run the program, use:'
icon: door-open
---

# Getting Started

## Getting Started — React + ICP (Rust) Project

This project combines a **React frontend** with a **Rust-based Internet Computer (ICP) backend** using the **DFX SDK**.\
Below are the steps to set up, build, and run the project locally.

***

### 1️⃣ Prerequisites

Make sure you have the following installed:

* **Node.js** (v16+ recommended) or **Yarn**
* **Rust** and **Cargo**
* **DFX SDK** (Internet Computer SDK)
* **Git**
* **Ollama** (for AI integration, if applicable)

***

### 2️⃣ Installation & Setup

#### 2.1 Clone the repository

```bash
git clone https://github.com/CoFi-Xyntra/copilot-finance.git
cd copilot-finance
```

***

#### 2.2 Install DFX

If you don’t have **DFX** installed yet:

```bash
sh -ci "$(curl -fsSL https://sdk.dfinity.org/install.sh)"
```

Verify the installation:

```bash
dfx --version
```

***

#### 2.3 Install Rust & Cargo

If you don’t have **Rust** installed:

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Load Rust environment variables:

```bash
source ~/.cargo/env
```

Add the WebAssembly target:

```bash
rustup target add wasm32-unknown-unknown
```

Check Cargo version:

```bash
cargo --version
```

***

### 3️⃣ Project Structure Overview

After cloning, check the project structure:

```bash
ls -la
```

Make sure the following files/folders exist:

* **`dfx.json`** → DFX configuration file
* **`package.json`** → Frontend dependencies
* **`src/`** → Rust backend code
* **`frontend/`** or similar → React frontend source code

***

### 4️⃣ Install Dependencies

#### 4.1 Rust dependencies (optional, if required by backend)

```bash
rustup target add wasm32-unknown-unknown
```

#### 4.2 Frontend dependencies

Using npm:

```bash
npm install
```

Or using yarn:

```bash
yarn install
```

***

### 5️⃣ Running the Project

#### 5.1 Start the local Internet Computer replica

```bash
dfx start --background
```

#### 5.2 Deploy backend canisters

```bash
dfx deploy
```

(Optional for testing playground mode):

```bash
dfx deploy --playground
```

#### 5.3 Start the frontend development server

```bash
npm start
```

Or:

```bash
npm run dev
```

(depending on your `package.json` setup)

***

### 6️⃣ Additional Commands

Stop the local DFX replica:

```bash
dfx stop
```

Manually create canisters:

```bash
dfx canister create backend
dfx canister create frontend
```

Build the project:

```bash
dfx build
```

***

### 7️⃣ Installing Candid Extractor

The **Candid Extractor** tool can be useful for extracting Candid interface definitions from Rust canisters:

```bash
cargo install candid-extractor
```

***

### 8️⃣ Multi-Terminal Workflow (Recommended for Development)

**Terminal 1** — Build & Start replica:

```bash
dfx build
dfx start
```

**Terminal 2** — Deploy canisters:

```bash
dfx deploy
```

Or for playground:

```bash
dfx deploy --playground
```

**Terminal 3** — Start frontend:

```bash
npm start
```

***

### 9️⃣ Ollama + DeepSeek Integration

This project also integrates **Ollama** with **DeepSeek** for AI-powered features.

#### 9.1 Install Ollama

Follow installation instructions from [https://ollama.ai](https://ollama.ai/).

#### 9.2 Pull the DeepSeek model

```bash
ollama pull deepseek
```

#### 9.3 Running DeepSeek locally

```bash
ollama run deepseek
```



