<div align="center">

<img src="../docs/logo.svg" alt="MindSteady logo" width="96" height="96">

</div>

# MindSteady Backend API

Django-based REST API server that provides AI-powered video content analysis and safety scoring for the MindSteady platform.

## 🎯 Overview

The MindSteady Backend is a robust Django application that analyzes video content metadata and provides safety recommendations to client applications. It serves as the intelligence core of the MindSteady ecosystem, utilizing machine learning models to classify content safety levels and recommend appropriate protective measures.

## ✨ Features

### 🧠 **AI-Powered Analysis**
- Video content safety classification using ML models
- Multi-factor analysis (metadata, URL patterns, content signals)
- Confidence scoring for analysis results
- Continuous model improvement through feedback loops

### 🔐 **Enterprise Security**
- API key authentication for client applications
- Rate limiting and abuse prevention
- CORS configuration for web clients
- Comprehensive request/response logging

### 📊 **Data Management**
- PostgreSQL database for scalable storage
- Analysis result caching for performance
- User preference and settings storage
- Analytics and reporting capabilities

### 🚀 **Production Ready**
- Docker containerization for easy deployment
- Health check endpoints for monitoring
- Structured logging with configurable levels
- Environment-based configuration

## 🏗️ Architecture

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Chrome        │    │   Django API    │    │   ML Models     │
│   Extension     │───►│   Server        │───►│   & Services    │
│                 │    │                 │    │                 │
│ • Video Data    │    │ • Analysis API  │    │ • Safety Scoring│
│ • User Settings │    │ • Authentication│    │ • Classification│
│ • Statistics    │    │ • Database      │    │ • Learning      │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

## 🚀 Quick Start

### Prerequisites
- Python 3.8 or higher
- PostgreSQL 12+ (or SQLite for development)
- Redis (optional, for caching)
- Docker (optional, for containerized deployment)

### Local Development Setup

1. **Clone and Navigate**:
   ```bash
   git clone <repository-url>
   cd mindsteady/backend
   ```

2. **Create Virtual Environment**:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Environment Configuration**:
   ```bash
   cp .env.example .env
   # Edit .env with your settings
   ```

5. **Database Setup**:
   ```bash
   python manage.py migrate
   python manage.py createsuperuser
   ```

6. **Run Development Server**:
   ```bash
   python manage.py runserver
   ```

7. **Access API**: Navigate to `http://localhost:8000/api/docs/`

### Docker Setup

1. **Build and Run**:
   ```bash
   docker-compose up --build
   ```

2. **Access API**: Navigate to `http://localhost:8000/api/docs/`

## 📡 API Documentation

### Core Endpoints

#### **POST /api/v1/analyze**
Analyze video content for safety and appropriateness.

**Authentication**: API Key required
**Rate Limit**: 100 requests per minute per key

**Request Body**:
```json
{
  "videoData": {
    "src": "https://example.com/video.mp4",
    "duration": 120.5,
    "videoWidth": 1920,
    "videoHeight": 1080,
    "currentTime": 0,
    "volume": 0.8,
    "playbackRate": 1.0,
    "url": "https://example.com/page",
    "title": "Example Page Title"
  },
  "userId": "optional-user-id",
  "sessionId": "optional-session-id"
}
```

**Response**:
```json
{
  "analysisId": "uuid-string",
  "safetyLevel": "safe|moderate|risky",
  "confidence": 0.85,
  "actions": {
    "reduceSpeed": true,
    "speedFactor": 0.75,
    "applyFilters": true,
    "filters": ["tone-down", "brightness"],
    "showWarning": false,
    "warningMessage": null
  },
  "metadata": {
    "processingTime": 150,
    "modelVersion": "v1.2.0",
    "timestamp": "2025-01-01T12:00:00Z"
  }
}
```

#### **GET /api/v1/health**
Health check endpoint for monitoring.

**Response**:
```json
{
  "status": "healthy",
  "database": "connected",
  "redis": "connected",
  "version": "1.0.0",
  "timestamp": "2025-01-01T12:00:00Z"
}
```

#### **GET /api/v1/stats**
Retrieve analysis statistics (requires authentication).

**Response**:
```json
{
  "totalAnalyses": 10542,
  "safetyBreakdown": {
    "safe": 8234,
    "moderate": 1876,  
    "risky": 432
  },
  "averageProcessingTime": 145,
  "last24Hours": 156
}
```

### Authentication

**API Key Header**:
```
Authorization: Bearer your-api-key-here
```

**Request API Key**:
```bash
curl -X POST http://localhost:8000/api/v1/auth/register \
  -H "Content-Type: application/json" \
  -d '{"name": "My App", "email": "app@example.com"}'
```

### Error Responses

```json
{
  "error": {
    "code": "INVALID_REQUEST",
    "message": "Missing required field: videoData.src",
    "details": {},
    "timestamp": "2025-01-01T12:00:00Z"
  }
}
```

## 🏗️ Project Structure

```
backend/
├── mindsteady/              # Django project root
│   ├── settings/           # Environment-specific settings
│   │   ├── base.py        # Base configuration
│   │   ├── development.py # Development settings
│   │   └── production.py  # Production settings
│   ├── urls.py            # URL routing
│   └── wsgi.py            # WSGI application
├── apps/
│   ├── analysis/          # Video analysis logic
│   │   ├── models.py      # Database models
│   │   ├── serializers.py # API serialization
│   │   ├── views.py       # API endpoints
│   │   └── services.py    # Business logic
│   ├── authentication/    # API key management
│   ├── ml_models/         # Machine learning integration
│   └── monitoring/        # Health checks and metrics
├── requirements/
│   ├── base.txt          # Core dependencies
│   ├── development.txt   # Development tools
│   └── production.txt    # Production requirements
├── docker/
│   ├── Dockerfile        # Container definition
│   └── docker-compose.yml # Multi-service setup
├── docs/
│   └── api.md           # Detailed API documentation
├── tests/               # Test suite
├── manage.py           # Django management script
└── README.md          # This file
```

