---
icon: tally-1
---

# Chat Window

#### Component Documentation: `ChatWindow` `.tsx`

**Overview**

`ChatWindow` is a React chat interface component that enables users to interact with a financial agent backend hosted on the Internet Computer blockchain. It displays a conversation history, handles user input, and manages API communication with the backend service.

**Key Features**

* Real-time message display with user/system differentiation
* Asynchronous communication with blockchain backend
* Loading states and error handling
* Responsive UI with Tailwind CSS styling

**State Management**

| State Variable | Type    | Description                                                              |
| -------------- | ------- | ------------------------------------------------------------------------ |
| `chat`         | Array   | Stores chat history objects with `user`/`system` messages                |
| `inputValue`   | string  | Tracks current value of message input field                              |
| `isLoading`    | boolean | Indicates when backend request is in progress (disables UI interactions) |

**Core Functions**

1. **`formatDate(date: Date)`**\
   &#xNAN;_&#x46;ormats timestamps to HH:MM (currently unused in UI)_
2. **`askAgent(messages: any[])`**\
   Handles backend communication:
   * Sends conversation history to `backend.chat()` endpoint
   * Updates chat with response on success
   * Implements error parsing for blockchain-specific errors
   * Manages loading states
3. **`handleSubmit(e: React.FormEvent)`**\
   Message submission handler:
   * Validates input
   * Updates chat with user message + "Thinking..." placeholder
   * Triggers backend request
   * Resets input field

**Component Structure**

```jsx
<div className="flex flex-col flex-1 overflow-hidden">
  {/* Message history container */}
  <div className="flex-1 overflow-auto p-6 space-y-4 flex flex-col">
    {chat.map(/* renders message bubbles */)}
  </div>

  {/* Input area */}
  <div className="p-4 border-t border-zinc-700 bg-zinc-900">
    <form onSubmit={handleSubmit}>
      <input /* message input */ />
      <button /* submit button */ />
    </form>
  </div>
</div>
```

**Message Rendering Logic**

```jsx
chat.map((message, index) => {
  const isUser = !!message.user;
  return (
    <div key={index} className={`flex ${isUser ? 'justify-end' : 'justify-start'}`}>
      <div className={`p-4 rounded-lg ${isUser ? 'bg-blue-600' : 'bg-zinc-800'}`}>
        {isUser ? message.user.content : message.system.content}
      </div>
    </div>
  );
})
```

**Backend Integration**

* Uses `backend.chat()` method from `declarations/backend`
* Payload structure: Array of message objects
*   Error handling for Internet Computer-specific errors:

    ```ts
    const match = String(e).match(/(SysTransient|CanisterReject), \\+"([^\\"]+)/);
    ```

**UI Features**

* Message bubbles color-coded by sender (blue for user, dark gray for system)
* Responsive layout with flexbox
* Input disabled during loading states
* Auto-scroll functionality (currently commented out)

**Usage Notes**

1. **Initial State**:\
   Displays welcome message from system agent
2. **Submit Workflow**:\
   User input → Add user message → Show "Thinking..." → API call → Replace with response
3. **Error Handling**:
   * Alerts user with parsed error message
   * Removes "Thinking..." placeholder on failure

**Optimization Opportunities**

1. Enable auto-scroll (uncomment useEffect)
2. Add message timestamps using `formatDate()`
3. Implement markdown rendering for system messages
4. Add rate limiting for submissions

**Dependencies**

```ts
import { useEffect, useRef, useState } from 'react';
import { backend } from 'declarations/backend'; // Internet Computer backend interface
```

**Styling Reference**

| Element        | Tailwind Classes                           |
| -------------- | ------------------------------------------ |
| User Message   | `bg-blue-600 text-white justify-end`       |
| System Message | `bg-zinc-800 text-white justify-start`     |
| Input Field    | `bg-zinc-800 text-white outline-none`      |
| Submit Button  | `bg-blue-600 hover:bg-blue-500 text-white` |
| Container      | `bg-zinc-900 border-zinc-700`              |
