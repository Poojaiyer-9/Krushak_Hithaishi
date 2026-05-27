# Krushak Hithaishi - Deployment & Integration Guide

## 🚀 Quick Start

### 1. **Development Environment Setup**

```bash
# Clone or navigate to project
cd "C:\Users\Hp\OneDrive\Desktop\Krushak hithaishi"

# Install dependencies
npm install

# Start development server
npm run dev
```

**Expected Output**:
```
✓ vite v5.4.21 ready in 2149 ms
✓ Local: http://localhost:3000/
✓ Network: use --host to expose
```

### 2. **Build for Production**

```bash
# Create optimized build
npm run build

# Preview production build locally
npm run preview
```

**Output**: Optimized files in `dist/` folder (~200KB gzipped)

---

## 📱 Platform Deployment Options

### **Option 1: Vercel (Recommended - Zero Config)**

```bash
# Install Vercel CLI
npm install -g vercel

# Deploy
vercel

# Set environment: Production
# Auto-generated URL: https://krushak-hithaishi.vercel.app
```

**Advantages**:
- ✅ Automatic deployments on git push
- ✅ Free SSL certificates
- ✅ Global CDN
- ✅ Preview URLs for testing
- ✅ Integrates with GitHub/GitLab/Bitbucket

---

### **Option 2: Netlify**

```bash
# Install Netlify CLI
npm install -g netlify-cli

# Login and connect
netlify login

# Deploy
netlify deploy --prod --dir=dist
```

**Advantages**:
- ✅ Form handling built-in
- ✅ Serverless functions support
- ✅ Analytics & monitoring
- ✅ Easy branch deployments

---

### **Option 3: Docker Container**

Create `Dockerfile`:
```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

RUN npm run build

EXPOSE 3000

CMD ["npm", "run", "preview"]
```

Build & run:
```bash
docker build -t krushak-hithaishi .
docker run -p 3000:3000 krushak-hithaishi
```

---

### **Option 4: AWS S3 + CloudFront**

```bash
# Build the app
npm run build

# Upload to S3
aws s3 cp dist/ s3://krushak-hithaishi-prod --recursive

# Create CloudFront distribution pointing to S3
aws cloudfront create-distribution --origin-domain-name krushak-hithaishi-prod.s3.amazonaws.com
```

---

## 🔌 Backend API Integration

### **Current Setup (Mock Data)**

The app currently uses hardcoded mock data in `App.jsx`:

```javascript
const mockDetectionData = {
  disease: 'Early Blight',
  confidence: 0.94,
  severity: 'High',
  // ... mock data
}
```

### **To Connect Real APIs**

#### **Step 1: Disease Detection API**

**Modify** `src/App.jsx` in `handleCaptureImage()`:

```javascript
const handleCaptureImage = async (imagePath) => {
  // Create FormData with image and context
  const formData = new FormData();
  formData.append('image', imageFile);
  formData.append('weather', JSON.stringify({
    temperature: 24,
    humidity: 78,
    rainfall: 3.5
  }));
  formData.append('cropStage', 'Flowering');
  formData.append('soilMoisture', 68);

  // Call your detection API
  const response = await fetch('/api/detection', {
    method: 'POST',
    body: formData
  });

  const data = await response.json();
  setDetectionData(data);
  setCurrentScreen('detection');
}
```

**Expected Response**:
```json
{
  "disease": "Early Blight",
  "confidence": 0.94,
  "severity": "High",
  "affectedArea": "35%",
  "weather": {
    "temperature": 24,
    "humidity": 78,
    "rainfall": 3.5,
    "condition": "Cloudy"
  },
  "cropStage": "Flowering",
  "soilMoisture": 68,
  "recommendations": [
    {
      "rank": 1,
      "name": "Mancozeb 75% WP",
      "dosage": "2.5 kg per acre",
      "timing": "Apply today evening (6 PM)",
      "reason": "High humidity creates ideal fungal growth...",
      "confidence": 0.94
    },
    // ... more recommendations
  ]
}
```

---

#### **Step 2: Stockping Shop Finder Integration**

**Modify** `src/screens/ShopsScreen.jsx`:

```javascript
useEffect(() => {
  const fetchShops = async () => {
    const response = await fetch('/api/shops', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        medicine: data.recommendations[0].name,
        formulation: '75% WP',
        quantity: 2.5,
        latitude: userLocation.lat,
        longitude: userLocation.lng,
        radius: 10 // km
      })
    });

    const shopData = await response.json();
    setShops(shopData);
  };

  fetchShops();
}, [data]);
```

**Expected Response**:
```json
[
  {
    "id": 1,
    "name": "Kisan Krushi Kendra",
    "distance": "2.3 km",
    "address": "Main Market, Bangalore",
    "phone": "+91-9876543210",
    "stock": 15,
    "formulation": "75% WP",
    "price": "450",
    "pricePerAcre": "1125",
    "availability": "In Stock",
    "rating": 4.7,
    "reviews": 234,
    "hours": "6 AM - 8 PM",
    "eta": "12",
    "verified": true,
    "latitude": 12.9716,
    "longitude": 77.5946,
    "navigationUrl": "https://maps.google.com/..."
  }
]
```

