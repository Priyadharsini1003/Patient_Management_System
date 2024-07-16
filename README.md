# Patient Management System

## Demo

[![Watch the video](https://i.vimeocdn.com/video/983580502.jpg)](https://vimeo.com/984827008)

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Setup](#setup)
3. [Configuration](#configuration)
4. [Running the Application](#running-the-application)
5. [API Endpoints](#api-endpoints)
6. [Request and Response Formats](#request-and-response-formats)
7. [Data Validation Rules](#data-validation-rules)
8. [JPA Entity Mapping](#jpa-entity-mapping)
9. [Conclusion](#conclusion)

## Prerequisites

Before you begin, ensure you have met the following requirements:
- Java 11 or higher installed
- Maven installed

## Setup

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd <repository-directory>
   ```

2. **Build the project using Maven:**
   ```bash
   mvn clean install
   ```

## Configuration

Swagger is configured to provide API documentation. You can access the Swagger UI at `/swagger-ui.html` once the application is running.

### Swagger Configuration

The Swagger configuration is located in `SwaggerConfig.java`:
```java
@Configuration
public class SwaggerConfig {

    @Bean
    public OpenAPI customOpenAPI() {
        return new OpenAPI()
                .info(new Info()
                        .title("Patient Management System API")
                        .version("1.0")
                        .description("API documentation for the Patient Management System"));
    }
}
```

## Running the Application

To run the application, use the following command:
```bash
mvn spring-boot:run
```

The application will be accessible at `http://localhost:8080`.

## API Endpoints

### View Home Page
- **URL:** `/`
- **Method:** `GET`
- **Description:** View the home page with the list of available services.

### User Registration
- **URL:** `/api/register`
- **Method:** `POST`
- **Description:** Register a new patient.
- **Request Body:** Patient object

### View Available Appointments
- **URL:** `/api/appointments`
- **Method:** `GET`
- **Description:** Retrieve available appointment slots.

### Book Appointment
- **URL:** `/api/book`
- **Method:** `POST`
- **Description:** Book an appointment.
- **Request Body:** Appointment object

### View Medications
- **URL:** `/api/medications`
- **Method:** `GET`
- **Description:** Retrieve the list of medications.

### Add Medication
- **URL:** `/api/medications`
- **Method:** `POST`
- **Description:** Add a new medication.
- **Request Body:** Medication object

### Update Medication
- **URL:** `/api/medications/{id}`
- **Method:** `PUT`
- **Description:** Update a medication.
- **Path Variable:** `id (long)`: ID of the medication to be updated

### Delete Medication
- **URL:** `/api/medications/{id}`
- **Method:** `DELETE`
- **Description:** Delete a medication by ID.
- **Path Variable:** `id (long)`: ID of the medication to be deleted

## Request and Response Formats

### Patient Model
```java
public class Patient {
    private long id;
    private String name;
    private String contactDetails;
    private String medicalHistory;

    // Getters and setters
}
```

### Example Request (Register Patient)
```json
{
    "name": "Jane Doe",
    "contactDetails": "123-456-7890",
    "medicalHistory": "None"
}
```

### Example Response (Patient Details)
```json
{
    "id": 1,
    "name": "Jane Doe",
    "contactDetails": "123-456-7890",
    "medicalHistory": "None"
}
```

## Data Validation Rules

- `name`: Cannot be empty or null
- `contactDetails`: Cannot be empty or null
- `medicalHistory`: Optional

Ensure the `Patient` model class has appropriate validation annotations to enforce these rules:
```java
import javax.validation.constraints.NotEmpty;

public class Patient {

    private long id;

    @NotEmpty(message = "Name is required")
    private String name;

    @NotEmpty(message = "Contact details are required")
    private String contactDetails;

    private String medicalHistory;

    // Getters and setters
}
```

## JPA Entity Mapping

### Patient Entity
Ensure you have the correct JPA annotations in the `Patient` entity class to map it to the database table:
```java
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.Table;

@Entity
@Table(name = "patients")
public class Patient {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private long id;

    @NotEmpty(message = "Name is required")
    private String name;

    @NotEmpty(message = "Contact details are required")
    private String contactDetails;

    private String medicalHistory;

    // Getters and setters
}
```

## Conclusion

This documentation provides the necessary steps to set up, configure, and run the Patient Management System project. It also details the available endpoints, request and response formats, data validation rules, and JPA entity mapping.

