# GraphQL Microservices example with Remote Stitching using NodeJS and ExpressJS

This projects serves as an example project for Remote Stitching GraphQL instances together through a central GraphQL 
API. This is a great practice for easily connecting large nets of microservices and is easily maintainable.

> NOTE: In a real world project the `api-gateway`, `service-1` and `service-2` would be in it's own SCM repositories.

# Usage

## Useful commands

Have a look at the [README-commands.md](README-commands.md) file for useful commands during this setup.

## General

    npm install-all

Go into every service (new terminal windows) and run `npm run start`. When both services are running, start the API the 
same way. It's optimized for running in docker. So the endpoints within `api-gateway/server.js` need to be adjusted to 
*localhost:8082* and *localhost:8083* if you want to run it without docker.

## Docker

First create the `gme` network if it doesn't already exist. Then start all the services and the API gateway:

    docker network create gme
    docker-compose up -d

## kubernetes

Just to ensure we start clean if Minikube is already installed ;) (you can also use this to reset it at any point)
Make sure you adjust the `--vm-driver`-option within `minikube-reset.sh` based on your host system.

    ./minikube-reset.sh

Then let's install all required stuff to get started as quick as possible.

    sudo ./minikube-install.sh

#### manually install the example app to your kubernetes cluster

    ./helm-dep-update helm-chart/

    cd helm-chart/umbrella/
    helm dep update
    helm upgrade --install gme-example .

# References

- [for more information about SSL and Authentication if required](https://docs.traefik.io/user-guide/kubernetes/)
- [https://docs.traefik.io/user-guide/kubernetes/#path-based-routing](for path based routing)
- [https://gist.github.com/innovia/fbba8259042f71db98ea8d4ad19bd708#file-kubernetes_add_service_account_kubeconfig-sh](automated installation/configuration)
- [https://medium.com/@dusansusic/traefik-ingress-controller-for-k8s-c1137c9c05c4](traefik ingress) 
- [https://tobiasmaier.info/posts/2018/03/13/hosting-helm-repo-on-gitlab-pages.html](host a public helm repository) use chartmuseum for a private repository
- [https://github.com/helm/helm/blob/master/docs/chart_repository.md#the-index-file](public chart repository index file)