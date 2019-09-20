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

# Deployment

The deployment will be done by executing kubectl commands inside the Google Cloud Shell.  The steps are as follows:

### Step 1
 
Log into Kubernetes Engine on Google Cloud Platform:
 
1) Navigate to the [Google Cloud Platform URL](https://console.cloud.google.com)
2) You will need a Google account (or to create a new one for this Lab)
3) Once registered, navigate in the menu to Compute -> Kubernetes Engine
4) Find the entergy-k8-c2 cluster and click "Connect"
5) Click "Run in Cloud Shell" to open the CLI prompt
6) If prompted, click "Start Cloud Shell"
7) It should load a command to start the shell, press Enter to execute the command
8) You should not have interactive login to Google Cloud and the Kubernetes cluster

### Step 2

Deploy our demo app into the Kubernetes cluster in a highly available configuration with 3 nodes:

1) Access the deployment at https://atlasc2.blob.core.windows.net/kub8-c2labs/k8training-deployment.yaml
2) Each student will have their own file; for example; https://atlasc2.blob.core.windows.net/kub8-c2labs/k8training-deployment-student1.yaml
3) We will number off in class and you will grab the appropriate file for your number (up to 12 available)
4) Execute the following command in Google Cloud Shell: kubectl apply -f https://atlasc2.blob.core.windows.net/kub8-c2labs/k8training-deployment-student#.yaml
5) The console should show the deployment created along with two services
    - Deployment - will create the specified number of pods
    - Service - allows internal traffic in the cluster
    - Load Balancer Service - creates external IP and load balances requests evenly across the pods created
6) Verify your pods are running: kubectl get pods
7) Verify your services are running: kubectl ger services
8) On the services, find the external IP of the Load Balancer service in the console log
9) Paste the IP into your browser to see the running app
10) Do the #HappyDance if it worked

# NOTES

You can run into some tricky issues that are not well explained online or in any tutorials.  A few of these issues are shown below:

1) Just deploying your container into pods won't work.  You have to create the load balancer service to externally expose the IP so you can reach it from outside the Kubernetes cluster.
2) Not just any URL can be used to point at the YAML file.  In particular, you cannot use a GitHub link to provide the YAML file.  If you do, it throws the following error:

` error: error parsing https://github.com/howieavp76/k8-training-c2/blob/master/k8training-deployment.yaml: error converting YAML to JSON: yaml: line 616: mapping values are not allowed in this context `

3) This error appears to happen on any GitHub YAML related link.  Copying the same file to a S3 bucket or Azure blob resolves the issue.
4) YAML formatting errors can be really hard to see and debug.  If your deploy fails due to a format/syntax issue, it can take forever to find it.  Online linting tools really help.  For example, you can go to [YAMLLINT](http:www.yamllint.com) for an online validator of your YAML format.
