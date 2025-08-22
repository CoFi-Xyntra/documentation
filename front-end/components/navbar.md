---
icon: lightbulb-exclamation-on
---

# Navbar

The `Navbar` component is a responsive navigation bar built with **React** and **Tailwind CSS**. It supports both desktop and mobile views, includes animated UI effects, and allows dynamic navigation between different sections of the page. This component also features a scroll effect that changes the navbar's background when the user scrolls down the page.

***

#### **Props**

* **`onSectionClick: (section: string) => void`**
  * A callback function that is triggered when a navigation item is clicked. It receives the section ID as a parameter.
* **`currentSection: string`**
  * The ID of the current active section, used to highlight the selected navigation item.

***

#### **Structure**

* **Logo Area**
  * Displays the brand logo and name.
  * Clicking the logo navigates to the **Home** section.
* **Desktop Navigation**
  * Visible on screens `md` and above.
  * Displays navigation items horizontally.
* **Mobile Navigation**
  * Accessible via a hamburger menu button on small screens.
  * Expands a vertical list of navigation items.

***

#### **Hooks Used**

* **`useState`**
  * `isScrolled`: Tracks if the page has been scrolled.
  * `isMobileMenuOpen`: Controls visibility of the mobile menu.
* **`useEffect`**
  * Adds/removes scroll listener for background change effect.

***

#### **Styling**

* Built with **Tailwind CSS** utility classes.
* Includes transitions and hover animations for a smooth user experience.
* Uses gradient backgrounds and semi-transparent overlays for a modern look.

***

#### **Usage Example**

```tsx
import { Navbar } from './Navbar';

const App = () => {
  const [currentSection, setCurrentSection] = useState('home');

  const handleSectionClick = (section: string) => {
    setCurrentSection(section);
    document.getElementById(section)?.scrollIntoView({ behavior: 'smooth' });
  };

  return (
    <>
      <Navbar onSectionClick={handleSectionClick} currentSection={currentSection} />
      {/* Your page sections here */}
    </>
  );
};
```
