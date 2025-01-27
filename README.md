````markdown
# Microservices with Python

This repository provides a hands-on tutorial on building a microservices architecture using Python, Kubernetes, RabbitMQ, MongoDB, and MySQL. It is based on the [freeCodeCamp.org tutorial](https://www.freecodecamp.org) and aims to offer practical experience in developing distributed systems.

## Table of Contents

- [Architecture Overview](#architecture-overview)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Running the Application](#running-the-application)
- [Contributing](#contributing)
- [License](#license)

## Architecture Overview

The application is designed to convert videos into MP3 files through the following workflow:

1. **Authentication**: Users log in via the API Gateway, which communicates with the Auth service to validate credentials stored in a MySQL database and returns an access token.
2. **Video Upload**: Users upload videos through the API Gateway, which stores them in MongoDB and places a message in the RabbitMQ queue indicating a new video is ready for processing.
3. **Conversion**: The Video-to-MP3 service retrieves the video from MongoDB, converts it to MP3 format, and stores the converted file back in MongoDB. It then sends a message to the RabbitMQ queue indicating the conversion is complete.
4. **Notification**: The Notification service listens for messages about completed conversions and sends an email to the user notifying them that their MP3 file is ready.
5. **Download**: Users can download the converted MP3 file through the API Gateway.

## Getting Started

### Prerequisites

Before running the application, ensure you have the following installed:

- **Docker**: [Install Docker](https://docs.docker.com/get-docker/) to build and manage containerized applications.
- **Kubernetes**: [Set up a Kubernetes cluster](https://kubernetes.io/docs/setup/) to orchestrate the deployment of services.
- **RabbitMQ**: Deploy RabbitMQ for message queuing between services.
- **MongoDB**: Deploy MongoDB for storing videos and converted MP3 files.
- **MySQL**: Deploy MySQL for user authentication data.

### Installation

1. **Fork the Repository**:

   - Navigate to the [GitHub repository](https://github.com/DavidDanso/microservices-python).
   - Click the "Fork" button in the top-right corner to create your own copy of the repository.

2. **Clone the Repository**:

   ```bash
   git clone https://github.com/your-username/microservices-python.git
   cd microservices-python
   ```
````

3. **Set Up Environment Variables**:

   Create a `.env` file in the root directory and define the necessary environment variables for each service (e.g., database credentials, RabbitMQ settings).

4. **Build Docker Images**:

   Build the Docker images for each service:

   ```bash
   docker build -t auth-service ./auth
   docker build -t converter-service ./converter
   docker build -t gateway-service ./gateway
   docker build -t notification-service ./notification
   ```

### Running the Application

1. **Start the Kubernetes Cluster**:

   ```bash
   minikube start
   ```

2. **Deploy Services**:

   Apply the Kubernetes configurations for each service:

   ```bash
   kubectl apply -f auth/kubernetes
   kubectl apply -f converter/kubernetes
   kubectl apply -f gateway/kubernetes
   kubectl apply -f notification/kubernetes
   ```

3. **Configure RabbitMQ**:

   After deploying RabbitMQ, create the necessary queues:

   - `video`: Queue for videos awaiting conversion.
   - `mp3`: Queue for notifications of completed conversions.

   Access the RabbitMQ management interface to set up these queues.

4. **Access the Application**:

   Use the API Gateway's external IP to interact with the application. You can obtain the IP address by running:

   ```bash
   minikube service gateway
   ```

5. **Shutdown**:

   Once finished, clean up the environment:

   ```bash
   minikube delete --all
   ```

## Contributing

Contributions are welcome! Please fork this repository and submit a pull request with your improvements.

## License

This project is licensed under the MIT License.

```

*Note: This README is structured to provide a clear and concise overview of the project, its architecture, setup instructions, and contribution guidelines.*
```
