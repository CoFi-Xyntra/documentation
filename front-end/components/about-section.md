---
icon: lightbulb-exclamation-on
---

# About Section

### Overview

The `AboutSection` component is a React functional component that renders a comprehensive "About Us" section for the COFI XYNTRA project. It includes company information, statistics, mission statement, team member profiles, and a call-to-action for recruitment.

### Data Structures

#### Team Members

The component defines an array of team member objects with the following structure:

```typescript
interface TeamMember {
  id: string;
  name: string;
  role: string;
  bio: string;
  image: string;
  linkedin: string;
  twitter: string;
  specialties: string[];
}
```

#### Company Statistics

The component defines an array of company statistic objects with the following structure:

```typescript
interface CompanyStat {
  label: string;
  value: string;
  icon: string;
}
```

### UI Sections

#### 1. Header Section

* Displays the company name with gradient styling
* Provides a brief description of the company's mission

#### 2. Company Statistics

* Renders 4 statistical indicators in a responsive grid
* Each stat includes an icon, value, and label
* Features hover effects and transitions

#### 3. Mission Statement

* Displays the company's mission in a styled container
* Uses gradient background with border effects

#### 4. Team Section

* Features team member profiles in a responsive grid
* Each profile includes:
  * Profile image (placeholder with initials)
  * Name and role
  * Biography
  * Specialty tags
  * Social media links (LinkedIn and Twitter)
  * Hover effects and animations

#### 5. Call-to-Action

* Encourages visitors to join the team
* Includes a styled button that links to job openings

### Usage

To use this component, simply import and include it in your React application:

```typescript
import { AboutSection } from './AboutSection';

function App() {
  return (
    <div>
      <AboutSection />
      {/* Other components */}
    </div>
  );
}
```

### Customization

To customize this component:

1. Replace placeholder images with actual team member photos
2. Update team member information in the `teamMembers` array
3. Modify company statistics in the `companyStats` array
4. Adjust colors and gradients to match your brand
5. Update social media links with actual URLs

### Dependencies

This component requires:

* React
* Tailwind CSS (with appropriate configuration)
* Heroicons or similar icon set (for social media icons)

###
