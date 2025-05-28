# Adstart Media

This repository serves as the orchestration layer for a multi-service application, bringing together a Spring Boot backend, a Next.js frontend, and a React Vite admin panel. It uses **Git Submodules** to include the individual project repositories and **Docker Compose** to manage their build and runtime lifecycle.

Each core application (backend, frontend, admin) is maintained in its own dedicated GitHub repository and is included here as a submodule. This setup allows for independent development and versioning of each service while providing a unified environment for local development and deployment using Docker.

## Project Structure

```
.
├── Adstart-Media-backend/   # Spring Boot Backend (Git Submodule)
├── Adstart-Media-Frontend/  # Next.js Frontend (Git Submodule)
├── Adstart-Media-Admin/     # React Vite Admin (Git Submodule)
├── docker-compose.yml       # Docker Compose file for orchestration
├── .gitmodules              # Git configuration for submodules
└── README.md                # This README file
```

## Prerequisites

Before you begin, ensure you have the following installed on your machine:

* **Git:** For cloning the repository and managing submodules.
* **Docker Desktop:** Includes Docker Engine and Docker Compose.

## Getting Started

Follow these steps to get the entire application suite up and running on your local machine.

### 1. Clone the Repository (with Submodules)

It's crucial to clone this repository *with its submodules* to ensure all application code is pulled down correctly.

```bash
git clone --recurse-submodules [https://github.com/teoMarinov/Adstart.git](https://github.com/teoMarinov/Adstart.git)

cd Adstart
```

If you accidentally cloned without `--recurse-submodules` or need to initialize them later:

```bash
git submodule update --init --recursive
```

### 2. Set Up Environment Variables

Each sub-project **must** have its own `.env` file (e.g., `Adstart-Media-backend/.env`). These files contain configurations specific to each service. Ensure they are properly set up according to each project's needs; refer to their individual READMEs for detailed instructions. The `docker-compose.yml` file is configured to load these environment variables for each respective service.

### 3. Build and Run the Applications

Once the repository and submodules are cloned, you can use Docker Compose to build the images and start all services:

```bash
docker-compose up --build
```

* The `--build` flag ensures that Docker Compose rebuilds the images for each service. This is especially important the first time you run it, or after making changes to a Dockerfile or code dependencies.
* This command will download base images, build your application images, and start the containers. This process might take some time on the first run.

## Accessing the Applications

Once all containers are up and running, you can access your applications via your web browser:

* **Spring Boot Backend:** `http://localhost:8080`
* **Next.js Frontend:** `http://localhost:3000`
* **React Vite Admin:** `http://localhost:5173`

## Managing the Applications

* **Stop all services:**
    ```bash
    docker-compose down
    ```
* **Stop and remove all services, networks, and anonymous volumes:**
    ```bash
    docker-compose down --volumes
    ```
* **View running containers:**
    ```bash
    docker-compose ps
    ```
* **View logs for a specific service (e.g., `adstart-server`):**
    ```bash
    docker-compose logs adstart-server
    ```
* **Run a command inside a specific service container (e.g., bash in `adstart-frontend`):**
    ```bash
    docker-compose exec adstart-frontend sh
    ```

## Updating Submodules

If any changes are pushed to the individual child repositories (e.g., `Adstart-Media-backend`), you'll need to pull those changes into this parent repository:

```bash
git pull                   # Pull changes for the parent repo itself
git submodule update --remote --merge # Pull latest changes for all submodules
```
After updating submodules, you might need to rebuild the specific service's Docker image:
```bash
docker-compose build <service_name> # e.g., docker-compose build adstart-frontend
docker-compose up -d <service_name> # Restart the specific service (or just `docker-compose up` to re-create it)
```

## Further Documentation

For detailed information about each specific application (e.g., how to run them standalone, their APIs, etc.), please refer to their respective `README.md` files located in their submodule directories:

* [`Adstart-Media-backend/README.md`](./Adstart-Media-backend/README.md)
* [`Adstart-Media-Frontend/README.md`](./Adstart-Media-Frontend/README.md)
* [`Adstart-Media-Admin/README.md`](./Adstart-Media-Admin/README.md)
