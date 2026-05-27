# Krushak Hithaishi - Project Structure & File Reference

## 📁 Complete Directory Structure

```
Krushak hithaishi/
├── package.json                    # Dependencies & scripts
├── vite.config.js                  # Vite build configuration
├── index.html                      # HTML entry point
├── .gitignore                      # Git ignore rules
│
├── README.md                       # Main project documentation
├── UI_DESIGN_GUIDE.md             # Comprehensive UI/UX guide
├── DEPLOYMENT_GUIDE.md            # Deployment & API integration
├── MOCKUPS_AND_SPECS.md          # Visual mockups & specifications
│
├── src/
│   ├── main.jsx                    # React application entry point
│   ├── App.jsx                     # Main app component (state management)
│   ├── App.css                     # Global styles & responsive design
│   │
│   └── screens/
│       ├── HomeScreen.jsx          # Feature showcase screen
│       ├── CameraScreen.jsx        # Leaf capture screen
│       ├── DiseaseDetectionScreen.jsx  # Detection results screen
│       ├── TreatmentScreen.jsx     # Treatment protocols screen
│       └── ShopsScreen.jsx         # Shop locator screen
│
└── node_modules/                   # Dependencies (auto-generated)
```

---

## 📄 File Descriptions

### **Configuration Files**

#### `package.json` (2KB)
**Purpose**: Project metadata, dependencies, and build scripts

**Key Scripts**:
```json
{
  "scripts": {
    "dev": "vite",                 // Start dev server on port 3000
    "build": "vite build",          // Build optimized production bundle
    "preview": "vite preview",      // Preview production build locally
    "start": "vite"                 // Alias for dev
  },
  "dependencies": {
    "react": "^18.2.0",            // Core React library
    "react-dom": "^18.2.0",        // React DOM utilities
    "lucide-react": "^0.338.0"     // Icon library
  }
}
```

---

#### `vite.config.js` (300B)
**Purpose**: Vite bundler configuration

**Configured Settings**:
- React plugin for JSX transformation
- Dev server on port 3000 with auto-open
- Optimized build settings

---

#### `index.html` (800B)
**Purpose**: HTML entry point for the React app

**Key Elements**:
- Viewport meta tag for mobile responsiveness
- Font system stack
- Root div for React mounting
- Deferred script loading of `src/main.jsx`

---

### **Documentation Files**

#### `README.md` (~3KB)
**Purpose**: Main project overview and quick start guide

**Includes**:
- Project vision & objectives
- Feature overview (5 key capabilities)
- App screen descriptions
- Technology stack
- Getting started instructions (npm install, npm run dev)
- Project structure
- Future enhancements
- Research context (IJRIAS 2025)

---

#### `UI_DESIGN_GUIDE.md` (~8KB)
**Purpose**: Comprehensive design system and component documentation

**Covers**:
- Screen-by-screen breakdown (all 5 screens)
- User journey flow diagram
- Color palette with hex codes
- Typography specifications (sizes, weights, colors)
- Spacing & layout guidelines
- Animation specifications
- Component architecture
- Accessibility compliance (WCAG 2.1 AA)

---

#### `DEPLOYMENT_GUIDE.md` (~6KB)
**Purpose**: Deployment, integration, and API connection instructions

**Includes**:
- Quick start (npm install, npm run dev)
- Production build instructions
- Deployment options (Vercel, Netlify, Docker, AWS S3)
- Backend API integration examples (detection, shops)
- Environment variables setup
- Performance optimization
- Testing checklist
- PWA setup instructions
- CI/CD pipeline with GitHub Actions
- Analytics & monitoring setup
- Launch checklist

---

#### `MOCKUPS_AND_SPECS.md` (~5KB)
**Purpose**: Visual mockups with ASCII art and precise specifications

**Shows**:
- All 5 screens with ASCII mockups
- Exact pixel dimensions (480×800px)
- Color references for each element
- Typography sizes for each text element
- Spacing measurements (8px baseline)
- Interactive states (hover, active, disabled)
- Complete color palette with hex codes
- Responsive breakpoints
- Animation timing and easing
- Visual hierarchy guide
- Accessibility checklist

---

### **Source Code Files**

#### `src/main.jsx` (100B)
**Purpose**: React application bootstrap

**Code**:
```javascript
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App'

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)
```

