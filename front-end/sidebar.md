---
icon: lightbulb-exclamation-on
---

# Sidebar

#### Component Documentation: `Sidebar.tsx`

**Overview**

The `Sidebar` component provides a navigation panel for chat applications, featuring a "New Chat" action button and a scrollable list of chat history items. Designed with a dark theme using Tailwind CSS.

**Key Features**

* Persistent "New Chat" creation button
* Scrollable chat history list
* Hover interactions for all actionable items
* Responsive flex layout
* Sample data demonstration (10 placeholder items)

**Component Structure**

```jsx
export default function Sidebar() {
  return (
    <div className="w-64 bg-zinc-800 p-4 flex flex-col">
      <button className="bg-zinc-700 hover:bg-zinc-600 text-white p-2 rounded mb-4">
        + New Chat
      </button>
      
      <div className="flex-1 overflow-auto">
        <ul className="space-y-2">
          {Array.from({ length: 10 }).map((_, idx) => (
            <li key={idx} className="p-2 hover:bg-zinc-700 rounded cursor-pointer">
              Chat #{idx + 1}
            </li>
          ))}
        </ul>
      </div>
    </div>
  )
}
```

**Visual Design**

| Element          | Tailwind Classes                                            | Purpose/Effect                               |
| ---------------- | ----------------------------------------------------------- | -------------------------------------------- |
| Main Container   | `w-64 bg-zinc-800 p-4 flex flex-col`                        | Fixed width dark sidebar with padding        |
| New Chat Button  | `bg-zinc-700 hover:bg-zinc-600 text-white p-2 rounded mb-4` | Primary action button with hover effect      |
| Scroll Container | `flex-1 overflow-auto`                                      | Expands remaining space with scroll overflow |
| Chat List        | `space-y-2`                                                 | Vertical spacing between list items          |
| Chat List Item   | `p-2 hover:bg-zinc-700 rounded cursor-pointer`              | Interactive items with hover highlighting    |

**Interactive Elements**

1. **New Chat Button**:
   * Fixed position at top
   * `hover:bg-zinc-600` lightens background on hover
   * Rounded corners
2. **Chat List Items**:
   * Display as clickable elements
   * Change background on hover (`hover:bg-zinc-700`)
   * Show pointer cursor indicating interactivity
   * Uniform padding and rounded corners

**Layout Behavior**

* **Fixed Width**: Consistent 256px (16rem) width (`w-64`)
* **Vertical Stack**: Flex column layout (`flex flex-col`)
* **Scroll Management**:
  * Content area expands vertically (`flex-1`)
  * Automatic scrollbars when content overflows (`overflow-auto`)

**Sample Data Implementation**

```jsx
{Array.from({ length: 10 }).map((_, idx) => (
  <li key={idx}>Chat #{idx + 1}</li>
))}
```

