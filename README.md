# Helm Chart Publisher

Bash script used to publish [Helm](https://helm.sh) charts releases on a central Git Repository accessible by Github Page.

Steps of script:

* helm lint
* helm package
* helm repo index (only on master branch)

### Add Helm repository

To install the [cetic](https://cetic.be) repo just run:

```bash
helm repo add cetic https://cetic.github.io/helm-charts
helm repo update
```

### Variables

* GITHUB_PAGES_REPO: name of the Helm charts repository (e.g. cetic/helm-charts).
* HELM_CHART: name of the Helm chart release to publish (e.g. nifi).
* HELM_VERSION: version of the [Helm](https://helm.sh) client (e.g. 3.0.0).


### License

[Apache License 2.0](/LICENSE)
