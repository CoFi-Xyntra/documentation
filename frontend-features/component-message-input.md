---
icon: tally-2
---

# Component - Message Input

#### Component Documentation: `MessageInput.tsx`

**Overview**

The `MessageInput` component provides a message input interface for chat applications. It features a text input field and a submission button with responsive styling using Tailwind CSS.

**Key Features**

* Clean, modern UI with dark mode styling
* Responsive flex layout
* Hover effects on interactive elements
* Accessibility-ready form structure

**Component Structure**

```jsx
export default function MessageInput() {
  return (
    <div className="p-4 border-t border-zinc-700 bg-zinc-900">
      <form className="flex items-center gap-2">
        <input
          type="text"
          className="flex-1 p-2 rounded bg-zinc-800 text-white outline-none"
          placeholder="Send a message"
        />
        <button
          type="submit"
          className="bg-blue-600 hover:bg-blue-500 px-4 py-2 rounded text-white"
        >
          Send
        </button>
      </form>
    </div>
  )
}
```

**Visual Design**

| Element       | Tailwind Classes                                             | Purpose/Effect                                 |
| ------------- | ------------------------------------------------------------ | ---------------------------------------------- |
| Container     | `p-4 border-t border-zinc-700 bg-zinc-900`                   | Top border separator with dark background      |
| Form          | `flex items-center gap-2`                                    | Flex layout with centered items and 0.5rem gap |
| Input Field   | `flex-1 p-2 rounded bg-zinc-800 text-white outline-none`     | Responsive input with dark styling, no outline |
| Submit Button | `bg-blue-600 hover:bg-blue-500 px-4 py-2 rounded text-white` | Primary button with hover effect               |

**Accessibility Features**

1. **Semantic HTML**: Proper use of `<form>`, `<input>`, and `<button>` elements
2. **Input Placeholder**: Clear "Send a message" prompt
3. **Hover States**: Visual feedback on button interaction
4. **Focus Management**: Outline removal maintains native focus ring for accessibility

**Responsive Behavior**

* **Flex Layout**: Input field expands to fill available space (`flex-1`)
* **Button**: Maintains fixed padding at all screen sizes
* **Spacing**: Consistent 0.5rem gap between elements (`gap-2`)

**Usage Recommendations**

1. **State Management**: Should be controlled by parent component (like `ChatWindow`)
2. **Event Handling**: Requires `onSubmit` handler on form and `onChange` on input
3. **Disable States**: Add `disabled` attributes during submission processes
4. **Validation**: Implement input validation in parent component

**Integration Example**

```jsx
// Parent component usage
<MessageInput 
  value={inputValue}
  onChange={(e) => setInputValue(e.target.value)}
  onSubmit={handleSubmit}
  isLoading={isLoading}
/>
```

**Enhancement Opportunities**

1. Add typing indicators
2. Implement file attachment support
3. Add emoji picker integration
4. Include character counter
5. Add voice input support

