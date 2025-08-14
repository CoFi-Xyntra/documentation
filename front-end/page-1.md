---
description: UI Component for Connecting to Plug Wallet
icon: v
---

# Page 1

### `ConnectPlugButton.tsx`&#x20;

This React component provides a **simple, user-friendly button** to connect your application to the **Plug** Internet Computer wallet.\
It uses the `usePlug` hook to handle wallet detection, connection, and disconnection.

***

#### **Props**

```ts
type Props = {
  whitelist?: string[];   // List of canister IDs the wallet should authorize
  host?: string;          // Network host (e.g., "https://ic0.app" for ICP mainnet)
  className?: string;     // Optional CSS class for custom styling
};
```

* **`whitelist`** — Canisters that the Plug wallet will allow access to.
* **`host`** — Target ICP network (mainnet or local development).
* **`className`** — Optional custom CSS class for button styling.

***

#### **Logic**

1.  **Initialize Wallet State**

    ```ts
    const plug = usePlug({ whitelist, host });
    ```

    * Uses the `usePlug` hook to check if Plug is available and manage its connection state.
2.  **Shorten Principal**

    ```ts
    const short = (p?: string) => (p ? `${p.slice(0, 5)}...${p.slice(-5)}` : "");
    ```

    * Helper function to display a shortened version of the user’s principal.
3.  **When Plug Is Not Installed**

    ```tsx
    if (!plug.available) {
      return <a href="https://plugwallet.ooo/">Install Plug</a>;
    }
    ```

    * Shows an **Install Plug** link directing users to the official site.
4.  **When Plug Is Connected**

    ```tsx
    if (plug.connected) {
      return (
        <div>
          Connected: {short(plug.principal)}
          <button onClick={plug.disconnect}>Disconnect</button>
        </div>
      );
    }
    ```

    * Displays the connected principal and a **Disconnect** button.
5.  **When Plug Is Available but Not Connected**

    ```tsx
    return (
      <button onClick={() => plug.connect({ whitelist, host })}>
        Connect Plug
      </button>
    );
    ```

    * Shows a **Connect Plug** button that triggers the connection flow.

####

