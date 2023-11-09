# Multi-Container Docker Project

This project consists of multiple components, including a client, server, and worker, each running in separate Docker containers. These components are deployed on an AWS Elastic Beanstalk instance. The project uses AWS RDS for PostgreSQL and AWS Elasticache for Redis to store values.

## Overview

- Client: A user interface for input and visualization.
- Server: A backend service for handling data and business logic.
- Worker: A background worker for processing and calculating values.
- AWS Elastic Beanstalk: The platform for deploying and scaling the project.
- AWS RDS (PostgreSQL): A relational database for data storage.
- AWS Elasticache (Redis): A cache for efficient data retrieval.

## Features

- **Client**: Provides a user-friendly interface for entering values and viewing results.
- **Server**: Serves as an API to handle data, calculations, and communication with the worker.
- **Worker**: Performs background calculations for Fibonacci sequences and stores results.
- **AWS Elastic Beanstalk**: Offers automated deployment, scaling, and monitoring.
- **AWS RDS (PostgreSQL)**: Stores data related to the application.
- **AWS Elasticache (Redis)**: Stores and retrieves values efficiently for the worker.


## Working

Multi-Docker Development Version
We will be using 4 Docker containers:

1. Client
Contains frontend React files in the src directory.
Includes an Nginx server that listens on port 3000, serving index.html for the / route.
2. Server
Accessed via the route /api.
index.js contains the initial setup for Redis and Postgres, with keys stored in keys.js.
Stores values in Postgres and the worker.
3. Nginx
Listens on port 80 and routes traffic to port 3000 (client) or 5000 (server).
4. Worker
Performs calculations for the Fibonacci series and sends the values to Redis.

Build All Images Command:
bash
Copy code
docker build -t multi-client -f Dockerfile.dev .
docker build -t multi-server -f Dockerfile.dev .
docker build -t multi-nginx -f Dockerfile.dev .
docker build -t multi-worker -f Dockerfile.dev .
Run All Containers on the Same Network:

Create network:
docker network create my-network

Run containers:
docker run -d -p 8000:80 --network my-network --name nginx6 multi-nginx
docker run -d --network my-network --name server multi-server
docker run -d --network my-network --name client multi-client
docker run -d --network my-network --name worker multi-worker

Also, run images for Redis and Postgres:
docker run -d redis
docker run -d postgres

Alternatively, use docker-compose-dev.yml:
docker-compose -f docker-compose-dev.yml up

## For Production
Use Dockerfiles instead of Dockerfile.dev.

Deploy using deploy.yaml for GitActions and AWS Beanstalk

Build and push images to DockerHub.
AWS Beanstalk uses the zip file, utilizing docker-compose.yaml.
Important: Run Postgres and Redis instances on separate AWS instances and set environment variables.

Note: While working with Docker Compose locally, Elastic Beanstalk uses Docker-compose to create and manage containers.

After Deployment:
AWS Elastic Beanstalk translates the Docker Compose configuration into a Dockerrun.aws.json file for deployment. This file defines how Elastic Beanstalk should run containers on AWS using ECS.


