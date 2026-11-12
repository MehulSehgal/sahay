# Contributing to Sahay — Cognitive Care Platform for Elders

Thank you for your interest in contributing to **Sahay**! Our mission is to build a culturally grounded, compassionate, and accessible cognitive care platform for elders across North-East India and beyond.

---


## 🌐 Step 1: Explore Before You Contribute
Before contributing, please:
- **Read the [README](./README.md)** to understand the project.
- **Explore the deployed website** to get a sense of its structure and features.
- Review **open issues** and **issue templates** to find where you can contribute.


## 💻 Step 2: Project Setup

```bash
# Install dependencies
npm install

# Start Express + Vite full-stack server
npm run dev

# Run TypeScript build check
npm run build
```

The app runs on port 3000 at `http://localhost:3000`.

---


## 🧭 Step 3: How to Contribute

1. **Star ⭐ and Fork 🍴** this repository.  

2. **Code Contributions:**  
   - Create a new branch based on the type of change *(see [Branch & Commit Conventions](#-branch--commit-conventions))*  
     ```bash
     git checkout -b feature/new-section
     ```
   - Make your code adjustments.  
   - Commit changes following the convention *(see [Branch & Commit Conventions](#-branch--commit-conventions))*.  
   - Open a Pull Request (PR).

3. **Design Contributions:**  
   - Include Figma or screen design images and links in your PR. You may upload screenshots, Figma links, or UI/UX previews.  
   - Place files in the designated design folders or relevant `.md` sections.
  
4. **Maintenance Contributions:**  
   - Address issues like:
     - Extracting embedded images or assets and adding them to `/assets/`.  
     - Moving CSS/JS into separate files.  
     - Updating README or file structure consistency.  
   - Submit your PR under the “maintenance” label.


---

# 🪶 Branch & Commit Conventions

| Type              | Branch Prefix | Commit Prefix | Description                                 |
| ----------------- | ------------- | ------------- | ------------------------------------------- |
| New Feature     | `feature/`    | `feat:`       | Adding new functionality or pages           |
| Bug Fix        | `fix/`        | `fix:`        | Resolving issues or broken behavior         |
| Maintenance    | `chore/`      | `chore:`      | Config updates, repo organization           |
| Documentation | `docs/`       | `docs:`       | Updating docs, README, or guides            |
| UI/UX & Design | `uiux/`       | `design:`     | Design mockups, page revamps, visual tweaks |
| Resources      | `resources/`  | `resource:`   | Adding educational content/resources        |
| Refactor       | `refactor/`   | `refactor:`   | Code improvement without feature change     |
| Style          | `style/`      | `style:`      | CSS fixes, spacing, or formatting changes   |

Example: 
```bash
# Branch
uiux/community-redesign

# Commit
design: revamp Community page layout for better clarity
```

---

# 🧾 Issue & Pull Request Rules

1. Browse through existing issues before creating new ones.
2. Get assigned to an issue before starting work.
3. No duplicate or spam issues.
4. If no PR or update is made within 5 days of assignment, it may be reassigned.
5. Major issues may have sub-issues — feel free to request one if you want to contribute to a smaller part.
6. Always mention issue number in your PR description (e.g., “Fixes #12”).

---
## Sahay Contribution Help

## 🌟 The "Golden Skeleton" Philosophy

Sahay is architected with a **golden baseline**:
1. **Fully Functional Reference Modules**:
   - The entire app shell (Desktop Sidebar, Responsive Mobile Nav, Topbar, Settings, Accessibility zoom).
   - **4 Flagship Cognitive Games**: Memory Match, Pattern Recall, Routine Recall, and Spot the Difference.
   - **Care Schedule Engine**: Reminders with interactive check-offs, search, and additions.
   - **Appointments System**: Upcoming clinical sessions with simulated direction/video triggers.
   - **Family & Caregiver Oversight**: Memory book with voice playback, live geofence map with radius slider, and alert feed.
   - **AI Voice Companion ("Talk to Sahay")**: Backed by Gemini server-side API with regional language awareness.
2. **Scaffolded Contributor Slots**:
   - Open slots for additional cognitive exercises (`Face & Family Match`, `Odd One Out`, `Number Recall`).
   - Localization dictionaries (Assamese, Bodo, Khasi, Manipuri, Mizo).
   - Hardware sensor or real GPS integration.

---

## 🧩 How to Add a New Cognitive Game (3 Steps)

Follow this recipe to implement one of the open activities (such as `faces`, `odd`, or `numbers`):

### Step 1: Create your game component
In `src/features/activities/games/YourGameName.tsx`:

```tsx
import React, { useState } from 'react';

interface YourGameProps {
  onSessionComplete?: (stats: { moves: number; accuracy: number }) => void;
  showToast: (msg: string, icon?: string) => void;
}

export const YourGameName: React.FC<YourGameProps> = ({ onSessionComplete, showToast }) => {
  // 1. Maintain local game state
  // 2. Render cards/tiles with 44px+ touch targets
  // 3. Call onSessionComplete({ moves, accuracy }) when finished
  return (
    <div className="max-w-[440px] mx-auto text-center">
      {/* Game board */}
    </div>
  );
};
```

### Step 2: Register in `src/features/activities/activityRegistry.ts`
Update the status of your activity from `'contribute'` to `'active'`:

```ts
{
  id: 'faces',
  title: 'Face & Family Match',
  description: '...',
  category: 'Memory',
  level: 1,
  maxLevel: 3,
  status: 'active', // <--- Change to 'active'
  iconName: 'user',
}
```

### Step 3: Wire into `src/features/activities/ActivityHost.tsx`
Import your component and return it in `renderGameContent()`:

```tsx
case 'faces':
  return <FaceFamilyMatch onSessionComplete={onSessionComplete} showToast={showToast} />;
```

---

## 🎨 Elder-Friendly Design System Rules

Please respect these principles when designing or contributing UI:

1. **Warm Palette**:
   - Background: `#FBF7EE` (Warm Paper)
   - Accent / Cards: `#FFFFFF` (Surface) with `#E6DAB9` (Muted Line borders)
   - Deep Forest: `#22403A` for headers and primary controls
   - Marigold: `#E2A33D` for milestones and active cards
2. **Typography**:
   - Headings: `font-fraunces` (Fraunces serif)
   - Controls & Badges: `font-baloo` (Baloo 2)
   - Body copy: `font-mulish` (Mulish sans-serif)
3. **Accessibility**:
   - Minimum touch target: 44px by 44px.
   - Text size responds to the user’s font scaler (`Normal`, `Large`, `Extra Large`).
   - High contrast (passes WCAG AA).
4. **Positive Framing**:
   - Never show "Game Over" or punitive red failure banners. Frame misses gently: *"Let's take a breath and try a shorter sequence."*

---


## 📋 Good First Issues 

Head to the issues tab to explore issues:

1. **Odd One Out Game (`odd`)**: Adding categorical classification with culturally rooted Assamese/NE items (`good first issue`, `easy`).
2. **Regional Localization**: Adding localized greeting phrases and reminder presets for Khasi, Bodo, and Mizo (`good first issue`, `easy`).
3. **Voice Pitch & Speech Speed Customizer**: User preferences for speech synthesis rate (`good first issue`, `easy`).
4. **Memory Book Audio Recording**: Hooking up browser MediaRecorder API to record custom family messages directly in the browser (`medium`, `help wanted`).

---

# 📜 Code of Conduct

Please note that this project is governed by a [Code of Conduct](./CODE_OF_CONDUCT.md).  
By participating, you are expected to uphold a respectful, inclusive, and positive environment for everyone.  
Be kind, constructive, and professional in all discussions and contributions.

---

# 🙌 Acknowledgements

We deeply appreciate every contributor who helps make **Sahay** better.  
Whether it’s fixing a small bug, improving design, or refining documentation - your efforts matter.

Special thanks to:
- **Project Maintainers** – for guidance and reviews  
- **Contributors** – for creativity and effort  
- **Community Members** – for feedback, testing, and support  

Your contribution helps build a safer, more connected digital space for all.
