# ORAAS DB Mock

`oraas-db-mock` is a lightweight mock database service created for the ORAAS (Operational Reporting as a Service) ecosystem. It simulates the database interactions required by dependent microservices, allowing developers and testers to run, integrate, and validate workflows without relying on a real database.

This mock service is ideal for:
- Local development without database dependencies  
- CI/CD pipelines  
- Unit testing and integration testing  
- API simulations  
- Sandbox/demo environment setup  

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Directory Structure](#directory-structure)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Running the Service](#running-the-service)
- [Configuration](#configuration)
- [Usage](#usage)
- [Mock Data](#mock-data)
- [Testing](#testing)
- [Docker Support](#docker-support)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

## Overview

`oraas-db-mock` serves as a stand-in for the ORAAS database, responding to queries with static or simulated data. It helps developers build and test applications that depend on ORAAS without requiring access to the production or staging DB.

This mock DB service can simulate:
- Data fetch operations  
- Static dataset responses  
- Basic CRUD-like mock behaviors  
- Query emulation for ORAAS flows  

---

## Features

- Easy-to-run standalone mock database server  
- Preloaded mock ORAAS dataset  
- Fast and lightweight  
- Customizable data files  
- Ideal for development and test environments  
- Docker-ready  

---

## Tech Stack

- **Language:** Python  
- **API Framework:** Lightweight HTTP server (Flask/FastAPI depending on repo implementation)  
- **Data Storage:** JSON/mock in-memory structures  
- **Containerization:** Docker  

---

## Architecture

The service acts as a simple API layer over mocked DB responses:

┌───────────────────────────────┐
│ ORAAS Client Application │
└───────────────┬───────────────┘
│ HTTP Requests
▼
┌───────────────────────────────┐
│ ORAAS DB Mock │
│ - Returns mock JSON data │
│ - Simulates DB responses │
└───────────────┬───────────────┘
│
▼
Mock Data Storage

yaml


---

## Directory Structure

oraas-db-mock/
│
├── main.py # Entry point of the mock DB service
├── data/ # Folder containing mock JSON datasets
├── config/ # Configuration files
├── utils/ # Helper utilities
├── requirements.txt # Python packages
└── Dockerfile # Docker build instructions

yaml


---

## Getting Started

### Prerequisites

- Python 3.7+  
- `pip`  
- Docker (optional)  

---

## Installation

Clone the repository:

```bash
git clone https://github.com/simpsonorg/oraas-db-mock.git
cd oraas-db-mock
Install dependencies:

bash

pip install -r requirements.txt
Running the Service
Start the mock DB service:

bash

python main.py
This starts a local server (port may vary based on code).

Configuration
Environment variables or config files may be used (depending on repository):

Variable	Description	Default
PORT	Port for the mock server	8080
MOCK_DATA_DIR	Directory for mock JSON files	./data

Example .env:

ini

PORT=9090
MOCK_DATA_DIR=./data
Usage
After running, you can hit endpoints like:

bash

GET /records
GET /records/{id}
GET /oraas/data
Example response:

json

{
  "id": "A123",
  "status": "ACTIVE",
  "type": "ORAAS_RECORD",
  "timestamp": "2025-01-20T12:00:00Z"
}
You can customize mock data inside the data/ directory.

Mock Data
All mock responses are stored inside the data/ directory as JSON files.

You can:

Add new mock data

Modify existing JSON files

Introduce new response patterns

This allows you to simulate real ORAAS query behavior without a real database.

Testing
You can test the mock endpoints using:

bash

curl http://localhost:8080/records
Or run automated tests (if present):

bash

pytest
Docker Support
Build the Docker image:

bash
docker build -t oraas-db-mock .
Run the container:

bash
docker run -p 8080:8080 oraas-db-mock
With environment variables:

bash

docker run -e PORT=9090 -e MOCK_DATA_DIR=/app/data -p 9090:9090 oraas-db-mock
Contributing
Contributions are welcome!

Fork the repository

Create a feature branch

Commit changes with clear messages

Open a pull request

License
This project is licensed under the Citi License.
