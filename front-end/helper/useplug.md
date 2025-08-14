---
description: React Hook for Connecting to the Plug Wallet and Creating Canister Actors
icon: tally-1
---

# usePlug

### `usePlug.ts`&#x20;

This file defines a **custom React + TypeScript hook** that makes it easier to connect a frontend application to the **Plug** Internet Computer wallet extension, manage its connection state, and create actors for calling canisters.

***

#### **Global Type Declaration**

```ts
declare global {
  interface Window {
    ic?: {
      plug?: {
        isConnected: () => Promise<boolean> | boolean;
        requestConnect: (opts: { ... }) => Promise<boolean>;
        createActor: <T>(opts: { canisterId: string; interfaceFactory: any; }) => Promise<T>;
        getPrincipal: () => Promise<{ toText: () => string }>;
        disconnect?: () => Promise<void>;
      };
    };
  }
}
```

* Extends the `Window` interface to include the `ic.plug` object provided by the Plug extension.
* Declares the available Plug methods:
  * **`isConnected`** — Checks if the wallet is connected.
  * **`requestConnect`** — Requests user permission to connect.
  * **`createActor`** — Creates a typed canister actor from an `idlFactory`.
  * **`getPrincipal`** — Retrieves the user’s principal.
  * **`disconnect`** _(optional)_ — Disconnects from the wallet.

***

#### **Types**

```ts
export type PlugState = { ... };
export type ConnectOptions = { ... };
```

* **`PlugState`** — Holds connection status, principal, and error information.
* **`ConnectOptions`** — Options for connecting to Plug (whitelist, host, timeout, key type).

***

#### **The `usePlug` Hook**

```ts
export function usePlug(defaultOpts?: ConnectOptions) { ... }
```

* Manages Plug wallet state and provides helper methods for interaction.
* **State Variables:**
  * `available` — Whether Plug is installed.
  * `connected` — Whether the user is connected to the site.
  * `principal` — The user’s wallet principal (if connected).
  * `error` — Any error message from recent operations.

***

**1. `refresh`**

```ts
const refresh = useCallback(async () => { ... }, []);
```

* Checks if Plug is available and updates connection state.
* If connected, retrieves the user’s principal.
* Called automatically when the component mounts.

***

**2. `connect`**

```ts
const connect = useCallback(async (opts?: ConnectOptions) => { ... }, [...]);
```

* Merges `defaultOpts` and `opts` to form connection settings.
* Calls `requestConnect` on Plug to request access from the user.
* If approved, updates connection state and retrieves principal.

***

**3. `disconnect`**

```ts
const disconnect = useCallback(async () => { ... }, []);
```

* Disconnects from the wallet if Plug supports `disconnect`.
* Clears connection state.

***

**4. `createActor`**

```ts
const createActor = useCallback(async <T,>(canisterId: string, idlFactory: any): Promise<T> => { ... }, [state.connected]);
```

* Creates a typed canister actor using `idlFactory` and `canisterId`.
* Throws an error if Plug is not connected.

***

**5. `getPrincipal`**

```ts
const getPrincipal = useCallback(async () => { ... }, [state.connected]);
```

* Retrieves the user’s principal in text format.
* Throws an error if Plug is not connected.

***

**6. Auto Refresh**

```ts
useEffect(() => { refresh(); }, [refresh]);
```

* Automatically checks Plug status when the hook is first used.

***

**7. Returned API**

```ts
const api = useMemo(() => ({ ...state, connect, disconnect, refresh, createActor, getPrincipal }), [...]);
return api;
```

* Returns an object containing:
  * Current state (`available`, `connected`, `principal`, `error`)
  * Methods (`connect`, `disconnect`, `refresh`, `createActor`, `getPrincipal`)

####

