# Krushak Hithaishi - Visual UI Mockups & Screen Specifications

## 📱 Mobile Device Viewport: 480px × 800px (iPhone SE / Pixel 4)

---

## SCREEN 1: HOME SCREEN
```
┌─────────────────────────────────┐
│ KRUSHAK HITHAISHI               │  ← Header (Green Gradient)
│ Krushak Hithaishi               │  ← App Logo: 🌾
│                                 │
│ Intelligent Disease Detection   │
│ & Treatment Pipeline            │
│                                 │
├─────────────────────────────────┤
│                                 │
│ 📸 AI-Powered Detection         │
│ Point your phone at diseased    │
│ leaf for instant diagnosis      │
│                                 │
│ ☁️ Real-time Weather            │
│ Considers weather, soil, and    │
│ growth stage for treatment      │
│                                 │
│ 💊 Ranked Treatment Protocols   │
│ Get specific dosage, timing     │
│ & explanation for each          │
│                                 │
│ 🗣️ Native Language Voice         │
│ Understand in Kannada,          │
│ Telugu & other languages        │
│                                 │
│ 🏪 Instant Shop Location        │
│ Find nearby shops with exact    │
│ medicine in stock right now     │
│                                 │
│ ✅ Complete in 15 Minutes       │
│ From problem to purchase        │
│ all in one app                  │
│                                 │
├─────────────────────────────────┤
│  [SCAN A LEAF NOW] (Green Btn)  │  ← CTA Button (Full Width)
│                                 │
│ Closing the gap between AI      │
│ detection and on-ground         │
│ treatment availability          │
└─────────────────────────────────┘
   FOOTER
```

**Color Scheme**:
- Header: Linear gradient (Dark Green → Light Green)
- Background: White
- Feature icons: Emoji (colored naturally)
- Button: Solid green with white text
- Footer text: Light gray

**Typography**:
- Logo: 24px, Bold, Dark Gray
- Subtitle: 14px, Regular, Gray
- Feature title: 14px, Bold, Dark
- Feature description: 13px, Regular, Medium Gray
- Button: 16px, Bold, White

---

## SCREEN 2: CAMERA SCREEN
```
┌─────────────────────────────────┐
│ ← [Back]  SCAN LEAF             │  ← Header with back button
├─────────────────────────────────┤
│                                 │
│  ┌───────────────────────────┐  │
│  │                           │  │  ← Camera/Image Preview
│  │        📱                 │  │     400px × 300px
│  │  Point camera at leaf     │  │     Gray background
│  │                           │  │
│  └───────────────────────────┘  │
│                                 │
│ LEAF SCANNING TIPS              │  ← Card section
│                                 │
│ • Place leaf on white           │
│   background                    │
│ • Ensure good lighting          │
│ • Focus on affected area        │
│ • Keep camera steady            │
│ • Capture entire leaf           │
│                                 │
│                                 │
├─────────────────────────────────┤
│ [CAPTURE LEAF IMAGE] (Green)    │  ← Action button
└─────────────────────────────────┘
```

**Interactions**:
- Button click → Shows "Analyzing Leaf..."
- Progress: Spinner animation for 1.5 seconds
- Transition: Fade to Detection Screen

**States**:
- Default: "CAPTURE LEAF IMAGE" (enabled)
- Loading: "ANALYZING LEAF..." (disabled, opacity 0.6)

---

## SCREEN 3: DISEASE DETECTION RESULT
```
┌─────────────────────────────────┐
│ ← [Back]  DETECTION RESULT      │  ← Header
├─────────────────────────────────┤
│                                 │
│  Early Blight 🔴 HIGH           │  ← Red card, left border
│  Confirmed fungal infection     │
│                                 │
│  ▰▰▰▰▰▰▰▰▰▰ 94%               │  ← Confidence bar + %
│                                 │
│  35%                            │  ← Affected area stat
│  of leaf surface affected       │
│                                 │
│ ENVIRONMENTAL CONTEXT           │  ← Blue weather widget
│ 🌡️ Temperature      24°C        │
│ 💧 Humidity         78%         │
│ 🌧️ Rainfall (24h)   3.5mm      │
│ ☁️ Condition        Cloudy      │
│                                 │
│ ┌──────────────────────────────┐│
│ │ Crop Stage: Flowering      │ ││  ← Two-column stats
│ │ Soil Moisture: 68%         │ ││
│ └──────────────────────────────┘│
│                                 │
│ ABOUT EARLY BLIGHT              │  ← Info cards
│ Causal Agent:                   │
│ Alternaria solani - A fungal    │
│ pathogen that thrives in warm,  │
│ humid conditions                │
│                                 │
│ Why It's Detected Now:          │
│ Current humidity (78%) +        │
│ temperature (24°C) + rainfall   │
│ create ideal fungal growth      │
│ conditions...                   │
│                                 │
│ Risk Level:                     │
│ 🔴 HIGH - Rapid spread          │
│ expected in 48 hours without    │
│ intervention. Immediate action  │
│ required.                       │
│                                 │
├─────────────────────────────────┤
│ [VIEW TREATMENT OPTIONS →]      │  ← Primary CTA
└─────────────────────────────────┘
```

