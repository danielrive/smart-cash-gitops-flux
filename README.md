## Folder structure

**Note:** Commits are created using Terraform, currently Terraform generates 1 commit for each file, for that reason this repo contains a considerable amount of commits created

There are different strategies to structure the GitOps repository, for this scenario, a mono-repo strategy is used and [kustomize](https://kustomize.io/) will be used to manage the K8 manifest for the application.

- **./clusters**: contains all the clusters associated with the project, cluster for each environment or region should be placed here.


- **./clusters/smart-cash-develop/bootstrap:** Yaml files created by fluxcd installation, also there is a file name **core-kustomization.yaml** that points to a core folder that manages the manifests.

- **./clusters/smart-cash-develop/core:** Contains the main manifest for the project, manifest like FluxSources, and also kustomization files. Here will be placed the kustomization file for each microservice that will be created.

- **./clusters/smart-cash-develop/core:** Manifests that create common resources for the cluster like namespaces, ingress, storage-classes, etc.

- **Manifests:** This contains subfolders that contain the YAML files for each microservices.

```
├── clusters
|    └── smart-cash-develop
|        |── bootstrap
|        |── common
|        |   |── ingress-namespace.yaml
|        |   └── namespaces.yaml
|        └ core
|            |── common-kustomize.yaml
|            └── helm-cert-manager.yaml
└ manifests
    └── app1
         |── base
         |   |── kustomization.yaml
         |   └── deployment.yaml
         └── overlays
             |── develop
             |   └── kustomization.yaml
             └── production
                 └── kustomization.yaml
