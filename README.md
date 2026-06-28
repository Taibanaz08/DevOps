# AWS Infrastructure & CI/CD Pipeline Project

## Project Overview

This project demonstrates a complete DevOps CI/CD pipeline.

The application source code is stored in GitHub. Jenkins automatically pulls the latest code, builds a Docker image, pushes the image to Docker Hub, and deploys the application to Kubernetes using deployment and service manifests.

---

# Architecture

The following diagram shows the complete CI/CD workflow of this project.
![](screenshots/architecture-diagram.png)

Developer
↓
GitHub
↓
Jenkins
↓
Docker Build
↓
Docker Hub
↓
Kubernetes Deployment
↓
Kubernetes Service
↓
Users

---

# Technologies Used

- Git & Github
- Jenkins
- Git & GitHub
- Docker
- Docker Hub
- Kubernetes (Kind)
- Nginx

---

# Project Workflow

1. Developer pushes code to GitHub.
2. Jenkins pulls the latest code.
3. Jenkins builds the Docker image.
4. Jenkins logs into Docker Hub.
5. Docker image is pushed to Docker Hub.
6. Kubernetes deploys the latest image.
7. Service exposes the application.
8. Users access the deployed application.

---

# Project Files

- Dockerfile
- Jenkinsfile
- deployment.yaml
- service.yaml
- pod.yaml
- README.md

---

# Screenshots

## Docker Images

Shows the Docker image created for this project.

![](screenshots/docker-images.png)

---

## Jenkins Pipeline Success

Shows the successful Jenkins pipeline execution.

![](screenshots/jenkins-pipeline.png)

---

## Kubernetes Pods

Shows all running Kubernetes Pods.

![](screenshots/k8s-pods.png)

---

## Kubernetes Deployment

Shows the deployment created in Kubernetes.

![](screenshots/k8s-deployment.png)

---

## Kubernetes Service

Shows the Kubernetes service exposing the application.

![](screenshots/k8s-service.png)

---

## Application Output

Shows the application running successfully.

![](screenshots/application-output.png)

---

# Components Explanation

## GitHub

Stores the application source code.

## Jenkins

Automates the CI/CD pipeline.

## Docker

Packages the application into a container image.

## Docker Hub

Stores Docker images.

## Kubernetes

Deploys and manages containerized applications.

## Deployment

Maintains the desired number of Pods.

## Service

Exposes the application for users.

---
Questions and Answers

Part 1 - Docker Fundamentals

Q1. What problem does Docker solve?

Docker provides a consistent environment so applications work the same on every machine.

Q2. Difference between VM and Container?

Virtual Machines include a complete operating system, while Containers share the host OS and are lightweight.

Q3. What is an Image?

A Docker Image is a template used to create containers.

Q4. What is a Container?

A Container is a running instance of a Docker Image.

Q5. What happens if a container is deleted?

The container is removed, but the Docker Image remains available.

---

Part 2 - Docker Operations

Q6. Difference between Image and Container?

Image is a blueprint. Container is the running instance of that blueprint.

Q7. Difference between docker stop and docker rm?

docker stop stops a running container.

docker rm permanently removes a container.

Q8. Where are container logs stored?

Container logs are stored inside Docker's storage directory on the host machine and can be viewed using:

docker logs <container-name>

---

Part 3 - Docker Volumes

Q9. Why are volumes needed?

Volumes store data permanently, even if the container is deleted.

Q10. What happens without volumes?

All application data is lost when the container is removed.

Q11. Difference between Volume and Bind Mount?

Volume is managed by Docker.

Bind Mount uses a specific host machine directory.

---

Part 4 - Docker Networking

Q12. Why use custom networks?

Custom networks allow containers to communicate securely using container names.

Q13. Difference between bridge and host network?

Bridge network provides isolated networking.

Host network shares the host machine's network directly.

Q14. How do containers communicate?

Containers communicate through Docker networks using container names or IP addresses.

---

Part 5 - Jenkins Installation

Q15. What is Jenkins?

Jenkins is an automation server used to build, test and deploy applications automatically.

Q16. What problem does Jenkins solve?

It automates repetitive software delivery tasks and reduces manual work.

Q17. Difference between CI and CD?

CI (Continuous Integration) automatically builds and tests code.

CD (Continuous Delivery/Deployment) automatically deploys applications after successful builds.

Q18. What is a Jenkins Pipeline?