## 🧠 Machine Learning Integration

### Content Analysis Pipeline

1. **Metadata Extraction**: Parse video metadata and context
2. **Feature Engineering**: Extract relevant safety indicators
3. **Model Inference**: Apply trained safety classification models
4. **Confidence Scoring**: Calculate prediction confidence
5. **Action Mapping**: Translate predictions to safety actions

### Model Management

```python
# Example model integration
from apps.ml_models.services import SafetyClassifier

classifier = SafetyClassifier()
result = classifier.analyze({
    'url_pattern': 'youtube.com',
    'title_keywords': ['action', 'adventure'],
    'duration': 120,
    'metadata': {...}
})
```

### Supported Models
- **URL Pattern Classifier**: Analyzes video source patterns
- **Content Keyword Analyzer**: Processes page titles and descriptions
- **Temporal Analysis**: Considers video duration and timing
- **Ensemble Model**: Combines multiple signals for final decision

## ⚙️ Configuration

### Environment Variables

```bash
# Django Settings
DEBUG=False
SECRET_KEY=your-secret-key
ALLOWED_HOSTS=localhost,127.0.0.1,your-domain.com

# Database
DATABASE_URL=postgresql://user:pass@localhost:5432/mindsteady
REDIS_URL=redis://localhost:6379/0

# API Configuration
API_RATE_LIMIT=100
API_CACHE_TIMEOUT=300

# ML Models
MODEL_VERSION=v1.2.0
MODEL_UPDATE_FREQUENCY=daily

# External Services
SENTRY_DSN=your-sentry-dsn
LOG_LEVEL=INFO
```

### Django Settings Structure

```python
# settings/base.py - Core settings
# settings/development.py - Debug mode, local DB
# settings/production.py - Security, performance optimizations
# settings/testing.py - Test-specific configuration
```

## 🧪 Testing

### Test Suite Structure
```
tests/
├── unit/               # Unit tests
│   ├── test_models.py
│   ├── test_views.py
│   └── test_services.py
├── integration/        # Integration tests
│   ├── test_api.py
│   └── test_ml_pipeline.py
└── fixtures/          # Test data
    └── sample_requests.json
```

### Running Tests
```bash
# Run all tests
python manage.py test

# Run specific test suite
python manage.py test tests.unit

# Run with coverage
coverage run manage.py test
coverage report

# Load test fixtures
python manage.py loaddata tests/fixtures/sample_data.json
```

## 📊 Monitoring & Analytics

### Health Monitoring
- Database connection status
- Redis connection (if configured)
- ML model availability
- API response times
- Error rates and types

### Analytics Tracking
- Request volume and patterns
- Safety level distribution
- Processing performance metrics  
- User engagement statistics
- Model accuracy feedback

### Logging Configuration
```python
LOGGING = {
    'version': 1,
    'handlers': {
        'file': {
            'level': 'INFO',
            'class': 'logging.FileHandler',
            'filename': 'mindsteady.log',
        },
    },
    'loggers': {
        'mindsteady': {
            'handlers': ['file'],
            'level': 'INFO',
        },
    },
}
```

## 🚢 Deployment

### Production Deployment

1. **Docker Deployment**:
   ```bash
   # Build production image
   docker build -f docker/Dockerfile -t mindsteady-api .
   
   # Run with environment
   docker run -d --env-file .env -p 8000:8000 mindsteady-api
   ```

2. **Cloud Platforms**:
   - **AWS**: ECS, Elastic Beanstalk, or EC2
   - **Google Cloud**: Cloud Run, App Engine, or GKE
   - **Azure**: Container Instances or App Service
   - **Heroku**: Git-based deployment with Procfile

3. **Database Setup**:
   ```bash
   # Production migrations
   python manage.py migrate --settings=mindsteady.settings.production
   
   # Create admin user
   python manage.py createsuperuser --settings=mindsteady.settings.production
   ```

### Performance Optimization

- **Caching**: Redis for API response caching
- **Database**: Connection pooling, query optimization
- **Static Files**: CDN integration for static assets
- **Load Balancing**: Multiple server instances
- **Auto-scaling**: Based on CPU/memory usage

## 🔒 Security

### Security Measures
- API rate limiting per client
- CORS configuration for web clients
- SQL injection prevention via ORM
- XSS protection in API responses
- HTTPS enforcement in production
- Environment variable security

### API Key Management
```python
# Generate new API key
from apps.authentication.models import APIKey
api_key = APIKey.objects.create(
    name="Chrome Extension",
    permissions=["analysis:read", "analysis:write"]
)
```

## 🤝 Contributing

### Development Workflow
1. **Fork & Clone**: Create your development environment
2. **Feature Branch**: Create branch for your feature
3. **Development**: Follow Django best practices
4. **Testing**: Write tests for new functionality
5. **Documentation**: Update API docs and README
6. **Pull Request**: Submit with detailed description

### Code Standards
- **PEP 8**: Python code formatting
- **Black**: Code formatter
- **Flake8**: Linting and style checking
- **Type Hints**: Use type annotations
- **Docstrings**: Document functions and classes

### Pre-commit Setup
```bash
pip install pre-commit
pre-commit install
pre-commit run --all-files
```

## 📄 License

MIT License - see [LICENSE](../LICENSE) file for details.

---

**Parent Project**: [MindSteady Platform](../README.md)  
**Related**: [Chrome Extension](../extension/README.md) | [SDK Agent](../sdk-agent/README.md)