**Color Coding**:
- Disease card: Red gradient (#fee2e2 → #fecaca)
- Disease text: Dark red (#7f1d1d)
- Severity badge: Bright red (#fecaca), Dark text
- Confidence bar: Green gradient (#16a34a → #059669)
- Weather widget: Blue gradient (#87ceeb → #4da6d6)
- Info cards: Light green background
- Button: Dark green

**Animations**:
- Cards fade in as page loads (staggered)
- Confidence bar animates from 0% to 94% (500ms ease)

---

## SCREEN 4: TREATMENT PROTOCOL
```
┌─────────────────────────────────┐
│ ← [Back]  TREATMENT PROTOCOL    │  ← Header
├─────────────────────────────────┤
│                                 │
│ FOR EARLY BLIGHT                │  ← Section title
│                                 │
│ ┌───────────────────────────────┐│
│ │ #1 Recommended  94% Effective │  ← Green card (selected)
│ │                               │
│ │ Mancozeb 75% WP               │  ← Product name (bold)
│ │                               │
│ │ Dosage per Acre               │  ← Dosage section
│ │ 2.5 kg per acre               │
│ │                               │
│ │ Application Timing            │  ← Timing section
│ │ Apply today evening (6 PM)    │
│ │                               │
│ │ Why This Treatment?           │  ← Explanation
│ │ High humidity (78%) creates   │
│ │ ideal conditions. Mancozeb    │
│ │ acts as preventive barrier.   │
│ └───────────────────────────────┘│
│                                 │
│ LISTEN IN YOUR LANGUAGE         │  ← Voice explanation section
│                                 │
│ [🔊 KANNADA] [🔊 TELUGU]        │  ← 2×2 grid
│ [🔊 ENGLISH] [🔊 HINDI]         │
│                                 │
│ Playing treatment instructions  │  ← Voice playing indicator
│ in Kannada... 🔊                │
│                                 │
│ ALTERNATIVE TREATMENTS          │  ← Alternative options
│                                 │
│ #2 Chlorothalonil 75% WP        │  ← Alternative card 1
│ 💊 1.5 L per acre               │
│ ⏰ Apply tomorrow morning        │
│                                 │
│ #3 Copper Fungicide (Bordeaux)  │  ← Alternative card 2
│ 💊 1% solution, 500L per acre   │
│ ⏰ Apply day after tomorrow      │
│                                 │
│ APPLICATION INSTRUCTIONS        │  ← Instructions section
│                                 │
│ Before Spraying:                │
│ • Wear protective gear          │
│ • Ensure no rain within 6h      │
│ • Spray early morning/evening   │
│ • Mix with adequate water       │
│                                 │
│ After Spraying:                 │
│ • Keep area sealed for 6h       │
│ • Don't allow livestock         │
│ • Repeat after 7-10 days        │
│ • Monitor plant recovery        │
│                                 │
├─────────────────────────────────┤
│ [📍 FIND MEDICINE NEAR ME]      │  ← CTA with icon
└─────────────────────────────────┘
```

**Color Scheme**:
- Selected treatment: Green highlight (#f0fdf4), Green border
- Alternative treatments: Light gray background
- Voice buttons: Gradient purple (#667eea → #764ba2)
- Voice playing: Purple background with animation
- Icon colors: Matching functionality (💊=medicine, ⏰=timing)
- CTA: Dark green with white text

**Interactive States**:
- Click alternative treatment → Changes selection highlight
- Click language button → Plays voice (shows loading animation)
- During voice playback → Button shows spinner, plays for 3s

---

## SCREEN 5: SHOP LOCATOR (STOCKPING INTEGRATION)
```
┌─────────────────────────────────┐
│ ← [Back]  FIND MEDICINE         │  ← Header
├─────────────────────────────────┤
│                                 │
│ ┌───────────────────────────────┐│
│ │ Searching for: Mancozeb 75%  ││  ← Search info card
│ │ 📍 Within 10km • Updated 2min ││
│ └───────────────────────────────┘│
│                                 │
│ NEARBY SHOPS WITH STOCK         │  ← Section title
│                                 │
│ ┌───────────────────────────────┐│
│ │ Kisan Krushi Kendra ✓         │  ← Shop #1 (Best match)
│ │ 📍 Main Market, Bangalore    │ │
│ │                       [2.3km]│ │  ← Distance badge (green)
│ │                               │
│ │ ✓ 15 units in stock          │  ← Stock status (green)
│ │                               │
│ │ Price: ₹450/kg               │  ← Pricing
│ │ 💰 ₹1,125 per acre           │
│ │                               │
│ │ ⭐ 4.7 (234 reviews)          │  ← Rating & hours
│ │ ⏱️ 6 AM - 8 PM               │
│ │                               │
│ │ ⏱️ 12 mins ETA               │  ← ETA badge
│ │ [☎️ CALL] [🧭 NAVIGATE]     │  ← Action buttons
│ └───────────────────────────────┘│
│                                 │
│ ┌───────────────────────────────┐│
│ │ Agri Supply Hub ✓            │ │  ← Shop #2
│ │ 📍 Whitefield, Bangalore    │ │
│ │                       [3.8km]│ │
│ │                               │
│ │ ⚠️ 8 units - Limited Stock   │
│ │ Price: ₹480/kg | ₹1,200/acre│
│ │ ⭐ 4.5 (156 reviews)          │
│ │ ⏱️ 7 AM - 7 PM | 18 mins    │
│ │ [☎️ CALL] [🧭 NAVIGATE]     │
│ └───────────────────────────────┘│
│                                 │
│ ┌───────────────────────────────┐│
│ │ Farmer's Market Store        │ │  ← Shop #3 (Cheapest)
│ │ 📍 Indiranagar, Bangalore  │ │
│ │                       [4.1km]│ │
│ │                               │
│ │ ✓ 22 units in stock          │
│ │ 💰 ₹420/kg | ₹1,050/acre    │  ← Best price
│ │ ⭐ 4.3 (89 reviews)           │
│ │ ⏱️ 8 AM - 6 PM | 21 mins    │
│ │ [☎️ CALL] [🧭 NAVIGATE]     │
│ └───────────────────────────────┘│
│                                 │
│ SHOP DETAILS (SELECTED)         │  ← Expanded view
│                                 │
│ Product Details                 │
│ Mancozeb 75% WP                 │
│ Formulation: 75% WP             │
│ Available: 15 units             │
│                                 │
│ Location & Contact              │
│ Main Market, Bangalore          │
│ Phone: +91-9876543210          │
│ Hours: 6 AM - 8 PM              │
│                                 │
│ TOTAL COST FOR YOUR FARM        │
│     ₹1,125                      │  ← Big, bold price
│                                 │
│ NEXT STEPS                      │  ← Process timeline
│ 1. Call shop to confirm         │
│ 2. Travel to shop (~12 mins)    │
│ 3. Purchase Mancozeb            │
│ 4. Apply treatment              │
│ 5. Monitor crop recovery        │
│                                 │
├─────────────────────────────────┤
│ [☎️ CALL KISAN KRUSHI KENDRA]  │  ← Bottom CTA
└─────────────────────────────────┘
```

**Color Scheme**:
- Search banner: Light green (#e0f7e8)
- Shop cards: White with subtle border
- Selected shop: Green highlight, darker border
- Distance badges: Green (#dcfce7)
- Stock status: Green background (#f0fdf4)
- Price highlight: Orange (#d97706)
- Limited stock: Yellow warning
- Rating: Gold stars (⭐)
- Action buttons: Border + hover effect
- CTA: Solid dark green

**Interactions**:
- Tap shop card → Selects it (highlight + details update below)
- Tap Call button → Alert with phone number
- Tap Navigate button → Opens Google Maps
- Swipe left/right → Scroll between shops

---

## 🎨 Typography & Spacing Reference

### **Font Sizes & Weights**
```
H1 (Screen titles): 20px, 700 weight, #2d5016
H2 (Section titles): 16px, 700 weight, #111
H3 (Card titles): 15px, 600 weight, #111
Body text: 13px, 400 weight, #666
Small text: 12px, 400 weight, #999
Badge text: 12px, 600 weight, variable color

Button text: 16px, 600 weight, white/green
```

### **Spacing Grid** (8px baseline)
```
Section gaps: 16px (2x)
Card margin: 12px (1.5x)
Card padding: 14-16px (1.75-2x)
Button padding: 12-14px (1.5-1.75x)
Icon margin: 8px (1x)
Line height: 1.4-1.6
```

---

## 🌈 Complete Color Palette

```javascript
const colors = {
  // Primary Green (Agricultural)
  darkGreen: '#2d5016',      // Primary action, text
  lightGreen: '#f0fdf4',     // Backgrounds, hover states
  
  // Status Colors
  success: '#16a34a',        // Stock available
  warning: '#d97706',        // Timing, pricing
  error: '#991b1b',          // High severity
  info: '#667eea',           // Voice/AI features
  
  // Gradients
  headerGradient: 'linear-gradient(135deg, #2d5016 0%, #3d7024 100%)',
  weatherGradient: 'linear-gradient(135deg, #87ceeb 0%, #4da6d6 100%)',
  voiceGradient: 'linear-gradient(135deg, #667eea 0%, #764ba2 100%)',
  diseaseGradient: 'linear-gradient(135deg, #fee2e2 0%, #fecaca 100%)',
  
  // Text
  textDark: '#111111',       // Primary text
  textMedium: '#666666',     // Secondary text
  textLight: '#999999',      // Tertiary text
  
  // UI Elements
  border: '#e5e7eb',         // Card borders
  divider: '#f5f5f5',        // Section dividers
  white: '#ffffff'           // Backgrounds
}
```

---

## 📐 Responsive Breakpoints

```css
/* Mobile (Primary) */
@media (max-width: 480px) {
  .app-container { max-width: 100%; }
  .card { padding: 12px; }
  .btn { padding: 12px 16px; font-size: 15px; }
}

/* Small Tablet */
@media (481px to 768px) {
  .app-container { max-width: 480px; margin: 0 auto; }
  .card { padding: 16px; }
  .btn { padding: 14px 20px; font-size: 16px; }
}

/* Desktop */
@media (769px+) {
  .app-container { max-width: 480px; margin: 0 auto; }
  /* No layout changes, app stays centered mobile size */
}
```

---

## 🎬 Animation Specifications

### **Screen Transitions** (300ms)
```css
From opacity: 0, translateX(100%)
To opacity: 1, translateX(0)
Easing: ease-out
```

### **Card Reveals** (500ms, staggered)
```css
From opacity: 0
To opacity: 1
Easing: ease-out
Delay: 100ms per card
```

### **Button Hover** (200ms)
```css
Transform: translateY(-2px)
Box-shadow: 0 4px 12px rgba(45, 80, 22, 0.3)
```

### **Loading Spinner** (800ms, infinite)
```css
Transform: rotate(0deg) → rotate(360deg)
Border: 3px solid #f3f4f6
Border-top: 3px solid #2d5016
```

### **Voice Playing** (Pulse, 1s)
```css
Scale: 1 → 1.05 → 1
Opacity: 0.7 → 1 → 0.7
```

---

## 📊 Visual Hierarchy

**Most Important** (Largest, Brightest)
1. Disease name + Severity badge
2. Confidence/Status metrics
3. Primary CTA buttons
4. Treatment product name
5. Pricing information

**Important** (Medium)
6. Weather widgets
7. Shop distance badges
8. Stock status
9. Alternative options
10. Additional details

**Supporting** (Smallest, Dimmest)
11. Labels & descriptions
12. Footer information
13. Placeholder text

---

## ✅ Accessibility Compliance

**WCAG 2.1 AA Standards**:
- ✓ Color contrast ratio ≥ 4.5:1 for normal text
- ✓ Large button targets (min 44×44px)
- ✓ Focus indicators on interactive elements
- ✓ Proper heading hierarchy (H1 → H4)
- ✓ Alt text for icons/emojis
- ✓ Readable font sizes (min 12px)
- ✓ Sufficient line height (1.4-1.6)
- ✓ Not relying on color alone for information
- ✓ Clear form labels
- ✓ Error messages in plain language

---

**This complete mockup guide ensures pixel-perfect consistency across all screens and states. Use this as reference for both frontend implementation and QA testing.**