**Responsibilities**:
- Imports React and ReactDOM
- Imports the main App component
- Mounts React app to the `root` div in `index.html`
- Enables StrictMode for development warnings

---

#### `src/App.jsx` (~250 lines)
**Purpose**: Main application component managing all screens and state

**Key Features**:
- State management with `useState` hooks:
  - `currentScreen`: Tracks which screen is displayed
  - `detectionData`: Stores disease detection results
  
- Navigation between screens:
  - Home → Camera → Detection → Treatment → Shops
  - Back buttons work through the flow
  
- Mock data generation in `handleCaptureImage()`:
  - Simulates disease detection with realistic data
  - Includes weather, crop stage, soil moisture
  - Provides 3 ranked treatment recommendations

**Key Functions**:
```javascript
const [currentScreen, setCurrentScreen] = useState('home')
const [detectionData, setDetectionData] = useState(null)

const handleStartDetection = () => setCurrentScreen('camera')
const handleCaptureImage = (imagePath) => {
  // Simulate detection + set mock data
  setDetectionData(mockDetectionData)
  setCurrentScreen('detection')
}
const handleViewTreatment = () => setCurrentScreen('treatment')
const handleViewShops = () => setCurrentScreen('shops')
const handleBack = () => {
  // Navigate back through the flow
}
```

**Return JSX**:
- Conditionally renders correct screen component
- Passes data and callback props to children
- Maintains single source of truth for app state

---

#### `src/App.css` (~600 lines)
**Purpose**: Global styles covering all screens and components

**Main Sections**:

1. **Layout & Container** (`.app-container`, `.screen-container`)
   - Mobile-first 480px max-width
   - Flexbox layout for full-screen apps
   - Box shadows and borders

2. **Header Styling** (`.header`)
   - Green gradient background
   - Back button styling
   - Title text styling

3. **Button Styles** (`.btn`, `.btn-secondary`, `.btn-small`)
   - Green gradient with hover effects
   - Responsive sizing
   - Active/disabled states

4. **Card Components** (`.card`, `.shop-card`, `.treatment-item`)
   - Border radius 12px
   - Box shadows
   - Hover transitions

5. **Badges & Labels** (`.badge`, `.stat-label`)
   - Color-coded by severity/type
   - Rounded pills

6. **Weather Widget** (`.weather-widget`)
   - Blue gradient
   - Flex layout for weather items
   - Icon + value pairs

7. **Treatment Cards** (`.treatment-item`, `.treatment-rank`)
   - Ranked styling with number badges
   - Color-coded dosage/timing
   - Explanation sections

8. **Shop Cards** (`.shop-card`, `.shop-distance`, `.shop-stock`)
   - Distance badges (green)
   - Stock status highlights
   - Action button pairs

9. **Voice Player** (`.voice-player`, `.play-button`)
   - Gradient purple background
   - Circular play button
   - Language display

10. **Animations** (@keyframes)
    - `slideInRight`: Screen transitions
    - `fadeIn`: Card reveals
    - `slideUp`: Element animations
    - `spin`: Loading spinner

11. **Responsive Media Queries**
    - Mobile: 320px - 480px
    - Tablet: 481px - 768px
    - Desktop: 769px+

12. **Scrollbar Styling**
    - Custom scrollbar appearance
    - Smooth scrolling

---

### **Screen Components**

#### `src/screens/HomeScreen.jsx` (~100 lines)
**Purpose**: First screen showing features and onboarding

**Elements**:
- Header with app name (green background)
- Logo emoji (🌾)
- App title & subtitle
- 6 feature cards with emoji + description
- Primary CTA button "Scan a Leaf Now"
- Footer with mission statement

**Props**:
- `onStartDetection`: Callback when user clicks CTA

**State**: None (stateless component)

**Key Interactions**:
- Button click → Calls `onStartDetection()` → Navigate to Camera

---

#### `src/screens/CameraScreen.jsx` (~100 lines)
**Purpose**: Leaf capture interface

**Elements**:
- Header with back button & title
- Camera/image preview area (gray placeholder)
- Tips card with bullet points
- "Capture Leaf Image" button
- Loading state with spinner

**Props**:
- `onCapture(imagePath)`: Called when image captured
- `onBack()`: Called when back button clicked

**State**:
```javascript
const [showCapture, setShowCapture] = useState(false)
```

