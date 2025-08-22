---
icon: lightbulb-exclamation-on
---

# Landing Page

### Overview

The `LandingPage` component is a comprehensive React component that serves as the main landing page for the COFI XYNTRA DeFi application. It features an animated background, navigation system, and multiple sections including hero, products, documentation, and about sections.

### Component Structure

#### Props

```typescript
interface LandingPageProps {
  onEnterApp: () => void;
}
```

#### State Management

The component uses several state variables:

* `isVisible`: Controls initial fade-in animation
* `currentText`: Manages the currently displayed text in the rotating headline
* `currentSection`: Tracks the currently active section for navigation

### Technical Features

#### Animation System

Uses multiple CSS keyframe animations:

* `gradientShift`: Animated gradient background
* `radialMove`: Radial gradient movement
* `floatGentle`: Floating elements animation
* `lightRay`: Light beam effects
* `symbolFloat`: Floating crypto symbols

### Usage

```typescript
import LandingPage from './LandingPage';

function App() {
  const handleEnterApp = () => {
    // Handle app entry logic
  };

  return (
    <LandingPage onEnterApp={handleEnterApp} />
  );
}
```

### Dependencies

* React
* Tailwind CSS
* Heroicons (for icons)
* Custom CSS animations

###
