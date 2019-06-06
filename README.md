Application Structure

The application conists of 14 small microservices. Theses can be split into 6 layers in such a way that anything in one layer only depends on a lower layer. The below diagram shows both the dependencies and the layers.

Set Up
Each microservice is contained in its own github repository, which contains the Dockerfile to build an image for the microservice. The initial set up for all microservices is the same apart from Mongo and Gateway. The following example runs through the deployment of the dashboard-service microservice. 

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
Write yaml files to deploy the newly created image and allow access to it via the network. Once written apply both