**Key Interactions**:
1. User clicks "Capture Leaf Image"
2. Sets `showCapture = true` (shows animation)
3. After 1.5s, calls `onCapture('/leaf-image.jpg')`
4. Parent component processes and navigates to Detection

**Simulations**:
- Image preview area shows gray background by default
- During capture: Green background with "📸 Capturing..." text
- Button disabled during capture

---

#### `src/screens/DiseaseDetectionScreen.jsx` (~150 lines)
**Purpose**: Display disease detection results with context

**Elements**:
- Header with back button
- Disease name card (red gradient with severity badge)
- Confidence score with visual progress bar
- Affected area stat
- Weather widget (blue) showing temp, humidity, rainfall, condition
- Two-column stats grid (crop stage, soil moisture)
- Disease information card with:
  - Causal agent (Alternaria solani)
  - Why detected now (environmental conditions)
  - Risk level assessment

**Props**:
- `data`: Detection result object with all disease info
- `onViewTreatment()`: Navigate to treatment screen
- `onBack()`: Navigate back to camera

**State**:
```javascript
const [showDetails, setShowDetails] = useState(false)
```

**Key Features**:
- Animated fade-in of cards on mount
- Confidence bar animates from 0% to actual percentage
- Color-coded severity badges (red for high)
- Bottom sticky button "View Treatment Options →"

**Data Structure**:
```javascript
data = {
  disease: 'Early Blight',
  confidence: 0.94,        // 0-1 scale
  severity: 'High',        // High/Medium/Low
  affectedArea: '35%',
  weather: {
    temperature: 24,
    humidity: 78,
    rainfall: 3.5,
    condition: 'Cloudy'
  },
  cropStage: 'Flowering',
  soilMoisture: 68
}
```

---

#### `src/screens/TreatmentScreen.jsx` (~200 lines)
**Purpose**: Show ranked treatment protocols with voice explanations

**Elements**:
1. **Current Treatment Card** (Green highlight)
   - Rank badge with effectiveness %
   - Product name (bold)
   - Dosage section
   - Timing section
   - Explanation section

2. **Voice Explanations** (4 language buttons)
   - Kannada, Telugu, English, Hindi
   - Button click triggers audio playback simulation
   - Shows "Playing..." indicator

3. **Alternative Treatments** (2 cards below)
   - Can be clicked to switch selection
   - Shows rank, dosage, and timing

4. **Application Instructions**
   - Before Spraying (4 bullet points)
   - After Spraying (4 bullet points)

5. **Bottom CTA**: "Find [Medicine] Near Me" with map icon

**Props**:
- `data`: Detection data with recommendations array
- `onViewShops()`: Navigate to shops screen
- `onBack()`: Navigate back to detection

**State**:
```javascript
const [selectedTreatment, setSelectedTreatment] = useState(0)
const [playingVoice, setPlayingVoice] = useState(null)
```

**Key Features**:
- Click alternative treatment → Updates selected index
- Click language button → Sets playingVoice state
- After 3s, clears playingVoice automatically
- Voice buttons disabled while playing

**Data Structure**:
```javascript
data.recommendations = [
  {
    rank: 1,
    name: 'Mancozeb 75% WP',
    dosage: '2.5 kg per acre',
    timing: 'Apply today evening (6 PM)',
    reason: 'High humidity creates ideal...',
    confidence: 0.94
  },
  // ... more recommendations
]
```

---

#### `src/screens/ShopsScreen.jsx` (~250 lines)
**Purpose**: Shop locator with Stockping integration

**Elements**:
1. **Search Summary Banner** (Green background)
   - Medicine being searched
   - Search radius & timestamp

2. **Shop Cards** (3 cards in array)
   - Shop name with verification badge
   - Address & distance
   - Stock count & status
   - Pricing (per kg & per acre)
   - Rating & hours
   - ETA badge
   - Call & Navigate buttons

3. **Selected Shop Details**
   - Expanded information section
   - Product details
   - Location & contact
   - Total cost for farm (large, bold)

4. **Process Timeline**
   - 5-step numbered list from confirmation to recovery

5. **Bottom CTA**: "Call [Shop Name]" button with phone icon

**Props**:
- `data`: Detection data with disease name
- `onBack()`: Navigate back to treatment

**State**:
```javascript
const [selectedShop, setSelectedShop] = useState(0)
```

