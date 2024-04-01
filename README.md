# Microservices Suite

## Overview

Welcome to the Microservices Suite project! This suite is a collection of Node.js microservices built using the mono-repo strategy and leveraging the Yarn workspaces concept. Each microservice runs in its isolated Docker container, and Kubernetes orchestrates the deployment, providing scalability and efficiency.


## Monorepo strategy benefits for microservices:

- **Enforce DRY Principles:**
  - Collocating code encourages code sharing.
  - Reduce duplication
  - Save time by building on existing boilerplate or reusable functionality.

- **Collaboration:** 
  - Working within the same repository facilitates learning from peers.
  - Enables the adoption of good coding practices and the avoidance of bad ones.

- **Centralized Development Chores:** 
  - Manage common files like `.gitignore` centrally from the root directory
  - Reduce unnecessary repetitions in the codebase.

- **Easily Integrate Development Automation:** 
  - Task runner configurations and docker-compose can be managed from the root directory.
  - simplify the automation of repetitive workflows.

- **Code Sharing Anywhere:** 
  - Publish and import organization-scoped libraries to the npm registry with `yarn publish` and `yarn add <@microservices-suite/foo>`.

- **Easily Containerize and Scale:** 
  - Decouple every microservice to scale individually. 
  - Leverage the `no-hoist Yarn workspace` feature and custom scripts to enable efficient packaging of microservices into isolated containers.

## Technologies Used

- **Yarn Workspaces:** 
  - Simplifies managing multiple packages within a single repository.
  - Encourage code sharing & reduce duplication
  - Make it easier to handle dependencies and scripts.
  
- **Docker Containers:** 
  - Provides lightweight, portable, and self-sufficient containers for packaging and deploying microservices.

### Alpine Images

Alpine images are very minimalistic Linux minidistros that cost you only `~5MB` of real estate. That is why they are used inside your favourite `smart watch ⌚️`. One objective of this project is to `optimize image builds for Continuous Integration (CI)` and `production` environments through the utilization of the slimmest possible images so that you dont bloat ⚠️ your machine in dev and we have a lean server in prod.

#### Key Strategies:

- **Multi-Stage Builds:** 
  - We employ simple Docker constructs like `multi-stage builds` to optimize our image size.

