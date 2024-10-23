# Vercel
### Setup Guide

This Project contains following services and folders:

- `api-server`: HTTP API Server for REST API's
- `build-server`: Docker Image code which clones, builds and pushes the build to S3
- `s3-reverse-proxy`: Reverse Proxy the subdomains and domains to s3 bucket static assets

### Local Setup

1. Run `npm install` in all the 3 services i.e. `api-server`, `build-server` and `s3-reverse-proxy`
2. Docker build the `build-server` and push the image to AWS ECR.
3. Setup the `api-server` by providing all the required config such as TASK ARN and CLUSTER arn.
4. Run `node index.js` in `api-server` and `s3-reverse-proxy`

At this point following services would be up and running:

| S.No | Service            | PORT    |
| ---- | ------------------ | ------- |
| 1    | `api-server`       | `:9000` |
| 2    | `socket.io-server` | `:9002` |
| 3    | `s3-reverse-proxy` | `:8000` |

### Demo

[Watch The Demo Video](https://imgur.com/I6KgmNR)

### Architecture

![Vercel Clone Architecture](https://i.imgur.com/r7QUXqZ.png)


Here's the updated README with the log viewing feature included:

---

# Vercel Clone - Part 2: Scalable Deployment System

## Overview

This is Part 2 of the Vercel-like platform project, where the system is scaled using **Kafka**, **ClickHouse**, **Postgres**, and a **Log Collection Pipeline**. The platform automates the process of deploying projects by providing a GitHub URL and now includes **real-time log viewing** on the frontend, showing every step of the deployment process. The architecture ensures high availability, scalability, and detailed monitoring of deployments.

## Features

- **Automated Deployment**: Simply provide a GitHub URL, and the system will automatically build and deploy the project.
- **Real-Time Log Viewing**: The frontend displays logs of all activities that happen after the submission of the GitHub URL, offering transparency during the build and deployment process.
- **Scalability with Kafka**: Event-driven architecture ensures that the platform scales efficiently with high demand.
- **Data Storage with ClickHouse and Postgres**: ClickHouse is used for fast log processing, while Postgres handles transactional data.
- **Log Collection Pipeline**: A robust pipeline collects, stores, and analyzes logs from deployments, with real-time access on the frontend.
- **AWS for Infrastructure**: Built using AWS services like EC2, S3, and Lambda.
- **Dockerized Microservices**: All services are containerized for consistency and ease of deployment.
- **Redis for Caching**: Improves performance with cached data.
- **Next.js**: Provides server-side rendering for a modern, responsive frontend.

## Tech Stack

- **System Design**: Optimized for scalability, fault tolerance, and reliability.
- **AWS**: 
  - EC2 for hosting services.
  - S3 for file and asset storage.
  - Lambda for serverless functions.
- **Docker**: All microservices are containerized for consistency and ease of management.
- **Redis**: Caches frequently accessed data for faster response times.
- **Kafka**: Manages the event-driven system to handle real-time communication between services.
- **ClickHouse**: High-performance data storage optimized for real-time log analytics.
- **Postgres**: Relational database for transactional data storage.
- **Next.js**: Used for the frontend, offering server-side rendering and a modern, responsive user experience.

## Key Additions in Part 2

1. **Kafka for Event-Driven Architecture**:
   - Kafka is utilized to decouple services and handle large volumes of asynchronous operations for scalable deployments.

2. **ClickHouse for Log Analytics**:
   - Logs generated during the deployment process are collected and stored in ClickHouse, allowing for fast querying and analysis.

3. **Postgres for Transactional Data**:
   - Postgres stores core application data like user details, deployment metadata, and project information.

4. **Real-Time Log Collection and Viewing**:
   - Logs from all stages of the deployment process are collected and displayed in real-time on the frontend, allowing users to track every action taken after submitting the GitHub URL.

## Setup and Installation

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/vercel-clone-part-2.git
cd vercel-clone-part-2
```

### 2. Install Dependencies

Install the necessary dependencies using npm or yarn:

```bash
npm install
# or
yarn install
```

### 3. Set Up Environment Variables

Create a `.env` file and add the necessary environment variables for Kafka, Redis, AWS, Postgres, and ClickHouse:

```bash
AWS_ACCESS_KEY_ID=<your-access-key>
AWS_SECRET_ACCESS_KEY=<your-secret-key>
REDIS_URL=<your-redis-url>
KAFKA_BROKER_URL=<your-kafka-broker-url>
CLICKHOUSE_URL=<your-clickhouse-url>
POSTGRES_URL=<your-postgres-url>
```

### 4. Run Docker Containers

Make sure Docker is installed. Use `docker-compose` to set up and run all services:

```bash
docker-compose up --build
```

This will start Kafka, Postgres, ClickHouse, Redis, and other necessary services.

### 5. Start the Application

Run the application locally:

```bash
npm run dev
```

The application will be available at `http://localhost:3000`.

## How It Works

1. **Submit GitHub URL**: The user provides a GitHub repository URL via the UI.
2. **Event Processing**: Kafka handles the event-driven communication and distributes tasks to various services.
3. **Deployment Process**: The system automatically builds the project inside Docker containers and deploys it using AWS infrastructure.
4. **Real-Time Logs**: Logs of the entire process (from fetching the repository to deployment) are shown on the frontend in real-time.
5. **Log Collection Pipeline**: Logs are processed and stored in ClickHouse, providing real-time insights into the deployment process.
6. **Data Storage**: Postgres stores metadata related to users, projects, and deployments, while ClickHouse stores detailed logs for fast access.

## Future Enhancements

- **Custom Deployment Strategies**: Support for blue-green or canary deployments.
- **Expanded Cloud Provider Support**: Add support for cloud providers beyond AWS, such as GCP or Azure.
- **Advanced Monitoring and Analytics**: Build dashboards for deeper insights into system health, performance, and user activity.
- **Load Balancing**: Implement dynamic load balancing for even more scalable deployments.

## Contributing

Contributions are welcome! Feel free to submit pull requests or open issues to report bugs or suggest new features.
---

This updated README includes the addition of **real-time log viewing** on the frontend, helping users track every step of their deployment process. Let me know if you need further customization!
