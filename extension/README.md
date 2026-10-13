<div align="center">

<img src="../docs/logo.svg" alt="MindSteady logo" width="96" height="96">

</div>

# MindSteady Chrome Extension

A powerful Chrome extension that provides real-time video content safety monitoring and parental controls across all websites.

## 🎯 Overview

The MindSteady Chrome Extension acts as the frontend client in the MindSteady ecosystem, intercepting video elements on web pages and applying AI-powered safety measures in real-time. It seamlessly integrates with the MindSteady backend API to provide comprehensive content analysis and protection.

## ✨ Features

### 🔍 **Automatic Video Detection**
- Detects all `<video>` elements across any website
- Monitors dynamically loaded content (AJAX, SPA frameworks)
- Handles iframe-embedded videos (where permissions allow)
- Periodic scanning every 5 seconds for missed content

### 🛡️ **Real-time Safety Controls**
- **Playback Speed Reduction**: Automatically slows down intense content
- **Visual Filters**: Applies tone-down, blur, and grayscale filters
- **Content Warnings**: Shows alert dialogs for inappropriate content
- **Skip Controls**: Allows users to continue or skip flagged videos

### ⚙️ **User Interface & Controls**
- Intuitive popup interface with comprehensive settings
- Real-time statistics (videos detected, analyzed, warnings)
- API configuration and connection testing
- Enable/disable toggle with visual status indicators

### 🔧 **Advanced Configuration**
- Strict mode for enhanced protection
- Adjustable filter strength (Light/Medium/Strong)
- Custom API endpoint configuration
- Settings persistence across browser sessions

## 🚀 Installation

### Option 1: Development Installation
1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   cd mindsteady/extension
   ```

2. **Open Chrome Extensions**:
   - Navigate to `chrome://extensions/`
   - Enable "Developer mode" (top-right toggle)

3. **Load Extension**:
   - Click "Load unpacked"
   - Select the `extension` folder
   - Extension will appear in your browser toolbar

### Option 2: Chrome Web Store (Coming Soon)
- Install directly from Chrome Web Store
- Automatic updates and enhanced security

## 🧪 Testing & Demo

### Quick Test
1. **Load Test Page**: Open `extension/test-page.html` in Chrome
2. **Open Controls**: Click MindSteady icon in toolbar
3. **Play Videos**: Test different safety behaviors:
   - **Video 1**: Normal playback (safe content)
   - **Video 2**: Reduced speed + filters (moderate content)  
   - **Video 3**: Warning dialog + pause (risky content)
4. **Check Console**: View debug messages (F12)

### Real-world Testing
- Visit YouTube, Vimeo, news sites, social media
- Monitor extension popup for detection statistics
- Observe safety measures applied to different content types

## 🔧 Configuration

### Extension Popup Settings
- **Protection Toggle**: Enable/disable content monitoring
- **Strict Mode**: Enhanced sensitivity for family environments
- **Filter Strength**: Adjust visual filter intensity
- **Warnings**: Enable/disable alert dialogs
- **API Endpoint**: Configure backend server URL

### Advanced Configuration
Edit `extension/background.js` for advanced customization:
```javascript
// Default API endpoint
this.apiEndpoint = 'https://your-api-server.com/analyze';

// Analysis sensitivity
const riskyPatterns = ['violent', 'scary', 'mature'];
const moderatePatterns = ['action', 'intense', 'fast'];
```

## 🛠️ Development

### Project Structure
```
extension/
├── manifest.json       # Extension configuration
├── src/
│   ├── content.js     # Video detection & manipulation
│   ├── background.js  # API communication service worker
│   ├── popup.html     # Extension popup interface
│   ├── popup.js       # Popup functionality
│   └── styles.css     # UI styling
├── icons/             # Extension icons
├── test-page.html     # Demo/testing page
└── README.md          # This file
```

### Key Components

#### Content Script (`content.js`)
- Injected into all web pages
- Detects and intercepts video elements
- Applies safety measures (speed, filters, warnings)
- Communicates with background script

#### Background Script (`background.js`)
- Service worker for Manifest V3 compliance
- Handles API communication with backend
- Manages settings and preferences
- Provides mock API responses for development

