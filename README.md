<div align="center">

<img src="docs/logo.svg" alt="MindSteady logo" width="120" height="120">

# MindSteady

**AI-Powered Video Content Safety Platform**

Keeping children safe online — one video at a time.

</div>

---

## 🎯 Overview

MindSteady is a comprehensive video content safety platform that analyzes video content in real time and applies gentle, automatic protections for children. It combines a browser extension, an AI-powered backend, and an agent toolkit that work together to detect video content, score its safety, and respond with calming measures such as slower playback, softer visuals, and clear warnings.

## 🏗️ Project Structure

This is a monorepo containing three interconnected components:

```
mindsteady/
├── extension/          # Chrome Extension - frontend client
├── backend/            # Django API - content analysis service
├── shieldagent/        # ADK agent toolkit - analysis pipeline
└── docs/               # Branding and documentation assets
```

### 🔧 Components Overview

| Component | Technology | Purpose | Status |
|-----------|------------|---------|--------|
| **Chrome Extension** | JavaScript, HTML, CSS | Browser-based video interception and safety controls | ✅ Complete |
| **Backend API** | Django, Python, AI/ML | Video content analysis and safety scoring | 🚧 In Development |
| **Shield Agent** | Python, Google ADK | Multi-agent analysis pipeline for content safety | 🚧 In Development |

---

## 🚀 Quick Start

### Prerequisites

- Node.js 16+
- Python 3.8+
- Chrome Browser
- Git

### 1. Clone Repository

```bash
git clone <repository-url>
cd mindsteady
```

### 2. Set Up Chrome Extension

```bash
cd extension
# Follow extension/README.md for installation
```

### 3. Set Up Backend API

```bash
cd backend
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver
# Follow backend/README.md for detailed setup
```

### 4. Set Up Shield Agent

```bash
cd shieldagent
# Follow shieldagent setup notes for installation
```

---

## 📚 Component Documentation

### [Chrome Extension](./extension/README.md)

Browser extension that intercepts video elements on web pages and applies safety measures in real time.

**Key Features:**

- Automatic video detection across all websites
- Real-time content analysis integration
- Playback speed control and visual filters
- Parental warning system with user controls
- Comprehensive settings and monitoring dashboard

### [Backend API](./backend/README.md)

Django-based REST API that provides AI-powered video content analysis and safety scoring.

**Key Features:**

- Video content analysis using ML models
- Safety level classification (safe/moderate/risky)
- RESTful API with authentication
- Database storage for analysis results
- Scalable deployment architecture

### [Shield Agent](./shieldagent/)

ADK-based agent toolkit that enables third-party platforms to incorporate MindSteady functionality.

**Key Features:**

- Parallel multi-agent content analysis
- Playback speed, color contrast, and content appropriateness checks
- Structured JSON recommendations
- Easy integration APIs for web platforms

---

## 🔄 System Architecture

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│  Chrome         │    │  Backend API    │    │  Shield Agent   │
│  Extension      │◄──►│  (Django)       │◄──►│  (Integration)  │
│                 │    │                 │    │                 │
│ • Video Detection│   │ • Content Analysis│  │ • Platform APIs │
│ • Safety Controls│   │ • ML Models     │    │ • Custom Policies│
│ • User Interface │   │ • Database      │    │ • Analytics     │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

---

## 🛠️ Development Workflow

### Setting Up Development Environment

```bash
# Install all dependencies
npm run install-all

# Start all services in development mode
npm run dev

# Run tests across all components
npm run test

# Build for production
npm run build
```

### Code Standards

- **JavaScript**: ESLint + Prettier configuration
- **Python**: Black formatter + Flake8 linting
- **Git**: Conventional commit messages
- **Testing**: Unit tests required for all components

---

## 🚢 Deployment

### Chrome Extension

1. Build extension package
2. Submit to Chrome Web Store
3. Configure API endpoints for production

### Backend API

1. Deploy to cloud provider (AWS/GCP/Azure)
2. Set up database and ML model services
3. Configure authentication and rate limiting

### Shield Agent

1. Package and publish to npm/PyPI
2. Generate API documentation
3. Provide integration examples

---

## 📊 Monitoring & Analytics

- **Extension Usage**: User engagement and safety interventions
- **API Performance**: Response times and analysis accuracy
- **Content Analysis**: Safety trend analysis and model improvements
- **Error Tracking**: Comprehensive logging and alerting

---

## 🤝 Contributing

1. Fork the repository
2. Create feature branch (`git checkout -b feature/amazing-feature`)
3. Follow component-specific development guides
4. Run tests and ensure code quality
5. Submit pull request with detailed description

See individual component READMEs for specific contribution guidelines.

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🆘 Support

- **Documentation**: Check component-specific READMEs
- **Issues**: Create GitHub issues for bugs and feature requests
- **Community**: Join our Discord/Slack for discussions
- **Enterprise**: Contact team for business inquiries

---

<div align="center">

*Building a safer digital environment for children, one video at a time.* 🛡️👶

</div>