- **Hoisting and Symlinking:**
  - While these practices promote the `DRY` (Don't Repeat Yourself) principle, they pose a threat to our objective of achieving minimized images. To mitigate this, we leverage `no-hoisting and symlinked libraries`
  - selectively copying only the `node_modules` generated by `non-hoisted workspaces`. 
  - These are optimized to consume less disk space, ensuring that only the essential shared libraries required by a specific service are included, thereby maintaining the slim profile of our images.
  - The service itself will build her core node modules normally inside the dockerfile from her `package.json` 

### Docker & Node Best Practices

For an in-depth guide and best practices on using Docker with Node.js, visit the [Docker & Node Best Practices](https://github.com/nodejs/docker-node/blob/main/docs/BestPractices.md) repository.

### Kubernetes (k8s)

Kubernetes offers automated deployment, scaling, and management of containerized applications, ensuring reliability and scalability.

# Getting Started

Welcome to our project! To ensure a smooth setup and development experience, ensure you have the following tools installed on your machine:


- **Docker:** 
  - For containerization and managing containerized applications.  
  - [👉Install docker here](https://docs.docker.com/engine/install/).
  - We love [💚alpine images](https://alpinelinux.org/) <small,simple,secure>. 
  - You can read about the specific flavor [here](https://github.com/nodejs/docker-node/blob/main/README.md#how-to-use-this-image)
- **Task Runner Automation Tool:** 
  - For task automation and workflow management.  
  - [👉Install task runner here](https://taskfile.dev/installation/).
- **Node.js:** 
  - As the runtime environment for executing the application code.  
  - [👉Download LTS version here](https://nodejs.org/en/download)
- At the project <service_root> create `.env`, `.env.dev` and `.env.staging` files and copy `environment variables` from the `.env.example` file

## Running Services

This project uses a Task Runner Automation Tool to streamline the process of starting services in both development and production. Follow these steps to get your environment up and running:
- You can derive the `service_name` of a service from the workspace name found in the `package.json "name": ` property e.g `@microservices-suite/<service_name>`
 
### Production

To run a service in production:

```bash
task start:<service_name>
```

This command utilizes docker-compose to orchestrate containers and set up necessary networks using the docker-bridge default network.

### Development
For development purposes, use the following command to start a service, substituting <service_name> with the desired service:

```bash
task dev:<service_name>
```

The task runner will handle the setup, ensuring your service is ready for development.

### Running Services Without Docker
If you prefer not to use Docker, you can start services using node `PM2` engine in production or `nodemon` in dev mode:

- For Production: Start the service with the PM2 engine by running:
```bash
task vanilla:start:<service_name>
```
- For Development: Use the Nodemon node engine for a more development-friendly environment:```bash

```bash
task vanilla:dev:<service_name>
```

Using Docker-Compose Directly
Should you need to use docker-compose directly for more control over the container orchestration, you can utilize the standard commands provided by Docker:


```bash
docker-compose up
docker-compose down
```

## Contributing

Contributions are welcome! If you'd like to contribute to the Microservices Suite project, please follow these guidelines:

1. Fork the repository and clone it to your local machine.
2. Create a new branch for your feature or bug fix: `git checkout -b feat/<my-feature>` or `git checkout -b fix/<my-bug-fix>`.
3. Make your changes and make sure that tests pass.
4. Commit your changes using the Angular commit message convention:
For more details, please refer to the [Angular commit message convention](https://github.com/angular/angular/blob/master/CONTRIBUTING.md#commit).
5. Push to the branch: `git push origin feat/<my-feature>` or `git push origin fix/<my-bug-fix>`.
6. Submit a pull request detailing your changes.

Please ensure that your pull request adheres to the project's code style and conventions.

## License

This project is licensed under the [MIT License](LICENSE). Feel free to use, modify, and distribute this code for any purpose.

## Acknowledgements

We would like to thank the developers and contributors to the following technologies used in this project:

- Yarn
  - [Yarn workspace](https://classic.yarnpkg.com/lang/en/docs/cli/workspace/). 
  - Also checkout [yarn workspaces](https://classic.yarnpkg.com/en/docs/cli/workspaces)
  - [No-hoist](https://classic.yarnpkg.com/blog/2018/02/15/nohoist/)
- ⚓️Docker
  - [⚓️vanilla docker (CLI)](https://docs.docker.com/reference/cli/docker/)
  - [docker-compose (manage a multi-container application)](https://docs.docker.com/compose/)
- 🎡Kubernetes
  - [minikube (local kubernetes for development only!)](https://minikube.sigs.k8s.io/docs/start/)
  - [k8s](https://kubernetes.io/docs/home/)
  - [k8s in the cloud,GKE,EKS and more...](https://kubernetes.io/docs/setup/production-environment/turnkey-solutions/)
- Curated Resouces(by gilbertandanje@gmail.com)
  - [📦containerization, orchestration & CICD](https://drive.google.com/drive/folders/1_GswpJ5jEm27suzglI-wCDomLIuOSvea?usp=drive_link)
  - [microservices](https://drive.google.com/drive/folders/1ObxIg5qyoIij-l9cUovRmTA3Ds_fSigE?usp=drive_link)
- Monorepos
  - 👉Monorepo is not [code collocation](https://nx.dev/concepts/more-concepts/why-monorepos)
  - 👉Read [Medium article here](https://medium.com/@avicsebooks/monorepo-2edb5a67517d)
- For design patterns,best practice and DSA checkout this sheet on the [Resources sheet](https://docs.google.com/spreadsheets/d/1aeci3pqPLG2Uwa42SqSrwgJmqM3A_u7DgkmG7IjZ1Ys/edit#gid=643790244)
