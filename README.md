# Abdullah's Coupon WebApp

## Overview

Abdullah's Coupon WebApp is a lightweight Flask-based web application that displays promotional discount coupons through a responsive, dark-themed UI and exposes coupon data via a REST JSON API. The project demonstrates a complete containerization and orchestration workflow using Docker and Kubernetes, making it suitable as a reference implementation for deploying simple web services in a cloud-native environment.

## Key Features

- **Coupon Dashboard** — Responsive card-based UI listing available discount coupons with titles, descriptions, expiry dates, and promo codes.
- **One-Click Copy** — Clipboard integration allows users to copy coupon codes instantly.
- **REST API Endpoint** — JSON API at `/coupons` exposes structured coupon data for programmatic consumption.
- **Dockerized** — Application is fully containerized using a minimal `python:3.9-slim` base image.
- **Kubernetes-Ready** — Includes a Kubernetes `Deployment` manifest configured to run 6 replicas for high availability.

## Tech Stack

| Category     | Technology                        |
|--------------|-----------------------------------|
| Language     | Python 3.9                        |
| Framework    | Flask                             |
| Templating   | Jinja2 (via `render_template_string`) |
| Containerization | Docker                        |
| Orchestration | Kubernetes                       |
| Base Image   | `python:3.9-slim`                 |

## Installation

### Prerequisites

- [Docker](https://docs.docker.com/get-docker/) installed
- (Optional) A Kubernetes cluster with `kubectl` configured

### 1. Clone the Repository

```bash
git clone https://github.com/vanix056/Computer-Networks-Dockerization-Project.git
cd Computer-Networks-Dockerization-Project/project
```

### 2. Build the Docker Image

```bash
docker build -t coupon-webapp .
```

### 3. Run the Container

```bash
docker run -p 5000:5000 coupon-webapp
```

The application will be available at `http://localhost:5000`.

### 4. Run Locally Without Docker

```bash
pip install flask
python app.py
```

## Usage

### Web UI

Open your browser and navigate to:

```
http://localhost:5000
```

Browse available coupons, view expiry dates, and click **Copy Code** to copy a promo code to your clipboard.

### JSON API

Retrieve all coupons as JSON:

```
GET http://localhost:5000/coupons
```

**Example response:**

```json
[
  {
    "id": 1,
    "title": "10% off",
    "expiry": "2024-12-31",
    "description": "Get 10% off on all items.",
    "code": "SAVE10"
  }
]
```

## Project Structure

```
Computer-Networks-Dockerization-Project/
└── project/
    ├── app.py            # Flask application — UI and API routes
    ├── Dockerfile        # Container build instructions
    ├── deployment.yaml   # Kubernetes Deployment manifest (6 replicas)
    └── flask_env/        # Python virtual environment (local development)
```

## API Routes

| Method | Endpoint   | Description                        |
|--------|------------|------------------------------------|
| `GET`  | `/`        | Renders the coupon dashboard UI    |
| `GET`  | `/coupons` | Returns all coupons as a JSON array |

## Deployment

### Docker Hub

The production image is published to Docker Hub as `vanix013/project:v6`.

Pull and run directly:

```bash
docker pull vanix013/project:v6
docker run -p 5000:5000 vanix013/project:v6
```

### Kubernetes

Apply the included deployment manifest to your cluster:

```bash
kubectl apply -f deployment.yaml
```

This creates a `Deployment` named `project` with **6 replicas**, each serving on container port `5000`. Expose the deployment with a Service as needed:

```bash
kubectl expose deployment project --type=LoadBalancer --port=80 --target-port=5000
```

## Infrastructure

- **Container Runtime:** Docker (`python:3.9-slim` base image, single-stage build)
- **Orchestration:** Kubernetes `apps/v1` Deployment
- **Replicas:** 6 (configured in `deployment.yaml` for load distribution)
- **Port:** Container exposes `5000`; mapped to host or Kubernetes service as needed

## Configuration

The application currently uses in-memory coupon data defined directly in `app.py`. No external environment variables or configuration files are required to run the application.

To extend with environment-based configuration (e.g., database URL, secret key), add a `.env` file and load it using `python-dotenv`.

## Contributing

1. Fork the repository and create a feature branch.
2. Keep changes focused and well-tested.
3. Follow [PEP 8](https://pep8.org/) style guidelines for Python code.
4. Submit a pull request with a clear description of your changes.

## License

This project is licensed under the [MIT License](LICENSE).

## Author

**Abdullah**
- GitHub: [@vanix056](https://github.com/vanix056)
- Docker Hub: [vanix013](https://hub.docker.com/u/vanix013)
