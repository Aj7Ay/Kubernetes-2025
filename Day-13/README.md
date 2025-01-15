## Day 13

Blog : https://mrcloudbook.com/how-to-create-kubernetes-pods-day-13/

<div align="center"> <img src="https://github.com/Aj7Ay/Kubernetes-2025/blob/main/Day-13/k8s-yt13.png"> </div>

Level 1: Easy Tasks

    Create a Pod using YAML
    Write a YAML file to create a Pod named simple-pod running an nginx container.
    Image: nginx:latest

    List All Pods
    Use the kubectl command to list all Pods running in the default namespace.

    Delete a Pod
    Delete a Pod named simple-pod using a single kubectl command.

    Describe a Pod
    Run a command to describe the simple-pod and review its events.

Level 2: Advanced Tasks

    Run a Pod with Environment Variables
    Create a YAML definition for a Pod named env-pod that passes the following environment variables to the container:
        APP_NAME=demo-app
        ENV=production

    Run a Multi-Container Pod
    Write a YAML file to create a Pod named multi-container-pod with two containers:
        nginx serving on port 80
        busybox running a simple sleep 3600 command

    Run a Pod with a Custom Command
    Create a Pod named command-pod running a busybox container. The container should run the command echo "Hello Kubernetes".
