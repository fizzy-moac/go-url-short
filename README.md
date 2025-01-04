Golang URL Shortener Project

# Golang URL Shortener Project

## Overview
A URL shortener is a service that takes a long URL and generates a shorter, unique alias for it. This alias can be used to redirect users to the original URL. This project is designed to be built in phases, covering a variety of features and utilizing different tools and libraries in the Go ecosystem.

## Phases
The project is divided into four phases to progressively build the application:

### Phase 1: Basic URL Shortening Service
#### Goals:
1. Create a REST API to shorten URLs.
2. Generate short, unique codes for each URL.
3. Implement a mechanism to store and retrieve URLs.

#### Tools and Libraries:
- **Go**: Programming language.
- **net/http**: For building the REST API.
- **gorilla/mux**: Router for handling API endpoints.
- **Postgres**: Database for storage.

#### Features:
1. POST `/shorten`
   - Request: `{ "url": "https://example.com" }`
   - Response: `{ "short_url": "http://localhost/<short-code>" }`
2. GET `/<short-code>`
   - Redirects to the original URL.

---

### Phase 2: Data Persistence and Analytics
#### Goals:
1. Improve data persistence.
2. Track usage analytics (e.g., click count, timestamp).

#### Tools and Libraries:
- **GORM**: ORM for database interaction.
- **MySQL/PostgreSQL**: Robust database.
- **logrus**: Logging library.

#### Features:
1. Track and store click counts for each short URL.
2. Include metadata like creation date, expiration date, and last accessed time.
3. GET `/analytics/<short-code>`
   - Response: `{ "click_count": 123, "last_accessed": "2025-01-01T12:00:00Z" }`

---

### Phase 3: Scalability and Performance
#### Goals:
1. Make the system scalable and performant.
2. Introduce caching to reduce database load.

#### Tools and Libraries:
- **Redis**: For caching frequently accessed URLs.
- **Go channels**: To handle concurrent requests efficiently.
- **Docker**: Containerize the application.

#### Features:
1. Cache short-to-long URL mappings in Redis.
2. Use goroutines to handle high traffic.
3. Optimize database queries.

---

### Phase 4: Advanced Features and Deployment
#### Goals:
1. Add advanced features.
2. Deploy the application.

#### Tools and Libraries:
- **JWT**: For user authentication and API security.
- **Kubernetes**: For deployment.
- **Prometheus/Grafana**: For monitoring and analytics.
- **CI/CD**: Automate testing and deployment.

#### Features:
1. User authentication with JWT.
2. Support custom short codes.
   - Example: `{ "url": "https://example.com", "custom_code": "myshort" }`
3. Set URL expiration dates.
4. Deploy on Kubernetes with Helm charts.

---

## API Specifications
### Phase 1
1. **POST** `/shorten`
   - **Request Body**:
     ```json
     {
       "url": "https://example.com"
     }
     ```
   - **Response Body**:
     ```json
     {
       "short_url": "http://localhost/<short-code>"
     }
     ```
2. **GET** `/<short-code>`
   - Redirects to the original URL.

### Phase 2
1. **GET** `/analytics/<short-code>`
   - **Response Body**:
     ```json
     {
       "click_count": 123,
       "last_accessed": "2025-01-01T12:00:00Z"
     }
     ```

### Phase 4
1. **POST** `/shorten`
   - **Request Body**:
     ```json
     {
       "url": "https://example.com",
       "custom_code": "myshort",
       "expires_in": 3600
     }
     ```
   - **Response Body**:
     ```json
     {
       "short_url": "http://localhost/myshort"
     }
     ```

---

## Additional Notes
1. Each phase should include unit and integration tests.
2. The project should follow clean architecture principles.
3. Phase transitions should allow for backward compatibility where applicable.

