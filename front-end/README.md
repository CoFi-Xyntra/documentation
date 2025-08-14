---
icon: '1'
---

# Front-end

### File Structure

```typescript
// Import dependencies
import React, { useState, useRef, useEffect } from 'react';
import ReactDOM from 'react-dom/client';
import { backend } from 'declarations/backend';
import botImg from '/bot.svg';
import userImg from '/user.svg';
import Sidebar from './components/Sidebar';
import ChatWindow from './components/ChatWindow';
import '/index.css';
import { createThirdwebClient } from "thirdweb";
import { client } from "./../config/client";
import { useProfiles, useActiveAccount, ConnectButton, ThirdwebProvider } from "thirdweb/react";

// Wallet connection component
export function WalletConnectComponent() {
  const account = useActiveAccount();
  
  useEffect(() => {
    if (account) {
      const address = account.address;
      console.log("Wallet connected:", address);
      backend.create_account(address)
        .then(() => console.log("Account registered"))
        .catch(err => console.error("Failed to register:", err));
    }
  }, [account]);

  return <ConnectButton client={client} />;
}

// Main App component
function App() {
  return (
    <div className="flex h-screen dark bg-zinc-900 text-white">
      <ChatWindow />
      <div className="w-64 bg-zinc-800 p-4 flex flex-col">
        <WalletConnectComponent />
      </div>
    </div>
  );
}

// Root rendering
export default App;

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <ThirdwebProvider client={client}>
      <App />
    </ThirdwebProvider>
  </React.StrictMode>
);
```

### Core Components

#### 1. `WalletConnectComponent`

Handles cryptocurrency wallet connection and account registration.

```tsx
export function WalletConnectComponent() {
  const account = useActiveAccount();  // Gets active crypto wallet

  useEffect(() => {
    if (account) {
      const address = account.address;
      backend.create_account(address);  // Registers with backend
    }
  }, [account]);

  return <ConnectButton client={client} />;
}
```

| Element                    | Purpose                                                 |
| -------------------------- | ------------------------------------------------------- |
| `useActiveAccount()`       | Thirdweb hook for detecting connected wallets           |
| `useEffect()`              | Triggers when wallet connection state changes           |
| `backend.create_account()` | Creates user account on Internet Computer canister      |
| `<ConnectButton>`          | Renders wallet connection UI (Metamask, Coinbase, etc.) |

***

#### 2. `App` Component

Main application layout and structure.

```tsx
function App() {
  return (
    <div className="flex h-screen dark bg-zinc-900 text-white">
      <ChatWindow />
      <div className="w-64 bg-zinc-800 p-4 flex flex-col">
        <WalletConnectComponent />
      </div>
    </div>
  );
}
```

| Element                     | Description                           |
| --------------------------- | ------------------------------------- |
| `<div className="flex...">` | Main container with dark mode styling |
| `<ChatWindow />`            | Primary chat interface component      |
| `<WalletConnectComponent>`  | Sidebar wallet connection/management  |

***

#### 3. Root Rendering

Initializes the React application.

```tsx
ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <ThirdwebProvider client={client}>
      <App />
    </ThirdwebProvider>
  </React.StrictMode>
);
```

| Element              | Purpose                                         |
| -------------------- | ----------------------------------------------- |
| `<React.StrictMode>` | Development checks for potential problems       |
| `<ThirdwebProvider>` | Provides wallet context to all components       |
| `client={client}`    | Thirdweb configuration (from `./config/client`) |

***

### Key Features

1. **Wallet Integration**:
   * Automatic account creation on wallet connection
   * Supports Ethereum-compatible wallets (Metamask, WalletConnect, etc.)
   * Seamless integration with Internet Computer backend
2. **UI Structure**:
   * Responsive layout using Tailwind CSS
   * Dark mode styling (`bg-zinc-900`, `text-white`)
   * Component-based architecture
3. **Backend Communication**:
   * Uses `declarations/backend` for canister interaction
   * Automatic account registration via `create_account()` method

***

### Dependencies

| Dependency             | Purpose                                            |
| ---------------------- | -------------------------------------------------- |
| `thirdweb/react`       | Crypto wallet connection and Web3 functionality    |
| `react-dom`            | DOM rendering for React components                 |
| `declarations/backend` | Generated interface for Internet Computer canister |
| `tailwindcss`          | CSS styling framework                              |

***

### Customization Guide

#### 1. Add Wallet Information Display

```tsx
{account && (
  <div className="mt-4 p-3 bg-zinc-700 rounded-lg">
    <p>Connected: {account.address.slice(0,6)}...{account.address.slice(-4)}</p>
    <p>Network: {account.chain?.name || 'Unknown'}</p>
  </div>
)}
```

#### 2. Enhance Error Handling

```tsx
const [error, setError] = useState<string | null>(null);

useEffect(() => {
  if (account) {
    backend.create_account(account.address)
      .catch(err => {
        setError("Registration failed: " + err.message);
        console.error(err);
      });
  }
}, [account]);

{error && <div className="text-red-400 p-2">{error}</div>}
```

#### 3. Add Multi-Chain Support

```tsx
// In root rendering:
<ThirdwebProvider 
  client={client}
  supportedChains={[Ethereum, Polygon, Arbitrum]}
>
  <App />
</ThirdwebProvider>
```

#### 4. Implement Loading States

```tsx
const [isRegistering, setIsRegistering] = useState(false);

useEffect(() => {
  if (account) {
    setIsRegistering(true);
    backend.create_account(account.address)
      .finally(() => setIsRegistering(false));
  }
}, [account]);

{isRegistering && <div>Creating account...</div>}
```

***

###
