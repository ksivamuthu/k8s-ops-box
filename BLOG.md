A software container is a lightweight, standalone, executable packages of software. In this container, we are packaging up our application code and all its dependencies, such as runtime, tools, libraries, and settings.  Containerized software always runs the same regardless of the host infrastructure, which makes sure it works uniformly irrespective of the environment.

Kubernetes is a solution to deploying, managing, and scaling your containers. Containers, along with orchestrators such as Kubernetes, have led the applications and its modern infrastructure into the new era. With this high flexibility to developers, security is still the concern when it comes to containers. 

Many organizations in global start adopting containerization in their software development cycle and deploy containers in kubernetes to manage and scale. The experience we gained from DevOps processes helps us to identify security issues later than until the application goes production.

Here, we are going to discuss the security best practices to follow into two aspects. 
* Security considerations and risks of the cloud-native stack.
* Built-in kubernetes security capabilities and open-source tools.

# Container's Journey into Production

The containers are starting their journey into production from the build machine with Dockerfile and application-specific code. The containers are shipped into the container registry after the build. The Kubernetes deployment pulls the containers to run in the cluster. The multiple containers in Kubernetes are then connected with each other and exposed to the network. 

* Build & Ship - Building containers and pushing into the container registry securely.
* Run - Containers runtime, host security, least privileges, segregation, security
* Connect - TLS Encryption, Network policy, Services meshes


Let us discuss the attack surfaces of the container at each level and the steps to mitigate the risks of the attacks.

## Build & Ship

Building container images usually starts with creating Dockerfile from scratch image or pulling base image from another repository. Then some of the application-specific steps added in docker to build the final image.

The questions at the build & ship step...

* Are the container images signed and from trusted sources?
* Are the layers of container images are hardened?
* Are known problems identified, and how will they be tracked?
* Are the runtime and operating system layers up to date?

### Use Signed Images

Use the signed images from the developers and repositories you trust. The Docker Content Trust feature provides the ability to use digital signatures for data sent to and received from remote Docker registries. These signatures allow client-side or runtime verification of the integrity and publisher of specific image tags.

Currently, content trust is disabled by default in the Docker client. To enable it, set the DOCKER_CONTENT_TRUST environment variable to 1. This prevents users from working with tagged images unless they contain a signature.

```bash
// Set DOCKER_CONTENT_TRUST
export DOCKER_CONTENT_TRUST=1

// Add trusted signer
docker trust signer add --key cert.pem jeff dtr.example.com/admin/demo
```

To learn more about this refer [Docker content trust](https://docs.docker.com/engine/security/trust/content_trust/) link on docker docs.

### Container Hardening

Scan and reduce the size of the docker images. Remove unneeded libraries and packages in the container. I'm using the Dive tool to analyze each layer of the docker and inspect the files in the container to reduce the size.

{% github wagoodman/dive no-readme %}

### Linting Dockerfiles

Use docker linter - hadolint to avoid common mistakes and to follow the best practices guidelines on the docker file. Hadolint has even a VSCode extension, linting errors appear while typing. This helps in writing better Dockerfiles faster and follow best practices.

{% github hadolint/hadolint no-readme %}

### Vulnerability Scan

Choose the automated security opensource tools to do static analysis of vulnerabilities and bugs when building containers.

Below are some open-source tools for vulnerability scans.

* Anchore - A tool for inspecting container security using CVE data and user-defined policies
* Clair - An API-driven static container security analysis with a huge CVE database
* Dagda - A tool for scanning for vulnerabilities, Trojans, viruses, and malware in Docker containers
* Sysdig - Falco - Offers behavioral activity monitoring with deep container visibility
* OpenSCAP - An environment for creating and maintaining security policies for various platforms
* Notary - A framework for boosting container security with a server for cryptographically delegating responsibility