#### Popup Interface (`popup.html/js`)
- User control panel and settings
- Real-time statistics display
- API configuration and testing
- Extension status monitoring

### Development Commands
```bash
# Install dependencies (if any)
npm install

# Run linting
npm run lint

# Build for production
npm run build

# Package for Chrome Web Store
npm run package
```

## 🔌 API Integration

### Backend Communication
The extension communicates with the MindSteady Django backend via REST API:

```javascript
// Request format
{
  "videoData": {
    "src": "video_url",
    "duration": 120,
    "videoWidth": 1920,
    "videoHeight": 1080,
    "url": "page_url", 
    "title": "page_title"
  },
  "timestamp": 1640995200000
}

// Response format
{
  "safetyLevel": "safe|moderate|risky",
  "confidence": 0.85,
  "actions": {
    "reduceSpeed": true,
    "speedFactor": 0.75,
    "applyFilters": true,
    "filters": ["tone-down"],
    "showWarning": false,
    "warningMessage": "Custom message"
  }
}
```

### Mock API Mode
For development without backend:
- Built-in mock responses based on URL patterns
- Simulates realistic analysis delays
- Configurable trigger patterns for testing

## 🎨 UI Components

### Extension Popup
- **Header**: Logo, status indicator
- **Controls**: Toggle switches, dropdowns
- **Statistics**: Video counts, analysis results
- **API Config**: Endpoint settings, connection test
- **Actions**: Refresh page, advanced settings

### Content Overlays
- **Warning Dialogs**: Native browser alerts
- **Visual Filters**: CSS filter effects applied to videos
- **Speed Controls**: Automatic playback rate adjustment

## 📊 Analytics & Monitoring

### Usage Statistics
- Videos detected per session
- Safety measures applied
- User interactions with warnings
- API response times and errors

### Debug Information
- Console logging with `MindSteady:` prefix
- Extension popup statistics
- Background script status messages
- API communication logs

## 🔒 Privacy & Security

### Data Handling
- Only video metadata sent to API (no actual video content)
- Local storage for user preferences
- No tracking or personal data collection
- HTTPS-only API communication

### Permissions
- `activeTab`: Access current webpage for video detection
- `scripting`: Inject content scripts
- `storage`: Save user settings
- `host_permissions`: Monitor videos across all sites

## 🐛 Troubleshooting

### Common Issues

**Extension not detecting videos:**
- Check if extension is enabled in popup
- Verify content script injection in console
- Try refreshing the page

**API connection errors:**
- Test API endpoint in popup settings
- Check network connectivity
- Verify CORS configuration on backend

**Videos not being analyzed:**
- Check console for JavaScript errors
- Ensure backend server is running
- Verify API response format

### Debug Mode
Enable verbose logging:
```javascript
// In background.js
const DEBUG_MODE = true;
```

## 🚢 Deployment

### Chrome Web Store Submission
1. **Build Production Package**:
   ```bash
   npm run build
   zip -r mindsteady-extension.zip extension/
   ```

2. **Prepare Store Assets**:
   - Extension icons (16x16, 32x32, 48x48, 128x128)
   - Screenshots and promotional images
   - Store description and privacy policy

3. **Submit for Review**:
   - Upload to Chrome Developer Dashboard
   - Complete store listing information
   - Submit for Google review process

### Updates & Versioning
- Update `manifest.json` version number
- Follow semantic versioning (e.g., 1.2.3)
- Test thoroughly before submission

## 🤝 Contributing

### Development Setup
1. Fork repository and create feature branch
2. Make changes following code standards
3. Test with both mock and real API
4. Submit pull request with detailed description

### Code Standards
- ESLint configuration for JavaScript
- Prettier formatting for consistent style
- JSDoc comments for functions
- Console logging with consistent prefixes

## 📄 License

MIT License - see [LICENSE](../LICENSE) file for details.

---

**Parent Project**: [MindSteady Platform](../README.md)  
**Related**: [Backend API](../backend/README.md) | [SDK Agent](../sdk-agent/README.md)