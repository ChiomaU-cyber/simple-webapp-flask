Simple Flask Web Application with CI/CD and Kubernetes Deployment 

This project demonstrates the development of a Simple Flask web application, which is containerized using Docker, deployed to a Kubernetes cluster, and integrated with a GitHub Actions CI/CD pipeline to automate building, testing, and deployment. Basic security practices are implemented to safeguard the application. 

Table of Contents 

Project Description 

Project Structure 

Prerequisites 

Local Development 

Docker Instructions 

Kubernetes Deployment 

CI/CD Pipeline 

Security Measures 

Project Summary 

 

Project Description 

This project involves building a simple API with Flask that responds to basic HTTP requests. The Flask app is containerized using Docker and deployed to a Kubernetes cluster. The CI/CD pipeline, implemented via GitHub Actions, automates the process of building the Docker image, pushing it to a container registry, and deploying it to the Kubernetes cluster. 

 

Project Structure 

bash 

simple-webapp-flask/ 
├── app.py                     # Flask web app code 
├── Dockerfile                 # Dockerfile for containerization 
├── requirements.txt           # Python dependencies 
├── README.md                  # Project documentation 
├── .github/                   # GitHub Actions workflows 
│   └── workflows/ 
│       └── ci-cd-pipeline.yml # CI/CD pipeline configuration 
└── k8s/                       # Kubernetes manifests 
    ├── deployment.yaml        # Kubernetes deployment manifest 
    └── service.yaml           # Kubernetes service manifest 

└── network.policy.yaml   # Kubernetes network.policy manifest 
 

 

Prerequisites 

Ensure the following tools are installed on your machine: 

Python 3.11.9 

Docker 

KinD (Kubernetes in Docker) 

GitHub Account (for CI/CD pipeline) 

Git (version control) 

 

Local Development 

Step 1: Clone the Repository 

Clone the repository to your local environment: 

bash 

Copy code 

git clone https://github.com/your-username/simple-webapp-flask.git 
cd simple-webapp-flask 
 

Step 2: Install Dependencies 

Install the required dependencies: 

bash 

Copy code 

pip install -r requirements.txt 
 

Step 3: Run the Application Locally 

Run the Flask application locally: 

bash 

Copy code 

python app.py 
 

The application will be accessible at http://localhost:8080. 

 

Docker Instructions 

Step 1: Build Docker Image 

Build the Docker image: 

bash 

Copy code 

docker build -t your-docker-repo/simple-flask-app:latest . 
 

Step 2: Run the Docker Container 

Run the Docker container: 

bash 

Copy code 

docker run -p 8080:8080 your-docker-repo/simple-flask-app:latest 
 

Access the Flask app at http://localhost:8080. 

Step 3: Push Docker Image to a Registry 

Push the image to Docker Hub or GitHub Packages: 

bash 

Copy code 

docker login 
docker tag simple-flask-app:latest your-docker-repo/simple-flask-app:latest 
docker push your-docker-repo/simple-flask-app:latest 
 

 

Kubernetes Deployment 

Step 1: Create a Kubernetes Cluster with KinD 

Create a local Kubernetes cluster using KinD: 

bash 

Copy code 

kind create cluster 
 

Step 2: Apply Kubernetes Manifests 

Deploy the application by applying the manifests in the k8s/ directory: 

bash 

Copy code 

kubectl apply -f k8s/deployment.yaml 
kubectl apply -f k8s/service.yaml 
 

Step 3: Verify the Deployment 

Verify the deployment status: 

bash 

Copy code 

kubectl get pods 
kubectl get services 
 

The Flask app should be running in a pod, and the service should expose it. 

 

CI/CD Pipeline 

Step 1: GitHub Actions Configuration 

The .github/workflows/ci-cd-pipeline.yml file automates the CI/CD process: 

CI: Builds and pushes the Docker image to the container registry. 

CD: Deploys the app to the Kubernetes cluster using kubectl. 

The pipeline runs automatically on every push to the main branch. 

 

Security Measures 

Container Security: 

Used an official slim base image (python:3.11.9) to reduce vulnerabilities. 

Set appropriate user permissions inside the container. 

Kubernetes Security: 

Configured resource limits (CPU/Memory) in the deployment manifest to prevent overuse. 

Applied best practices in securing Kubernetes resources. 

 

Project Summary 

API Functionality 

The API is built using Flask and offers two basic endpoints: 

/: Displays a welcome message. 

/how-are-you: Responds with a friendly message. 

How the API Was Containerized 

A Dockerfile was created using Python as the base image. 

Application files (app.py, requirements.txt) were copied into the container. 

Flask was installed inside the container, and the app was exposed on port 8080. 

CI/CD Process Explanation 

Continuous Integration (CI): On every push to the main branch, GitHub Actions builds the Docker image, tags it, and pushes it to Docker Hub. 

Continuous Deployment (CD): The pipeline deploys the application to a Kubernetes cluster using kubectl. 

How the API Was Deployed on Kubernetes 

The deployment manifest (deployment.yaml) specifies the number of replicas and the Docker image for the Flask app. 

The service manifest (service.yaml) exposes the app via a load balancer for external access. 

Security Measures Implemented 

Used a minimal Docker base image to reduce vulnerabilities. 

Configured Kubernetes resource requests and limits to secure the environment.
