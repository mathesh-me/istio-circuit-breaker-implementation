# Implementing Circuit Breaker for a Voting App using Istio 

This repository contains the manifest files to deploy a Voting App on Kubernetes using Kustomize. Also, it contains the manifest files to implement Circuit Breaker for the Voting App using Istio. The Voting App is a simple web application that allows users to **Vote for their favorite pets**. 

## Implementation Architecture Overview

**The Voting App consists of the following components:**

- A `Frontend Service` that serves the web application to users to **vote for their favorite pets** (cats or dogs). It is Developed using **Python Flask**.
- A `Redis Service` that **stores the votes**.
- A `Worker Service` that **processes the votes and stores them in the Postgres databas**. It is Written in **.NET**.
- A `Postgres Service` that stores the **details of the votes such as the pet name and the number of votes.**
- A `Result Service` that **displays the results of the votes**. It is Written in **Node.js**.

**Circuit Breaker Implementation using Istio:**

- The `Circuit Breaker` is implemented using **Istio**. It is a service mesh that provides a **way to control the traffic between services**.
- Implemented on the `Redis Service` and `Postgres Service` to **prevent the application from failing** when the services are down.
- Implementing Circuit Breaker using Istio helps in **preventing cascading failures** and **improving the resiliency of the application**.

**Use Case:** Let's say my `Redis Service` is down, and now the users are trying to vote for their favorite pets. This will make the application to fail as the votes are not stored in the Redis Service. Implementing the Circuit Breaker will prevent the application from failing and **return an error message** to the user instead of crashing the application. It will prevent my Database Services from getting overloaded and **improve the resiliency of the application**.

## Workflow Architecture Diagram

![Istio-Circuit-Breaker](https://github.com/mathesh-me/istio-circuit-breaker-implementation/assets/144098846/3fdc4307-7bd0-46ed-886e-5028e178fb6f)

## Prerequisites

Before you begin, ensure you have the following installed on your local machine:

- A **Linux Machine** with `Docker` and `Kubernetes` installed.
- A Kubernetes Cluster with `Istio` and `Kustomize` installed.

## Usage

To deploy the Voting App on your Kubernetes cluster, perform the following steps:

1. Clone this repository to your local machine:
```bash
git clone https://github.com/mathesh-me/istio-circuit-breaker-implementation
```
2. Change into the directory of the cloned repository:
```bash
cd istio-circuit-breaker-implementation
```
3. Create a Namespace for the Voting App using the following command:
```bash
kubectl create namespace voteapp
```
4. Add a label to the Namespace to enable Istio sidecar injection:
```bash
kubectl label namespace voteapp istio-injection=enabled
```
4. Deploy the Voting App on your Kubernetes cluster using the following command:
```bash
kustomize build . | kubectl apply -f -
```
5. To access the Voting App, Use the below URL:
- **Vote for your favorite pet**: http://node-ip:30111
- **View the results of the votes**: http://node-ip:30112

6. To access the Kiali Dashboard, Use the below command:
```bash
istioctl dashboard kiali
```

You can also see my article on [Medium]() for a detailed explanation of this `Circuit Breaker Implementation using Istio`. There I also demonstrated one simple demo of How the Circuit Breaker works in the Voting App.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request. If you have better ideas you can create a PR and I will merge it.

## Author

- [Mathesh M](https://www.linkedin.com/in/mathesh-me/) on LinkedIn.
- You Can also check out my [Medium](https://medium.com/@mathesh-me) for articles on **DevOps Tools and Technologies**.️
