---
icon: lightbulb-exclamation-on
---

# Navbar

Here's the English documentation for the Navbar component:

```react
/**
 * Fixed Navigation Bar Component with Responsive Design
 * 
 * A sticky navigation bar that transitions styles on scroll and provides
 * smooth navigation between application sections. Features both desktop
 * and mobile-responsive layouts with a toggleable mobile menu.
 * 
 * @component
 * @param {Object} props - Component properties
 * @param {Function} props.onSectionClick - Callback function triggered when navigation items are clicked
 * @param {string} props.currentSection - Currently active section identifier
 * 
 * @state {boolean} isScrolled - Tracks if user has scrolled past 20px for style changes
 * @state {boolean} isMobileMenuOpen - Controls mobile menu visibility
 * 
 * @features
 * - Scroll-responsive design with backdrop blur effect
 * - Mobile-first responsive layout with breakpoints
 * - Animated logo with gradient and status indicator
 * - Active section highlighting
 * - Smooth transitions and hover animations
 * - Accessible mobile menu with toggle animation
 * 
 * @breakpoints
 * - sm: 640px+ (Shows logo text, adjusts sizing)
 * - md: 768px+ (Shows desktop navigation)
 * 
 * @navigationItems
 * Contains array of navigation objects with:
 * - id: Section identifier
 * - label: Display text
 * - icon: Emoji visual indicator
 * 
 * @classes
 * Uses Tailwind CSS for styling with custom gradients and transitions
 */
```

Key Features Explained:

1. **Scroll Behavior**:

* Changes from transparent to semi-opaque background after 20px scroll
* Adds backdrop blur effect and border for glassmorphism effect

2. **Responsive Design**:

* Mobile menu (hidden on md+ screens)
* Conditional logo text visibility
* Adaptive spacing and sizing

3. **Interactive Elements**:

* Hover effects on all interactive items
* Active state highlighting with cyan accent color
* Animated logo with scale transformation on hover
* Live status indicator (green dot)

4. **Mobile Menu**:

* Slides down with backdrop blur
* Closes automatically on selection
* Mirror desktop navigation items

5. **Accessibility**:

* Semantic HTML structure
* ARIA-friendly toggle buttons
* Responsive touch targets

Usage Example:

```jsx
<Navbar 
  onSectionClick={(section) => handleNavigation(section)}
  currentSection={activeSection}
/>
```