Answer:
A Jenkins Pipeline is a sequence of automated stages that build, test, and deploy an application using a Jenkinsfile.

Q19. Why use pipelines instead of manual deployments?

Answer:
Pipelines automate the deployment process, reduce human errors, save time, and ensure consistent deployments.

Q20. Difference between Freestyle and Pipeline jobs?

Answer:

Freestyle Job| Pipeline Job
Configured using Jenkins UI| Defined in a Jenkinsfile
Difficult to maintain| Easy to maintain and version control
Limited flexibility| Highly flexible and reusable

Q21. Why use a registry?

Answer:
A container registry stores Docker images so they can be shared, downloaded, and deployed from any system.

Q22. Difference between local image and registry image?

Answer:

Local Image| Registry Image
Stored on local machine| Stored in Docker Hub or another registry
Accessible only locally| Accessible from anywhere
Used for local testing| Used for deployment and sharing

Q23. Why not build images directly on production servers?

Answer:
Building images on production servers consumes resources, increases security risks, and may affect running applications. Images should be built in CI/CD pipelines and deployed to production.

Q24. What is Kubernetes?

Answer:
Kubernetes is a container orchestration platform that automates container deployment, scaling, load balancing, and management.

Q25. Why not run containers directly?

Answer:
Running containers directly does not provide auto-healing, scaling, load balancing, or easy management. Kubernetes provides all these features.

Q26. What problems does Kubernetes solve?

Answer:
Kubernetes solves container management problems such as automatic deployment, scaling, load balancing, self-healing, and high availability.

---

Part 9 - Pods

Q27. What is a Pod?

Answer:
A Pod is the smallest deployable unit in Kubernetes. It contains one or more containers that share the same network and storage.

Q28. Why doesn't Kubernetes deploy containers directly?

Answer:
Kubernetes deploys Pods instead of individual containers because Pods provide networking, storage, and lifecycle management for containers.

Q29. Can a Pod contain multiple containers?

Answer:
Yes. A Pod can contain one or more containers that work together and share the same network and storage.

---

Part 10 - Deployments

Q30. Why did the Pod return automatically?

Answer:
The Pod was recreated automatically because the Deployment maintains the desired number of replicas.

Q31. Difference between Pod and Deployment?

Pod| Deployment
Runs one or more containers| Manages Pods
Can fail permanently| Automatically recreates failed Pods
Not self-managing| Supports scaling and rolling updates

Q32. What is desired state?

Answer:
Desired state is the expected state defined by the user, such as the number of replicas or container image. Kubernetes continuously works to maintain this state.

---

Part 11 - Services

Q33. Why do Pods need Services?

Answer:
Pods need Services because Pod IP addresses can change. A Service provides a stable IP address and DNS name for accessing Pods.

Q34. Difference between ClusterIP and NodePort?

ClusterIP| NodePort
Accessible only inside the cluster| Accessible from outside the cluster
Default Service type| Exposes the application using a node port

Q35. What happens when Pod IP changes?

Answer:
The Service automatically forwards traffic to the new Pod IP, so users can still access the application without interruption.

---

Part 12 - Rolling Updates

Q36. What is a rolling update?

Answer:
A rolling update gradually replaces old Pods with new Pods without stopping the application.

Q37. Why is rolling update safer?

Answer:
It updates Pods one by one, reducing downtime and allowing quick recovery if an issue occurs.

Q38. What is zero downtime deployment?

Answer:
Zero downtime deployment means the application remains available to users while a new version is being deployed.

---

Part 13 - Rollback

Q39. Why are rollbacks important?

Answer:
Rollbacks allow the application to quickly return to the previous stable version if the new deployment fails.

Q40. How does Kubernetes maintain availability?

Answer:
Kubernetes maintains availability by monitoring Pods, restarting failed Pods, replacing unhealthy Pods, and distributing traffic across healthy Pods.

---

Part 14 - Jenkins + Kubernetes Integration

Q41. How does Jenkins communicate with Kubernetes?

Answer:
Jenkins communicates with Kubernetes using the "kubectl" command and Kubernetes configuration (kubeconfig) to deploy and manage resources.

Q42. Why automate deployments?

Answer:
Automation makes deployments faster, more reliable, consistent, and reduces manual errors.

Q43. What risks exist in manual deployments?

Answer:
Manual deployments can cause human errors, inconsistent configurations, longer deployment times, and increased downtime.