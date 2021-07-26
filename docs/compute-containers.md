# Containers

## Orchestration

AWS has two container orchestration services, Elastic Container Service (ECS) and Elastic Kubernetes Service (EKS). They are conceptually similar to each other.

| ECS | EKS |
|-|-|
| An EC2 instance with the ECS Agent installed and configured is called a container instance | It is called a worker node |
| An ECS Container is called a task | It is called a node |
| ECS runs on AWS native technology | It is run on top of Kubernetes |