# Smart Email Assistant

An AI-powered email assistant that helps users draft professional email responses using Google's Gemini API. This application leverages advanced language models to generate contextual, tone-appropriate email replies.

---

## Table of Contents

- [Features](#features)
- [Technology Stack](#technology-stack)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [API Documentation](#api-documentation)
- [Project Structure](#project-structure)
- [Development](#development)
- [License](#license)

---

## Features

- **AI-Powered Email Generation**: Uses Google Gemini API to generate intelligent email responses
- **Tone Control**: Supports custom tone specification (professional, casual, formal, etc.)
- **RESTful API**: Clean and intuitive API for email generation
- **Spring Boot Framework**: Built on Spring Boot 4.0.2 for robust application architecture
- **Reactive Support**: Includes WebFlux for non-blocking I/O operations
- **Easy Integration**: Simple request-response model for seamless integration

---

## Technology Stack

- **Language**: Java 21
- **Framework**: Spring Boot 4.0.2
  - Spring Web MVC
  - Spring WebFlux (reactive)
- **Build Tool**: Maven
- **Libraries**:
  - Lombok (for reducing boilerplate code)
  - Jackson (for JSON processing)
  - JSpecify (for better null safety)
- **External API**: Google Gemini API

---

## Architecture

The application follows a layered architecture:

```
Controller Layer
    ↓
Service Layer (Business Logic)
    ↓
External API (Google Gemini)
```

### Components

1. **EmailGeneratorController**: REST controller handling incoming API requests
2. **EmailGeneratorService**: Business logic for email generation and API communication
3. **EmailRequest**: Data model for request payload

---

## Prerequisites

- **Java 21** or higher installed
- **Maven 3.6+** installed
- **Google Gemini API Key** (obtain from Google Cloud Console)
- **Internet Connection** (for API calls)

---

## Installation

1. **Clone the Repository**
   ```bash
   git clone https://github.com/your-repo/Smart-Email-Assistant.git
   cd Smart-Email-Assistant
   ```

2. **Navigate to the Project Directory**
   ```bash
   cd email-writer/email-writer
   ```

3. **Build the Project**
   ```bash
   mvn clean install
   ```

---

## Configuration

### Setting Up API Credentials

1. Obtain your Google Gemini API key from [Google Cloud Console](https://console.cloud.google.com/)

2. Update the `application.properties` file with your credentials:
   ```properties
   spring.application.name=email-writer
   
   gemini.api.url=https://generativelanguage.googleapis.com/v1/models/gemini-pro:generateContent
   gemini.api.key=YOUR_API_KEY_HERE
   ```

3. Alternatively, set environment variables:
   ```bash
   export GEMINI_API_URL=https://generativelanguage.googleapis.com/v1/models/gemini-pro:generateContent
   export GEMINI_API_KEY=your_api_key_here
   ```

### Application Properties

- **Port**: Default is 8080 (configurable via `server.port` in application.properties)
- **Context Path**: `/api/v1/email` for all email endpoints

---

## Running the Application

### Using Maven
```bash
mvn spring-boot:run
```

### Using Java Command
```bash
java -jar target/email-writer-0.0.1-SNAPSHOT.jar
```

### With Custom Properties
```bash
java -jar target/email-writer-0.0.1-SNAPSHOT.jar \
  --gemini.api.url=<YOUR_API_URL> \
  --gemini.api.key=<YOUR_API_KEY>
```

The application will start on `http://localhost:8080`

---

## API Documentation

### Generate Email Response

**Endpoint**: `POST /api/v1/email/generate`

**Request Body**:
```json
{
  "emailContent": "Hi, I wanted to discuss the project timeline for Q2...",
  "tone": "professional"
}
```

**Request Parameters**:
- `emailContent` (string, required): The original email content to respond to
- `tone` (string, optional): Desired tone for the response (e.g., "professional", "casual", "formal", "friendly")

**Response**:
```json
{
  "response": "Thank you for reaching out regarding the Q2 project timeline..."
}
```

**Status Codes**:
- `200 OK`: Email response generated successfully
- `400 Bad Request`: Invalid or missing request parameters
- `500 Internal Server Error`: API processing error

**Example Request**:
```bash
curl -X POST http://localhost:8080/api/v1/email/generate \
  -H "Content-Type: application/json" \
  -d '{
    "emailContent": "Can you provide an update on the status?",
    "tone": "professional"
  }'
```

---

## Project Structure

```
Smart-Email-Assistant/
├── README.md
├── LICENSE
└── email-writer/
    └── email-writer/
        ├── pom.xml                          # Maven configuration
        ├── mvnw                             # Maven wrapper (Linux/Mac)
        ├── mvnw.cmd                         # Maven wrapper (Windows)
        ├── HELP.md
        └── src/
            ├── main/
            │   ├── java/
            │   │   └── com/email/email_writer/
            │   │       ├── EmailWriterApplication.java      # Main Spring Boot application
            │   │       └── app/
            │   │           ├── EmailGeneratorController.java # REST API endpoints
            │   │           ├── EmailGeneratorService.java    # Business logic
            │   │           └── EmailRequest.java             # Request DTO
            │   └── resources/
            │       ├── application.properties                # Configuration
            │       ├── static/                               # Static resources
            │       └── templates/                            # HTML templates
            └── test/
                └── java/
                    └── com/email/email_writer/
                        └── EmailWriterApplicationTests.java  # Unit tests
```

---

## Development

### Running Tests
```bash
mvn test
```

### Building JAR
```bash
mvn clean package
```

### Code Generation with Lombok
The project uses Lombok annotations to reduce boilerplate code:
- `@Data`: Generates getters, setters, equals, hashCode, toString
- `@AllArgsConstructor`: Generates constructor for all fields
- `@NonNull`: Runtime null-checks

### IDE Setup
For IntelliJ IDEA:
1. Install Lombok plugin
2. Enable annotation processing in Settings → Compiler → Annotation Processors

---

## Error Handling

The service includes error handling for:
- JSON parsing errors
- API connection failures
- Invalid response formats

Errors are returned with descriptive messages prefixed with "Error processing request:"

---

## How It Works

1. User sends an email content and desired tone to the API
2. The service constructs a prompt with the email context and tone
3. The prompt is sent to Google Gemini API via HTTP POST request
4. The API returns a generated response
5. The service extracts the text content from the API response
6. The generated email reply is returned to the user

---

## Future Enhancements

- [ ] User authentication and authorization
- [ ] Email history and templates
- [ ] Support for multiple language models
- [ ] Batch processing for multiple emails
- [ ] Response customization and refinement
- [ ] Integration with email clients
- [ ] Analytics and usage metrics

---

## License

This project is licensed under the terms specified in the LICENSE file.

---

## Contributing

Contributions are welcome! Please follow these steps:
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## Support

For issues, questions, or suggestions, please open an issue in the repository or contact the development team.
