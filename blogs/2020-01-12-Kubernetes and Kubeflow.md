Let's start with some basic concepts and go to Kubernetes and Kubeflow later. 

## Microservices:
Microservices are an architectural approach to building applications where multiple pieces of an app work independently while together. They have the following characteristics:
- separate business logic functions
- instead of one big program, several smaller applications
- communicate via well defined APIs - usually HTTP
- works in demand

Monolithic architecture versus microservices architecture

![](2020-08-30-16-05-02.png)

Advantages of Microservices:
- language independent (microservices commuicate via HTTP)
- fast iterations
- small teams (smaller projects --> smaller teams)
- fault isolation (one fail, won't intervene other microservices)
- pair well with containers
- SCALABLE (big plus, can scale up or down in demand)

Disadvantages of Microservices:
- complex networking (many microservices communicate with each other, big and complicated network)
- overhead (need to know the architecture to organize and orchestrate things, dynamically spin up databases, containanization)

## Docker
Docker is an open platform for developers and sysadmins to build, ship and deliver software in packages called containers, whether on laptops, data center virtual machines, or the cloud.
Containers are a way to package software in a format that can run isolated on a shared operating system. Unlike virtual machines, containers do not bundle a full operating system -- only libraries and settings required to make the software work are needed.

![](2020-08-30-16-16-42.png)

Containers can share bins and libraries.
Once an app is built, add a Dockerfile into the app folder to create an image of the app.

## Kubernetes
Container orchestration (deploying and scaling containers )

Kubernetes is an open-source system for automating deployment, scaling, and management of containerized applications.

![](2020-08-30-16-24-52.png)
![](2020-08-30-16-33-54.png)

- If a pod gets deleted or failed, Kubernetes will automatically create a new pod. 
- It can be scaled up or down very easily by creating or deleting some pods.
- It also provides a friendly GUI called dashboard to allow user-friendly operations of the Kubernetes cluster.

### Deploy Docker container in Kubernetes
It requires a separate Yaml file in the app folder which includes all deployment parameters for deployment 
An example file directory looks like the following:

![](2020-08-30-17-13-19.png)

Spin up a Kubernetes cluster --> Download the image from the Dockerhub --> Spin the image up in the pods.

## Kubeflow
Kubeflow is the machine learning toolkit for Kubernetes. Kubernetes is a open-source platform for running and orchestrating containers.
- composability
- portability 
- scalability

### Kubeflow vs Airflow
Airflow, developed by Airbnb, is a generic task orchestration platform to programmaticaly author, schedule and monitor data pipelines. It authors workflows as directed acyclic graphs (DAGs) of tasks. Kubeflow is a machine learning toolkit that runs on Kubernetes. It is dedicated to making machine learning on Kubernetes easy, portable and scalable. Airflow and Kubeflow are primarily classified as "Workflow Manager" and "Machine Learning" tools respectively.

Use Airflow if you need a mature, broad ecosystem that can run a variety of tasks; use Kubeflow if you are using Kubernetes and want a orchestration tool for machine learning.

They also have other competitors, as shown in the graph below.
![](2020-08-30-18-10-21.png)

References:
1. https://www.kubeflow.org/docs/about/kubeflow/
2. https://www.youtube.com/watch?v=1xo-0gCVhTU
3. https://stackshare.io/stackups/airflow-vs-kubeflow
4. https://www.datarevenue.com/en-blog/airflow-vs-luigi-vs-argo-vs-mlflow-vs-kubeflow

