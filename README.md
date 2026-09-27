# HomeKey Prototype

**Developer:** Jiayu Feng

A Next.js prototype for a real-estate workflow interface, with separate buyer and seller journeys, timeline-based process visualization, and supporting frontend/backend integration points.

## File Structure
````
├── src
│   ├── app
│   │   ├── layout.tsx         # Root layout (HTML <head>, global providers)
│   │   ├── page.tsx           # Main entry: Hero, Timeline, Features, Footer
│   │   ├── styles
│   │   │   └── animation.css  #  animations
│   │   ├── types
│   │   │   └── item.ts        # Shared TS types: TimelineStage, FeatureItem
│   │   ├── data
│   │   │   └── stages.ts      # Static arrays: buyer/seller stages & features
│   │   ├── components
│   │   │   ├── Hero.tsx       # Navbar + Hero section
│   │   │   ├── Timeline.tsx   # AI timeline & Gantt chart
│   │   │   ├── Features.tsx   # Feature grid for buyers/sellers
│   │   │   └── Footer.tsx     # Site footer
│   │   └── globals.css        # Tailwind & global styles
│   ├── public                 # Static assets (favicon, images)
│   └── README.md              # ← You are here
├── next.config.ts             # Next.js configuration
├── tsconfig.json              # TypeScript configuration
├── package.json               # NPM scripts & dependencies
└── postcss.config.js          # Tailwind/PostCSS setup

````

---

## 🔗 Key Integration Points

### 1. Timeline & Stages
- **File:** `src/data/stages.ts`  
  Contains `buyerStages` and `sellerStages`: arrays of `TimelineStage`.  
- **Frontend:** passed as props into `Timeline` component (`src/app/components/Timeline.tsx`).

**Backend tasks:**
- Replace static arrays with calls to your REST/GraphQL endpoints.
- Each stage should map to a database record (e.g. `timeline_stages` table).
- Expose endpoints:
  - `GET /api/stages?type=buyer|seller`
  - `PATCH /api/stages/:id` to update completion/status.

---

### 2. Feature Listings
- **File:** `src/data/stages.ts`  
  Also exports `buyerFeatures` and `sellerFeatures`: arrays of `FeatureItem`.  
- **Frontend:** `Features.tsx` renders based on `activeTab`.

**Backend tasks:**
- Serve feature content dynamically, if needed:
  - `GET /api/features?role=buyer|seller`

---

### 3. Types & Contracts
- **File:** `src/app/types/item.ts`  
  Defines shared interfaces:
  ```ts
  export type TimelineStage = { id, title, description, duration, traditionalDuration, aiBenefit, isCompleted }
  export type FeatureItem = { id, title, description, icon }
---

### 4. Component Props

* **Hero.tsx**
  Props: `isVisible`, `activeTab`, `setActiveTab`
* **Timeline.tsx**
  Props: `isVisible`, `activeTab`, `setActiveTab`, `timelineRef`, `animatedSteps`, `setAnimatedSteps`, `showCompletionAnimation`, `setShowCompletionAnimation`, `expandedBenefit`, `setExpandedBenefit`, `setIsVisible`
* **Features.tsx**
  Props: `activeTab`, `setActiveTab`, `buyerFeatures`, `sellerFeatures`
* **Footer.tsx**
  No props

---

## 🛠️ Running & Developing

1. **Install**

   ```bash
   npm install
   ```
2. **Dev Server**

   ```bash
   npm run dev
   ```

3. **Backend API**
  ```bash
   cd backend
   npm install
   npm run dev
   ```

4. **MySQL Database**
  ```bash
   cd backend
   ./pocketbase serve
  ```
