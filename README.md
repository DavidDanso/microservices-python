# Python Microservices Video-to-MP3 Converter

Convert video files to MP3 format using a distributed microservices architecture. Built with Python, Kubernetes, RabbitMQ, MongoDB, and MySQL.

## System Architecture

- **API Gateway**: Entry point for all client requests
- **Auth Service**: Handles user authentication (MySQL)
- **Converter Service**: Processes video to MP3 conversion
- **Notification Service**: Sends conversion completion emails
- **Storage**: MongoDB for videos/MP3s, MySQL for user data
- **Message Queue**: RabbitMQ for service communication

## Quick Start

### Prerequisites

- Docker
- Kubernetes cluster
- kubectl CLI
- Git

### Clone and Setup

```bash
# Clone repository
git clone https://github.com/DavidDanso/microservices-python.git
cd microservices-python

# Create environment file
cp .env.example .env
# Edit .env with your configurations
```

### Deploy Services

```bash
# Start Kubernetes
minikube start

# Deploy core services
kubectl apply -f k8s/

# Verify deployments
kubectl get pods
kubectl get services
```

### Environment Variables

Required variables in `.env`:

```
# Auth Service
AUTH_DB_HOST=
AUTH_DB_USER=
AUTH_DB_PASSWORD=
AUTH_DB_NAME=

# RabbitMQ
RABBITMQ_HOST=
RABBITMQ_USER=
RABBITMQ_PASSWORD=

# MongoDB
MONGO_HOST=
MONGO_USER=
MONGO_PASSWORD=
```

## API Endpoints

### Authentication

- POST `/auth/login`: User login
- POST `/auth/register`: Create account

### Video Processing

- POST `/upload`: Upload video file
- GET `/download/{file_id}`: Download converted MP3
- GET `/status/{file_id}`: Check conversion status

## Development Setup

1. Install development dependencies:

```bash
pip install -r requirements-dev.txt
```

2. Run tests:

```bash
pytest tests/
```

3. Local development with Docker Compose:

```bash
docker-compose up --build
```

## Monitoring

Access service metrics:

- RabbitMQ Dashboard: `http://localhost:15672`
- Kubernetes Dashboard: `minikube dashboard`

## Common Issues

1. **Services not connecting**: Check network policies and service DNS names
2. **Conversion failing**: Verify ffmpeg installation in converter service
3. **Queue backup**: Monitor RabbitMQ memory usage and consumer count

## Contributing

1. Fork repository
2. Create feature branch: `git checkout -b feature-name`
3. Commit changes: `git commit -am 'Add feature'`
4. Push branch: `git push origin feature-name`
5. Submit pull request

Last updated: January 2025
