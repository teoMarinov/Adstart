# Backend Project Documentation

## Overview

This project is a CRUD application built with Java and Spring Boot, designed to handle quote requests. While the developer has more experience with Node.js and TypeScript, this project aims to follow best practices for Java development.

For more information about the overall project setup and architecture, see the main [`README.md`](README.md). For details on setting up and running the backend specifically, refer to [`Adstart-Media-Backend/README.md`](https://github.com/teoMarinov/Adstart-Media-Backend/blob/main/README.md).

## Authentication

The project supports admin authentication using JWT (JSON Web Tokens). The security configuration, including JWT handling, can be found in [`SecurityConfig.java`](https://github.com/teoMarinov/Adstart-Media-Backend/blob/main/src/main/java/com/teodor/backend/config/SecurityConfig.java).

## Project Structure

The project follows the Model-View-Controller (MVC) architectural pattern, with the following directory structure:

*   **config**: Contains configuration files, such as routes middleware.
*   **controller**: Contains the controllers that handle incoming API requests and route them to the appropriate services.
*   **dto**: Contains Data Transfer Objects (DTOs) used to transfer data between the client and the server.
*   **entity**: Contains the entity classes that represent the data model.
*   **enums**: Contains any enums used in the project.
*   **exceptionhandler**: Contains classes for handling exceptions globally.
*   **repository**: Contains the repositories that provide data access methods for the entities.
*   **seeder**: Contains classes used to seed the database with initial data like creating admin user.
*   **service**: Contains the service classes that implement the business logic of the application.

## Main Purpose: Handling Quote Requests

The primary function of this application is to manage quote requests. You can interact with the application through the frontend UI, which is accessible at [https://brix.teodormarinov.online/](https://brix.teodormarinov.online/). The frontend code is located in the [`Adstart-Media-Frontend`](https://github.com/teoMarinov/Adstart-Media-Frontend) directory.

## Quote Request Flow

1.  **Data Validation:** When a user submits a quote request through the frontend, the data is validated using the [`QuoteRequestDto.java`](https://github.com/teoMarinov/Adstart-Media-Backend/blob/main/src/main/java/com/teodor/backend/dto/QuoteRequestDto.java) DTO in the backend. This ensures that the input data is in the correct format and meets the required criteria.
2.  **API Handling:** The API request is handled by the [`QuoteRequestController.java`](https://github.com/teoMarinov/Adstart-Media-Backend/blob/main/src/main/java/com/teodor/backend/controller/QuoteRequestController.java). This controller exposes the API endpoints for creating, retrieving, and managing quote requests.
3.  **Business Logic:** The [`QuoteRequestController.java`](https://github.com/teoMarinov/Adstart-Media-Backend/blob/main/src/main/java/com/teodor/backend/controller/QuoteRequestController.java) uses the [`QuoteRequestService.java`](https://github.com/teoMarinov/Adstart-Media-Backend/blob/main/src/main/java/com/teodor/backend/service/QuoteRequestService.java) to handle the business logic for the request. This service contains the core logic for creating, retrieving, and updating quote requests.
4.  **Database Interaction:** The [`QuoteRequestService.java`](https://github.com/teoMarinov/Adstart-Media-Backend/blob/main/src/main/java/com/teodor/backend/service/QuoteRequestService.java) uses the `JpaRepository` (specifically, [`QuoteRequestRepository`](https://github.com/teoMarinov/Adstart-Media-Backend/blob/main/src/main/java/com/teodor/backend/repository/QuoteRequestRepository.java)) to interact with the database and persist the quote request data.

## Try it Out Yourself

The backend API is hosted at [https://api.brix.teodormarinov.online](https://api.brix.teodormarinov.online). You can use tools like `curl` or Postman to interact with the API endpoints.

### Available Endpoints

Here's a list of the available endpoints in the controllers:

#### AuthController ([`AuthController.java`](Adstart-Media-Backend/src/main/java/com/teodor/backend/controller/AuthController.java))

*   `POST /auth/login`: Authenticates a user and returns a JWT token.
    *   **Publicly Accessible**
    *   Requires a `username` and `password` in the request body.
    *   Returns a JWT token in the response.

#### QuoteRequestController ([`QuoteRequestController.java`](Adstart-Media-Backend/src/main/java/com/teodor/backend/controller/QuoteRequestController.java))

*   `POST /quote-request`: Creates a new quote request.
    *   **Publicly Accessible**
    *   Requires a valid `QuoteRequestDto` in the request body.
*   `GET /quote-request`: Retrieves all quote requests with pagination.
    *   **Requires JWT Token**
    *   Accepts an optional `page` query parameter for pagination.
*   `GET /quote-request/{id}`: Retrieves a quote request by its ID.
    *   **Requires JWT Token**

#### SubscriptionController ([`SubscriptionController.java`](Adstart-Media-Backend/src/main/java/com/teodor/backend/controller/SubscriptionController.java))

*   `POST /subscribe`: Subscribes an email to the newsletter.
    *   **Publicly Accessible**
    *   Requires a `SubscriptionDto` with an `email` in the request body.

### Obtaining a JWT Token

To access the endpoints that require a JWT token, you first need to authenticate with the `/auth/login` endpoint.

1.  Send a `POST` request to `https://api.brix.teodormarinov.online/auth/login` with the following JSON body:

    ```json
    {
      "username": "admin",
      "password": "admin"
    }
    ```

2.  The response will contain an `AuthResponseDto` with a `token` field. This is your JWT token.

    ```json
    {
      "success": true,
      "error": false,
      "errorMessage": null,
      "data": {
        "token": "YOUR_JWT_TOKEN",
        "username": "admin",
        "id": 1
      }
    }
    ```

3.  Include the JWT token in the `Authorization` header of your requests to the protected endpoints. The header should be in the format: `Bearer YOUR_JWT_TOKEN`.

    Example using `curl`:

    ```bash
    curl -H "Authorization: Bearer YOUR_JWT_TOKEN" https://api.brix.teodormarinov.online/quote-request
    ```

This expanded documentation provides a comprehensive overview of the project, including how to interact with the API and handle authentication.