---

### **Open-Meteo Weather API (Free, No Auth Required)**

```javascript
// In App.jsx or a weather service
const getWeatherData = async (latitude, longitude) => {
  const response = await fetch(
    `https://api.open-meteo.com/v1/forecast?` +
    `latitude=${latitude}&longitude=${longitude}&` +
    `current=temperature_2m,relative_humidity_2m,precipitation,weather_code`
  );

  const data = await response.json();
  
  return {
    temperature: data.current.temperature_2m,
    humidity: data.current.relative_humidity_2m,
    rainfall: data.current.precipitation,
    condition: getWeatherCondition(data.current.weather_code)
  };
}
```

---

### **NASA POWER Soil Moisture API (Free, No Auth Required)**

```javascript
// In App.jsx or a soil service
const getSoilMoisture = async (latitude, longitude) => {
  const response = await fetch(
    `https://power.larc.nasa.gov/api/v1/resources/MOD16A2_105/query?` +
    `latitude=${latitude}&longitude=${longitude}&` +
    `start=20260527&end=20260527&format=json`
  );

  const data = await response.json();
  return data.properties.qs.values[0][1]; // Soil moisture percentage
}
```

---

## 🎙️ Voice Explanation Integration (gTTS + IndicTrans2)

### **Backend Service Setup** (Node.js + Express)

```javascript
// backend/routes/voice.js
const express = require('express');
const router = express.Router();
const gTTS = require('gtts');
const axios = require('axios');

router.post('/explain', async (req, res) => {
  const { treatment, language } = req.body;

  // Step 1: Translate to target language using IndicTrans2 API
  const translatedText = await translateText(treatment, language);

  // Step 2: Generate speech using gTTS
  const gtts = new gTTS({
    text: translatedText,
    lang: language, // 'kn', 'te', 'hi', 'en'
    slow: false
  });

  // Stream audio to client
  res.setHeader('Content-Type', 'audio/mpeg');
  gtts.stream().pipe(res);
});

async function translateText(text, targetLang) {
  const response = await axios.post(
    'https://api.indictrans.ai/translate',
    {
      text: text,
      source: 'en',
      target: targetLang
    }
  );
  return response.data.translated_text;
}

module.exports = router;
```

### **Frontend Voice Player**

**Already implemented** in `TreatmentScreen.jsx`:

```javascript
const handlePlayVoice = async (lang) => {
  setPlayingVoice(lang);
  
  const response = await fetch('/api/voice/explain', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      treatment: currentTreatment.name,
      dosage: currentTreatment.dosage,
      timing: currentTreatment.timing,
      reason: currentTreatment.reason,
      language: lang
    })
  });

  const audioBlob = await response.blob();
  const audioUrl = URL.createObjectURL(audioBlob);
  const audio = new Audio(audioUrl);
  audio.play();

  audio.onended = () => setPlayingVoice(null);
}
```

---

## 🔐 Environment Variables

Create `.env.local` in project root:

```env
# API Endpoints
VITE_DISEASE_API=https://api.yourdomain.com/detection
VITE_SHOP_API=https://api.yourdomain.com/shops
VITE_VOICE_API=https://api.yourdomain.com/voice

# Third-party APIs (if needed)
VITE_OPEN_METEO_KEY=
VITE_GOOGLE_MAPS_KEY=YOUR_MAPS_API_KEY
VITE_STOCKPING_API_KEY=YOUR_STOCKPING_KEY

# Analytics
VITE_ANALYTICS_ID=G-XXXXXXXXXXXXX

# Environment
VITE_ENVIRONMENT=development
```

**Usage in code**:
```javascript
const API_URL = import.meta.env.VITE_DISEASE_API;
const MAPS_KEY = import.meta.env.VITE_GOOGLE_MAPS_KEY;
```

---

## 📊 Performance Optimization

### **Build Analysis**

```bash
# Analyze bundle size
npm install -D @vite-plugin-visualizer/plugin
```

**vite.config.js**:
```javascript
import { visualizer } from '@vite-plugin-visualizer/plugin'

