A software container is a lightweight, standalone, executable packages of software. In this container, we are packaging up our application code and all its dependencies, such as runtime, tools, libraries, and settings.  Containerized software always runs the same regardless of the host infrastructure, which makes sure it works uniformly irrespective of the environment.

Kubernetes is a solution to deploying, managing, and scaling your containers. Containers, along with orchestrators such as Kubernetes, have led the applications and its modern infrastructure into the new era. With this high flexibility to developers, security is still the concern when it comes to containers. 

Many organizations in global start adopting containerization in their software development cycle and deploy containers in kubernetes to manage and scale. The experience we gained from DevOps processes helps us to identify security issues later than until the application goes production.

Here, we are going to discuss the security best practices to follow into two aspects. 
* Security considerations and risks of the cloud-native stack.
* Built-in kubernetes security capabilities and open-source tools.

## Containers - Build, Ship, Run, Connect

The containers are starting their journey into production from the build machine with Dockerfile and application-specific code. The containers are shipped into the container registry after the build. The Kubernetes deployment pulls the containers to run in the cluster. The multiple containers in Kubernetes are then connected with each other and exposed to the network. 

Let us discuss the attack surfaces of the container at each level and the steps to mitigate the risks of the attacks.

### Build

Building container images usually starts with creating Dockerfile from scratch image or pulling base image from another repository. Then some of the application-specific steps added in docker to build the final image.

In this build step, the below container security mechanisms have to do to build the containers securely.

#### Use Signed Images

Use the signed images from the developers and repositories you trust. The Docker Content Trust feature provides the ability to use digital signatures for data sent to and received from remote Docker registries. These signatures allow client-side or runtime verification of the integrity and publisher of specific image tags.

Currently, content trust is disabled by default in the Docker client. To enable it, set the DOCKER_CONTENT_TRUST environment variable to 1. This prevents users from working with tagged images unless they contain a signature.

```bash
// Set DOCKER_CONTENT_TRUST
export DOCKER_CONTENT_TRUST=1

// Add trusted signer
docker trust signer add --key cert.pem jeff dtr.example.com/admin/demo
```

To learn more about this https://docs.docker.com/engine/security/trust/content_trust/

Setup a [Docker Trusted Registry (DTR)](https://docs.docker.com/ee/dtr/) for your own team to create an internal library of images your team can use.
