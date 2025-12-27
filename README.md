# YT Project

A comprehensive full-stack application combining Android mobile development, backend services, and Google Cloud deployment.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [Tech Stack](#tech-stack)
- [Quick Start](#quick-start)
- [Android Setup](#android-setup)
- [Backend Setup](#backend-setup)
- [Deployment to Google Cloud](#deployment-to-google-cloud)
- [API Endpoints](#api-endpoints)
- [Contribution Guidelines](#contribution-guidelines)

## Overview

YT is a modern, scalable application that provides seamless integration between mobile and backend services. The project is designed with a microservices architecture, enabling independent development, testing, and deployment of different components.

The application leverages cutting-edge technologies to deliver a robust, performant, and maintainable codebase suitable for production environments.

## Features

- **Cross-Platform Mobile Support**: Native Android application with intuitive UI/UX
- **RESTful API**: Well-documented and tested API endpoints
- **Cloud-Native Architecture**: Deployed on Google Cloud Platform with auto-scaling capabilities
- **Authentication & Authorization**: Secure user authentication and role-based access control
- **Data Persistence**: Reliable database with proper indexing and optimization
- **Real-Time Updates**: WebSocket support for real-time data synchronization
- **Comprehensive Logging**: Structured logging for monitoring and debugging
- **Error Handling**: Graceful error handling with detailed error messages

## Architecture

### System Architecture

```
┌─────────────────────────────────────────────────────┐
│          Android Mobile Application                 │
│  (Kotlin/Java, Jetpack, Retrofit, Room Database)   │
└────────────────────┬────────────────────────────────┘
                     │ HTTPS/REST/WebSocket
                     ▼
┌─────────────────────────────────────────────────────┐
│             Google Cloud Load Balancer              │
└────────────────────┬────────────────────────────────┘
                     │
        ┌────────────┼────────────┐
        ▼            ▼            ▼
   ┌────────┐  ┌────────┐  ┌────────┐
   │  API   │  │  API   │  │  API   │ (Cloud Run/Kubernetes)
   │Instance│  │Instance│  │Instance│
   └────────┘  └────────┘  └────────┘
        │            │            │
        └────────────┼────────────┘
                     │
        ┌────────────┴────────────┐
        ▼                         ▼
   ┌──────────────┐         ┌──────────────┐
   │   Cloud SQL  │         │ Cloud Storage│
   │   (Database) │         │  (Assets)    │
   └──────────────┘         └──────────────┘
```

### Component Architecture

- **Android Client**: Native Android application handling UI/UX and local data persistence
- **API Gateway**: Load balancing and request routing
- **Backend Services**: RESTful services handling business logic
- **Data Layer**: Cloud SQL database with proper schema management
- **External Services**: Integration with third-party services as needed

## Tech Stack

### Frontend (Android)
- **Language**: Kotlin/Java
- **UI Framework**: Android Jetpack (Compose/XML layouts)
- **Networking**: Retrofit 2, OkHttp3
- **Local Database**: Room Database
- **Dependency Injection**: Hilt/Dagger
- **Image Loading**: Glide/Coil
- **Architecture Pattern**: MVVM/MVI

### Backend
- **Runtime**: Node.js / Python / Java (specify as applicable)
- **Framework**: Express.js / FastAPI / Spring Boot (specify as applicable)
- **Database**: PostgreSQL / MySQL (Cloud SQL)
- **ORM**: Sequelize / SQLAlchemy / Hibernate (specify as applicable)
- **Authentication**: JWT / OAuth 2.0
- **API Documentation**: Swagger/OpenAPI

### Infrastructure
- **Deployment Platform**: Google Cloud Platform
- **Container Orchestration**: Cloud Run / Google Kubernetes Engine (GKE)
- **Load Balancing**: Cloud Load Balancer
- **Database**: Cloud SQL
- **Storage**: Cloud Storage
- **Monitoring**: Cloud Monitoring / Cloud Logging
- **CI/CD**: Cloud Build / GitHub Actions

## Quick Start

### Prerequisites

- **Git**: Version control
- **Android Studio**: For Android development
- **Node.js 16+** / **Python 3.9+** / **Java 11+**: For backend development (specify as applicable)
- **Docker**: For containerization
- **Google Cloud SDK**: For GCP deployment
- **PostgreSQL/MySQL**: For local development (optional with Docker)

### Clone the Repository

```bash
git clone https://github.com/brandmclen-web/yt.git
cd yt
```

### Project Structure

```
yt/
├── android/                 # Android application
│   ├── app/
│   ├── build.gradle
│   └── settings.gradle
├── backend/                 # Backend services
│   ├── src/
│   ├── package.json / requirements.txt / pom.xml
│   └── Dockerfile
├── docs/                    # Documentation
├── .github/
│   └── workflows/          # CI/CD workflows
├── docker-compose.yml      # Local development setup
└── README.md
```

## Android Setup

### Prerequisites

- Android Studio Arctic Fox or newer
- Android SDK 21+ (API level)
- Gradle 7.0+
- Kotlin 1.6+

### Installation & Configuration

1. **Open the Android Project**
   ```bash
   cd android
   ```

2. **Install Dependencies**
   ```bash
   ./gradlew build
   ```

3. **Configure API Endpoints**
   
   Edit `android/app/src/main/res/values/strings.xml`:
   ```xml
   <resources>
       <string name="api_base_url">https://api.example.com/v1</string>
       <string name="websocket_url">wss://api.example.com/ws</string>
   </resources>
   ```

4. **Set Up Local Properties**
   
   Create `android/local.properties`:
   ```properties
   sdk.dir=/path/to/android/sdk
   ```

5. **Build the Application**
   ```bash
   ./gradlew assemble
   ```

6. **Run on Emulator or Device**
   ```bash
   ./gradlew installDebug
   adb shell am start -n com.example.yt/.MainActivity
   ```

### Development Workflow

- **Build Variants**: Debug, Release, and Staging configurations
- **Automated Tests**: Run with `./gradlew test`
- **Lint Checks**: Run with `./gradlew lint`
- **Code Coverage**: Generate with `./gradlew jacocoTestReport`

### Signing & Release Build

1. **Generate Keystore**
   ```bash
   keytool -genkey -v -keystore release.keystore -alias yt -keyalg RSA -keysize 2048 -validity 10000
   ```

2. **Configure Signing in `build.gradle`**
   ```gradle
   signingConfigs {
       release {
           storeFile file('release.keystore')
           storePassword System.getenv("KEYSTORE_PASSWORD")
           keyAlias 'yt'
           keyPassword System.getenv("KEY_PASSWORD")
       }
   }
   ```

3. **Build Release APK**
   ```bash
   ./gradlew assembleRelease
   ```

## Backend Setup

### Prerequisites

- Node.js 16+ / Python 3.9+ / Java 11+ (specify as applicable)
- Package manager (npm/yarn, pip, maven/gradle)
- PostgreSQL/MySQL 12+
- Redis (for caching, optional)

### Installation & Configuration

1. **Navigate to Backend Directory**
   ```bash
   cd backend
   ```

2. **Install Dependencies**
   
   For Node.js:
   ```bash
   npm install
   ```
   
   For Python:
   ```bash
   pip install -r requirements.txt
   ```
   
   For Java:
   ```bash
   mvn install
   ```

3. **Configure Environment Variables**
   
   Create `.env` file:
   ```env
   # Server Configuration
   NODE_ENV=development
   PORT=3000
   
   # Database Configuration
   DB_HOST=localhost
   DB_PORT=5432
   DB_USER=postgres
   DB_PASSWORD=password
   DB_NAME=yt_db
   
   # Authentication
   JWT_SECRET=your-secret-key-change-this
   JWT_EXPIRATION=7d
   
   # Google Cloud
   GCP_PROJECT_ID=your-project-id
   GCP_SERVICE_ACCOUNT_PATH=./service-account.json
   
   # API Configuration
   API_VERSION=v1
   CORS_ORIGIN=http://localhost:3000
   
   # Logging
   LOG_LEVEL=debug
   ```

4. **Database Setup**
   
   Create and migrate database:
   ```bash
   # Using Docker Compose (recommended)
   docker-compose up -d postgres
   
   # Run migrations
   npm run migrate  # or appropriate migration command
   ```

5. **Start Development Server**
   ```bash
   npm run dev
   # Server running at http://localhost:3000
   ```

6. **Run Tests**
   ```bash
   npm test
   ```

### Development Best Practices

- **Environment Variables**: Use `.env` for local configuration, never commit secrets
- **Database Migrations**: Version control all schema changes
- **Code Formatting**: Use ESLint/Prettier (or language equivalents)
- **API Documentation**: Maintain Swagger/OpenAPI specifications
- **Logging**: Use structured logging (e.g., Winston, Python logging)
- **Error Handling**: Implement comprehensive error handling middleware

## Deployment to Google Cloud

### Prerequisites

- Google Cloud Account with billing enabled
- `gcloud` CLI installed and authenticated
- Docker installed locally
- Appropriate IAM permissions

### Step 1: Prepare for Deployment

1. **Create GCP Project**
   ```bash
   gcloud projects create yt-project
   gcloud config set project yt-project
   ```

2. **Enable Required APIs**
   ```bash
   gcloud services enable \
     cloudbuild.googleapis.com \
     run.googleapis.com \
     sqladmin.googleapis.com \
     cloudresourcemanager.googleapis.com \
     containerregistry.googleapis.com
   ```

### Step 2: Set Up Cloud SQL Database

1. **Create Cloud SQL Instance**
   ```bash
   gcloud sql instances create yt-db \
     --database-version=POSTGRES_14 \
     --tier=db-f1-micro \
     --region=us-central1 \
     --availability-type=REGIONAL
   ```

2. **Create Database and User**
   ```bash
   gcloud sql databases create yt_production --instance=yt-db
   gcloud sql users create yt_user --instance=yt-db --password
   ```

3. **Migrate Database Schema**
   ```bash
   # Connect to database and run migrations
   gcloud sql connect yt-db --user=yt_user
   # Run migration scripts
   ```

### Step 3: Configure Cloud Build

1. **Create `cloudbuild.yaml` in repository root**
   ```yaml
   steps:
     # Build Docker image
     - name: 'gcr.io/cloud-builders/docker'
       args:
         - 'build'
         - '-t'
         - 'gcr.io/$PROJECT_ID/yt-backend:$SHORT_SHA'
         - '-t'
         - 'gcr.io/$PROJECT_ID/yt-backend:latest'
         - '.'
       dir: 'backend'
   
     # Push to Container Registry
     - name: 'gcr.io/cloud-builders/docker'
       args:
         - 'push'
         - 'gcr.io/$PROJECT_ID/yt-backend:$SHORT_SHA'
   
     # Deploy to Cloud Run
     - name: 'gcr.io/cloud-builders/gke-deploy'
       args:
         - run
         - --filename=k8s/
         - --image=gcr.io/$PROJECT_ID/yt-backend:$SHORT_SHA
         - --location=us-central1
         - --cluster=yt-cluster
   
   images:
     - 'gcr.io/$PROJECT_ID/yt-backend:$SHORT_SHA'
     - 'gcr.io/$PROJECT_ID/yt-backend:latest'
   
   options:
     machineType: 'N1_HIGHCPU_8'
   ```

2. **Connect Repository to Cloud Build**
   ```bash
   gcloud builds connect --repository-name=yt --repository-owner=brandmclen-web
   ```

### Step 4: Deploy Backend to Cloud Run

1. **Build and Deploy**
   ```bash
   gcloud run deploy yt-backend \
     --source backend \
     --platform managed \
     --region us-central1 \
     --allow-unauthenticated \
     --set-env-vars="DB_HOST=CLOUD_SQL_IP,DB_USER=yt_user,DB_PASSWORD=YOUR_PASSWORD"
   ```

2. **Configure Cloud SQL Connections**
   ```bash
   gcloud run services update yt-backend \
     --add-cloudsql-instances=PROJECT_ID:us-central1:yt-db \
     --region=us-central1
   ```

### Step 5: Set Up Load Balancer

1. **Create Load Balancer**
   ```bash
   gcloud compute load-balancers create yt-lb \
     --global \
     --enable-http2
   ```

2. **Configure Backend Service**
   ```bash
   gcloud compute backend-services create yt-backend \
     --global \
     --protocol=HTTPS \
     --health-checks=yt-health-check
   ```

### Step 6: Monitor Deployment

1. **View Logs**
   ```bash
   gcloud logging read "resource.type=cloud_run_revision" --limit 50 --format json
   ```

2. **Set Up Monitoring Alerts**
   ```bash
   gcloud monitoring policies create \
     --notification-channels=CHANNEL_ID \
     --display-name="YT Backend Error Rate"
   ```

### CI/CD Pipeline

The GitHub Actions workflow automatically:
1. Runs tests on pull requests
2. Builds Docker images
3. Pushes to Container Registry
4. Deploys to Cloud Run on merge to main
5. Sends deployment notifications

See `.github/workflows/` for detailed configuration.

## API Endpoints

### Base URL
```
Production: https://api.example.com/v1
Staging: https://staging-api.example.com/v1
Development: http://localhost:3000/v1
```

### Authentication
All requests (except login/register) require a JWT token in the Authorization header:
```
Authorization: Bearer <token>
```

### Core Endpoints

#### Authentication
- **POST** `/auth/register` - Register new user
  ```json
  Request:
  {
    "email": "user@example.com",
    "password": "password123",
    "name": "John Doe"
  }
  
  Response (201):
  {
    "id": "uuid",
    "email": "user@example.com",
    "name": "John Doe",
    "token": "eyJhbGc..."
  }
  ```

- **POST** `/auth/login` - Login user
  ```json
  Request:
  {
    "email": "user@example.com",
    "password": "password123"
  }
  
  Response (200):
  {
    "token": "eyJhbGc...",
    "refreshToken": "eyJhbGc...",
    "expiresIn": 3600
  }
  ```

- **POST** `/auth/refresh` - Refresh token
  ```json
  Request:
  {
    "refreshToken": "eyJhbGc..."
  }
  
  Response (200):
  {
    "token": "eyJhbGc..."
  }
  ```

#### Users
- **GET** `/users/profile` - Get current user profile
- **PUT** `/users/profile` - Update user profile
- **GET** `/users/:id` - Get user by ID
- **DELETE** `/users/:id` - Delete user account

#### Resources (Example)
- **GET** `/resources` - List all resources with pagination
  ```json
  Query Parameters:
  - page: number (default: 1)
  - limit: number (default: 20)
  - sort: string (default: -createdAt)
  - filter: object
  
  Response (200):
  {
    "data": [...],
    "pagination": {
      "page": 1,
      "limit": 20,
      "total": 100,
      "pages": 5
    }
  }
  ```

- **POST** `/resources` - Create resource
- **GET** `/resources/:id` - Get resource by ID
- **PUT** `/resources/:id` - Update resource
- **DELETE** `/resources/:id` - Delete resource

#### Health Check
- **GET** `/health` - Service health status
  ```json
  Response (200):
  {
    "status": "healthy",
    "timestamp": "2025-12-27T20:00:45Z",
    "uptime": 3600,
    "database": "connected"
  }
  ```

### Error Responses

Standard error response format:
```json
{
  "error": {
    "code": "INVALID_REQUEST",
    "message": "Invalid request parameters",
    "details": [
      {
        "field": "email",
        "message": "Invalid email format"
      }
    ]
  }
}
```

Common Status Codes:
- `200` - OK
- `201` - Created
- `400` - Bad Request
- `401` - Unauthorized
- `403` - Forbidden
- `404` - Not Found
- `409` - Conflict
- `500` - Internal Server Error

### Rate Limiting

API endpoints are rate limited:
- **Unauthenticated**: 100 requests/hour
- **Authenticated**: 1000 requests/hour

Rate limit headers:
```
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 999
X-RateLimit-Reset: 1640609645
```

### WebSocket API

Connect to real-time updates:
```javascript
const ws = new WebSocket('wss://api.example.com/ws?token=YOUR_TOKEN');

ws.onmessage = (event) => {
  const message = JSON.parse(event.data);
  // Handle real-time updates
};

ws.onerror = (error) => {
  console.error('WebSocket error:', error);
};
```

## Contribution Guidelines

### Getting Started

1. **Fork the Repository**
   ```bash
   # On GitHub UI, click "Fork"
   ```

2. **Clone Your Fork**
   ```bash
   git clone https://github.com/YOUR_USERNAME/yt.git
   cd yt
   ```

3. **Add Upstream Remote**
   ```bash
   git remote add upstream https://github.com/brandmclen-web/yt.git
   ```

### Development Workflow

1. **Create Feature Branch**
   ```bash
   git checkout -b feature/your-feature-name
   # or for bug fixes:
   git checkout -b fix/bug-description
   ```

2. **Commit Changes**
   ```bash
   git add .
   git commit -m "feat: add new feature" -m "Detailed description of changes"
   # or
   git commit -m "fix: resolve issue with authentication"
   ```

   Use conventional commit format:
   - `feat:` for new features
   - `fix:` for bug fixes
   - `docs:` for documentation
   - `style:` for code style changes
   - `refactor:` for code refactoring
   - `perf:` for performance improvements
   - `test:` for test additions/changes
   - `chore:` for build, dependencies, etc.

3. **Push to Your Fork**
   ```bash
   git push origin feature/your-feature-name
   ```

4. **Create Pull Request**
   - Go to GitHub and create PR against `main` branch
   - Fill in the PR template with description, changes, and testing notes
   - Link related issues

### Code Standards

#### Android Development
- Follow [Kotlin Coding Conventions](https://kotlinlang.org/docs/coding-conventions.html)
- Use meaningful variable/function names
- Add KDoc comments for public APIs
- Ensure test coverage > 80%
- Run `./gradlew lint` before submitting

#### Backend Development
- Follow language-specific style guides
- Maintain consistent code formatting
- Add unit tests for new features
- Update API documentation in Swagger/OpenAPI
- Test database migrations thoroughly

### Testing Requirements

All contributions must include:

1. **Unit Tests**
   ```bash
   # Android
   ./gradlew test
   
   # Backend
   npm test  # or appropriate command
   ```

2. **Integration Tests**
   - Test API endpoints
   - Test database interactions
   - Test external service integrations

3. **Code Coverage**
   - Minimum 80% code coverage for new code
   - Upload coverage reports to CI/CD

### Pull Request Checklist

Before submitting, ensure:

- [ ] Code follows project style guidelines
- [ ] All tests pass locally (`./gradlew test`, `npm test`)
- [ ] Code coverage is maintained or improved
- [ ] Documentation is updated (README, API docs, code comments)
- [ ] Commits are well-structured with clear messages
- [ ] No merge conflicts with `main` branch
- [ ] No sensitive data (API keys, passwords) in code

### Review Process

1. **Automated Checks**
   - CI/CD pipeline runs tests and lint checks
   - Code coverage reports generated
   - Automated security scanning

2. **Code Review**
   - Maintainers review code for quality and compatibility
   - Comments and suggestions provided
   - Request changes if needed

3. **Approval and Merge**
   - Requires at least 2 approvals for main branch
   - Squash and merge for clean history
   - Automated deployment to staging (if applicable)

### Reporting Issues

1. **Use GitHub Issues**
   - Clear, descriptive title
   - Detailed description of the issue
   - Steps to reproduce
   - Expected vs actual behavior
   - Environment details

2. **Label Issues**
   - `bug` for bug reports
   - `feature` for feature requests
   - `documentation` for doc issues
   - `good first issue` for beginners

### Getting Help

- **Questions**: Open a discussion in GitHub Discussions
- **Chat**: Join our Slack/Discord community (if applicable)
- **Documentation**: Check wiki and existing issues
- **Email**: Contact maintainers at support@example.com

### Community Guidelines

- Be respectful and inclusive
- Provide constructive feedback
- Help review other PRs
- Share knowledge and best practices
- Report security issues responsibly

---

## License

This project is licensed under the MIT License - see LICENSE file for details.

## Support

For support, documentation, and discussions:
- 📧 Email: support@example.com
- 💬 GitHub Issues: [Create an issue](https://github.com/brandmclen-web/yt/issues)
- 📚 Documentation: [Wiki](https://github.com/brandmclen-web/yt/wiki)

## Acknowledgments

- Android Jetpack documentation and samples
- Google Cloud Platform guides
- Community contributions and feedback

---

**Last Updated**: 2025-12-27

**Maintainers**: @brandmclen-web and team
