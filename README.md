# Kubernetes Training

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 8.3.3.  It was created to provide a test container and set of deployment scripts to allow hands on lab work deploying the application into a Kubernetes cluster.  This project helps re-enforce classroom learning provided through the PowerPoint slides and instructor lectures.  As part of this project, students will:

- Review the configuration (YAML) files that make up a Kubernetes deployment
- Understand the Dockerfile configuration and what it does
- Observe the build of a Docker image and deployment to Docker Hub
- Log into the C2 provisioned Google Cloud Kubernetes cluster to deploy the application
- Upgrade and scale the application via configuration
- Observe various kubectl commands and monitoring capabilities built into the platform

## Docker Build

- ng build --prod //compiles the Angular app to static code in the /dist folder
- docker image build -t howieavp76/k8-training-c2 . //builds the Docker image
- docker push howieavp76/k8-training-c2 //push to docker hub image repository
- docker run -p 3000:80 --rm k8-training-c2 //runs the Docker container

**NOTE: Login first to Docker Hub**

- docker login --username=howieavp76

## Deployment

The deployment will be done by executing kubectl commands inside the Google Cloud Shell.  
