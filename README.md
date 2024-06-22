# This repository has scripts to create Dockerfile and creation on Flask App with EKS deployment and Load balancer

A Flask App with my portfolio has been deployed to [aac7776be0bfd47caafd0e0468cf0237-1596588144.us-east-1.elb.amazonaws.com](aac7776be0bfd47caafd0e0468cf0237-1596588144.us-east-1.elb.amazonaws.com)


Steps Taken : 

1. Create a Flask App- Resume Portfolio.
2. Dockerize the Flask APP.
3. Expose the necessary ports in Docker.
4. Test the Docker Image locally 
5. Build Docker image and push it to Docker Hub, make the registry Private.
6. Install eksctl and Kubectl.
7. Create Clustur on EKS with named group using configuration file 
8. Later create the deployment file with replaicas for pods
9: Provide suitable permissions and secrets to pull the private docker image
10: Create the service as a load balancer



Debugging : 
** When Deployed the pods were going in a CrashBackLoop **

Ways to troubleshhot: 
1) Kubetcl describe <pod name>
2) Look at logs for the pods Kubectl logs <pod name>

Kubect logs gave me ->   Python "exec /usr/local/bin/python3: exec format error".

Took some investigation : 
When building docker images locally on macos it uses the executable for ARM 64 where as AWS EC2 instances run on AMD 64.
** Resolution was to force docker to use the AMD 64 in Docker File  FROM --platform=linux/amd64  python:3.8-slim-buster  on Docker while using Apple M1 Max **


Currently the Website runs with 4 replica pods and 2 worker nodes for fault tolerance and high avalibility.