**Key Interactions**:
- Tap shop card → Updates selected index & details
- Tap Call button → Shows alert with phone number
- Tap Navigate button → Would open maps (alert in demo)

**Mock Shops Data**:
```javascript
const shops = [
  {
    name: 'Kisan Krushi Kendra',
    distance: '2.3 km',
    address: 'Main Market, Bangalore',
    phone: '+91-9876543210',
    stock: 15,
    price: '450',           // per kg
    pricePerAcre: '1125',
    availability: 'In Stock',
    rating: 4.7,
    reviews: 234,
    hours: '6 AM - 8 PM',
    eta: '12',              // minutes
    verified: true
  },
  // ... more shops
]
```

**Color Coding**:
- Green: Available stock, good distance, verified
- Yellow: Limited stock
- Orange: Pricing (calls attention)
- Blue: Time/ETA information

---

## 🔄 Component Relationship Diagram

```
App.jsx (State Management)
├── [currentScreen = 'home']
│   └── HomeScreen.jsx
│       └── {onClick} → handleStartDetection()
│
├── [currentScreen = 'camera']
│   └── CameraScreen.jsx
│       ├── {onClick} → handleCaptureImage(imagePath)
│       ├── {onClick} → handleBack()
│
├── [currentScreen = 'detection']
│   └── DiseaseDetectionScreen.jsx (data)
│       ├── {onClick} → handleViewTreatment()
│       ├── {onClick} → handleBack()
│
├── [currentScreen = 'treatment']
│   └── TreatmentScreen.jsx (data)
│       ├── {onClick} → handleViewShops()
│       ├── {onClick} → handleBack()
│
└── [currentScreen = 'shops']
    └── ShopsScreen.jsx (data)
        └── {onClick} → handleBack()
```

---

## 📊 Code Statistics

| File | Lines | Purpose |
|------|-------|---------|
| App.jsx | 250 | Main state & navigation |
| App.css | 600 | All styling |
| HomeScreen.jsx | 100 | Onboarding |
| CameraScreen.jsx | 100 | Image capture |
| DiseaseDetectionScreen.jsx | 150 | Results display |
| TreatmentScreen.jsx | 200 | Treatments + voice |
| ShopsScreen.jsx | 250 | Shop finder |
| **Total** | **~1,650** | **Production code** |

---

## 🎯 Key Design Patterns Used

### **1. Component Composition**
- 5 screen components, each handling one feature
- Shared CSS through App.css
- Reusable component patterns

### **2. State Management**
- Single source of truth in App.jsx
- Props passed down to children
- Callbacks passed up to App

### **3. Conditional Rendering**
```javascript
{currentScreen === 'home' && <HomeScreen />}
{currentScreen === 'camera' && <CameraScreen />}
// ... etc
```

### **4. Mock Data Pattern**
- Realistic data structure for backend integration
- Can swap mock data with API calls
- Consistent data flow

### **5. Navigation Flow**
- Linear flow through screens
- Back button works through stack
- State maintains context across screens

---

## 🔗 Integration Points for Backend

**Replace these with real API calls**:

1. **Detection API**: `App.jsx` line ~85
   - Current: Mock data generation
   - Replace with: `fetch('/api/detection', ...)`

2. **Shop Finder API**: `ShopsScreen.jsx` line ~20
   - Current: Hardcoded shop array
   - Replace with: `fetch('/api/shops', ...)`

3. **Voice API**: `TreatmentScreen.jsx` line ~115
   - Current: 3-second simulation
   - Replace with: `fetch('/api/voice/explain', ...)`

4. **Weather API**: `App.jsx` line ~85
   - Current: Mock data
   - Replace with: `fetch('https://api.open-meteo.com/...')`

5. **Maps Integration**: `ShopsScreen.jsx` button handlers
   - Current: Alert dialogs
   - Replace with: `window.open('https://maps.google.com/...')`

---

## 🚀 To Get Started

1. **Review README.md** for project overview
2. **Look at MOCKUPS_AND_SPECS.md** to see exact screen layouts
3. **Check UI_DESIGN_GUIDE.md** for design system details
4. **Read App.jsx** to understand state management flow
5. **Review individual screen components** to see implementation
6. **Check DEPLOYMENT_GUIDE.md** for backend integration

---

**Total Production Code**: ~1,650 lines
**Total Documentation**: ~20KB of detailed guides
**Ready for**: Production deployment with API integration
