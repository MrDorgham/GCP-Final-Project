This repository contains Terraform code to set up a GCP environment for a Python app. Below are instructions for setting up the environment.

## **Prerequisites**

- GCP account
- Terraform
- Docker

## **Set Up**

1. To initialize the environment, run `terraform init`.
2. To preview the resources to be created, use `terraform plan`.
3. To create the resources, run `terraform apply`.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/75739d25-fc78-448a-93bb-2d37355416f8/Untitled.png)

## **Building and Uploading Docker Image**

1. Build the Docker image for the Python app with `docker build -t gcp-python-app .`.
2. Tag the Docker image with `docker tag gcp-python gcr.io/careful-trainer-377212/gcp-python-app`.
3. Upload the Docker image to Google Container Registry with `docker push gcr.io/careful-trainer-377212/gcp-python-app`.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b692db97-ff9e-456b-8b6b-d6b873e0b31f/Untitled.png)

## **SSH to Private VM**

1. Install `kubectl` with the following commands:
    - `sudo apt-get update`.
    - `sudo apt-get install kubectl`.
    - `sudo apt-get install google-cloud-sdk-gke-gcloud-auth-plugin`.
2. Authorize `gcloud` to access the Cloud Platform with your Google user credentials by running `gcloud auth login` and `gcloud auth application-default login`.
3. Set the `gcloud` account by running `gcloud conf set account [ACCOUNT]`.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1568213b-9cd2-41a5-98b3-1098f2c8b791/Untitled.png)

## Take a Remote of the Private GKE Cluster

1. SSH to GKE with `gcloud container clusters get-credentials private-cluster --region us-east1-b --project careful-trainer-377212`.
2. Copy the `gke_deployment_files` directory to the remote machine with `git clone <HTTP URL>` after installing `git`:
    - `sudo apt install git`.

## **Deploy to GKE**

1. Apply the Kubernetes deployment and service configurations with `kubectl create -Rf .`.
2. Get the load balancer IP and port with `kubectl get svc`. This will provide you with the external IP address and the port of the service. 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c8b5fae3-8f66-4d33-bdf3-4a01b499c101/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5ca79cf8-07f0-419b-b3cd-5fb71350e586/Untitled.png)
