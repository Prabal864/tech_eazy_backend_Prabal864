# Tech Eazy Backend

## Getting Started

### Prerequisites:
1. Java SDK 21 or higher.
2. Spring dependencies.
3. A database instance (H2 In-Memory Database).
4. Postman (optional, for testing API).

### Installation:
1. Clone the repository:
   ```bash
   git clone https://github.com/Prabal864/tech_eazy_backend_Prabal864.git
   cd tech_eazy_backend_Prabal864
   ```

2. Configure application properties for database connectivity (update `application.properties`).

3. Build the project:
   ```bash
   ./mvnw clean install
   ```

4. Run the project:
   ```bash
   ./mvnw spring-boot:run
   ```

### Testing APIs:
- Import the `postman_collection.json` file into Postman to access pre-configured requests for all API endpoints.
- **Server Port:** The application runs on port `80`.
