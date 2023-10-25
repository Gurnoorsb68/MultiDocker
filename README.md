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
