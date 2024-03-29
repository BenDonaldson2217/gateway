Application Structure

The application conists of 14 small microservices. Theses can be split into 6 layers in such a way that anything in one layer only depends on a lower layer. The below diagram shows both the dependencies and the layers.

Set Up
Each microservice is contained in its own github repository, which contains the Dockerfile to build an image for the microservice. The initial set up for all microservices is the same apart from Mongo. The following example runs through the deployment of the dashboard-service microservice. 

Step 1: Clone the git repository.
Run the following command:

git clone https://github.com/BenDonaldson2217/dashboard-service.git

This clones the corresponding repository into your present working directory. This repository contains all the required files for deploying the microservice.

Step 2: Building the docker image.
To build the docker image run:

docker build -t ${yourDockerHubUsername}/dashboard-service .

This builds the dashboard-service image and tags it, allowing for it to be pushed to your dockerhub.

Step 3: Pushing the image.
Run:

docker push ${yourDockerHubUsername}/dashboard-service

This pushs the newly created image to your dockerhub, allowing you to use this image to quickly deploy the service on the cloud.

Step 4: Write deployment and service yaml files.
Write yaml files to deploy the newly created image and allow access to it via the network. Once written apply both to deploy the microservice. 
Note: authentication-service requires an environment variable called ACTIVATION_LINK and email_service needs environment variables called GMAIL_USER, GMMAIL_PASS and SERVICE_NAME. 

Step 5: Mongo
Write deployment and service yaml files to deploy mongo. This is done with the default mongo image instead of a personally created image. This image and service should be named "mongo".

After this is completed, all the microservices are set up and connected.

Redeploying upon updates.

To redeploy and update each microservice as the corresponding github repository is pushed to, we need to set up a jenkins pod in kubernetes. This jenkins will recieve a webhook from any of the repositories which will trigger a rebuild of the corresponding image and then replace the image currently used by the pod with the newer version. 