export default {
  plugins: [visualizer()]
}
```

### **Lighthouse Scores Target**

| Metric | Target | Current |
|--------|--------|---------|
| Performance | >90 | Expected: 95+ |
| Accessibility | >90 | Expected: 98+ |
| Best Practices | >90 | Expected: 100 |
| SEO | >90 | Expected: 95+ |

### **Optimization Checklist**

- [x] Code splitting by routes
- [x] CSS minification
- [x] Image optimization placeholders
- [x] Lazy loading for screens
- [x] CSS animations (GPU accelerated)
- [ ] Service workers for offline
- [ ] Image compression with WebP
- [ ] GZIP/Brotli compression (server)

---

## 🧪 Testing Checklist

### **Functional Testing**

```bash
# Manual tests (since no test framework set up)
- [ ] Home screen renders correctly
- [ ] Camera screen captures image/file upload
- [ ] Disease detection displays results
- [ ] Treatment screen shows all 3 options
- [ ] Voice buttons trigger audio playback
- [ ] Shop list updates dynamically
- [ ] Phone/navigation buttons work
- [ ] Back navigation between screens works
- [ ] Responsive design on mobile (375px, 480px)
- [ ] Responsive design on tablet (768px)
```

### **Automated Testing Setup (Optional)**

```bash
npm install -D vitest @testing-library/react

# Add to package.json
"scripts": {
  "test": "vitest"
}
```

---

## 📲 Progressive Web App (PWA) Setup

Create `public/manifest.json`:

```json
{
  "name": "Krushak Hithaishi - Disease Detection for Farmers",
  "short_name": "Krushak Hithaishi",
  "description": "AI-powered crop disease detection with real-time treatment and medicine procurement",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#2d5016",
  "icons": [
    {
      "src": "/icon-192.png",
      "sizes": "192x192",
      "type": "image/png",
      "purpose": "any"
    },
    {
      "src": "/icon-512.png",
      "sizes": "512x512",
      "type": "image/png",
      "purpose": "any"
    }
  ]
}
```

**index.html**:
```html
<link rel="manifest" href="/manifest.json">
<meta name="theme-color" content="#2d5016">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
```

---

## 🔄 CI/CD Pipeline

### **GitHub Actions Workflow** (.github/workflows/deploy.yml)

```yaml
name: Deploy to Vercel

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
      
      - run: npm install
      - run: npm run build
      
      - uses: vercel/action@v4
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          vercel-args: '--prod'
```

---

## 📊 Analytics & Monitoring

### **Google Analytics Integration**

```bash
npm install gtag
```

**src/main.jsx**:
```javascript
import gtag from 'gtag'

gtag.initialize('G-XXXXXXXXXXXXX')

// Track page views
gtag.pageview({
  page_path: currentScreen,
  page_title: `Krushak - ${currentScreen}`
})
```

### **Error Tracking (Sentry)**

```bash
npm install @sentry/react
```

```javascript
import * as Sentry from "@sentry/react"

Sentry.init({
  dsn: "YOUR_SENTRY_DSN",
  environment: "production"
})
```

---

## 🎯 Success Metrics to Track

1. **Conversion Funnel**
   - Home → Camera: % completing
   - Camera → Detection: Detection success rate
   - Detection → Treatment: User engagement
   - Treatment → Shops: Medicine purchase intent

2. **Performance Metrics**
   - Time to detection: <8s
   - App load time: <2s
   - Screen transition lag: <300ms

3. **User Engagement**
   - Voice explanation usage: % tapping language buttons
   - Shop finder usage: % viewing shops
   - Call-to-action clicks: % proceeding to call

4. **Error Tracking**
   - API failures
   - Image upload errors
   - Navigation errors

---

## 🚀 Launch Checklist

- [ ] All environment variables set
- [ ] Backend APIs tested and documented
- [ ] Disease model integrated and tested
- [ ] Stockping API integration verified
- [ ] Weather API working
- [ ] Voice generation tested
- [ ] Push notifications configured
- [ ] Analytics tracking enabled
- [ ] Error monitoring enabled
- [ ] SEO meta tags added
- [ ] Social media share preview set
- [ ] Privacy policy & Terms of Service created
- [ ] GDPR compliance (if applicable)
- [ ] Security headers configured
- [ ] Rate limiting enabled
- [ ] Load testing completed
- [ ] Browser compatibility tested
- [ ] Accessibility audit passed
- [ ] Lighthouse scores >90
- [ ] Staging deployment verified
- [ ] Production deployment successful
- [ ] Monitoring & alerting active

---

## 📞 Support & Maintenance

### **Common Issues**

**Issue**: Browser can't connect to localhost:3000
```bash
# Solution: Check if port is in use
netstat -ano | findstr :3000
# Kill the process
taskkill /PID <PID> /F
```

**Issue**: npm install fails
```bash
# Solution: Clear npm cache
npm cache clean --force
npm install
```

**Issue**: Build is too large
```bash
# Solution: Analyze bundle
npm run build -- --analyze
```

---

## 📚 Additional Resources

- [Vite Documentation](https://vitejs.dev/)
- [React Hooks Guide](https://react.dev/reference/react)
- [Lucide Icons](https://lucide.dev/)
- [Open-Meteo API](https://open-meteo.com/)
- [Stockping API](https://www.stockping.com/api)
- [Google Maps JavaScript API](https://developers.google.com/maps/documentation/javascript)

---

**Built with 💚 for sustainable agriculture & farmer empowerment**
