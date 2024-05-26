# React App CI/CD Pipeline with Jenkins and Docker

Welcome to the React App CI/CD Pipeline repository! This project demonstrates how to set up a Continuous Integration and Continuous Deployment (CI/CD) pipeline for a React application using Jenkins and Docker. Below, you'll find detailed instructions and explanations for each part of the setup.

## Table of Contents
- Introduction
- Project Structure
- Jenkins Pipeline
- Docker Setup
- Getting Started
- License

## Introduction
This repository contains a Jenkinsfile and a Dockerfile for automating the build, testing, and deployment of a React application. The Jenkins pipeline installs dependencies, builds the Docker image, runs the Docker container, and pushes the image to a Docker registry. The Dockerfile is a multi-stage build that first compiles the React app and then serves it using Nginx.

## Project Structure

├── Jenkinsfile

├── Dockerfile

├── src

│   ├── components

│   ├── App.js

│   ├── index.js

│   └── ...

├── public

│   ├── index.html

│   └── ...

├── package.json

└── ...

**Jenkinsfile:** Contains the Jenkins pipeline configuration.

**Dockerfile:** Defines the Docker image build process.

**src/:** Source code for the React application.

**public/:**  Public assets for the React application.

**package.json:** Node.js dependencies and scripts.

## Jenkins Pipeline

### Jenkinsfile:

pipeline {

    agent any

    stages {
        stage('Dependency Installation') {
            steps {
                bat 'npm install'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t my_image .'
            }
        }
        
        stage('Run Docker Image') {
            steps {
                bat 'docker run -d -p 3000:3001 my_image'
            }
        }
        
        stage('Push Docker Image') {
            steps {
                bat 'docker push my_image'
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed :('
        }
    }
}

### Stages Explanation

**Dependency Installation:** Installs the necessary Node.js dependencies.

**Build Docker Image:** Builds a Docker image for the React app.

**Run Docker Image:** Runs the Docker container.

**Push Docker Image:** Pushes the Docker image to a registry.

**Post Actions**
- _Success:_ Prints a success message.
- _Failure:_ Prints a failure message.

## Docker Setup

### Dockerfile:

FROM node:16 as build

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

RUN npm run build

FROM nginx:stable-alpine

COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

### Explanation

**Build Stage:**

- Uses the official Node.js image.
- Sets the working directory.
- Installs dependencies.
- Copies the source code.
- Builds the React app.
  
**Serve Stage:**

- Uses the official Nginx image.
- Copies the build output to Nginx's HTML directory.
- Exposes port 80.
- Starts Nginx.
 
## Getting Started
To get started with this project, follow these steps:

**Clone the repository:**

git clone https://github.com/yourusername/your-repo.git 

**Set up Jenkins:**

- Install Jenkins and configure it.
- Create a new Jenkins job and use the Jenkinsfile from this repository.

**Build and Run Docker Image Locally:**

- docker build -t my_image .
- docker run -d -p 3000:3001 my_image

**Access the Application:**

Open a web browser and navigate to http://localhost:3000.

## License
This project is licensed under the MIT License. See the LICENSE file for details.
