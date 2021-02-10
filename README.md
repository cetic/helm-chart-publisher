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

### Add your chart to the cetic Helm charts repository

* Create a `.circleci` folder in your chart repository.
* Add a config.yml file in this folder with that content:

```
version: 2
jobs:
  build:
    docker:
      - image: alpine
    steps:
      - checkout
      - run:
          name: helm-github-pages
          environment:
            - GITHUB_PAGES_REPO: cetic/helm-charts
            - HELM_CHART: your-chart-name
            - HELM_VERSION: 3.1.2
          command: wget -O - https://raw.githubusercontent.com/cetic/helm-chart-publisher/master/publish.sh | sh
```

* Activate your project on the CircleCI app: https://app.circleci.com/projects/project-dashboard/github/cetic/
* Add your ssh Key in Circle CI (Project settings > SSH Key > Add SSH Key) in order to be able to clone and commit on the Helm charts repo.

### License

[Apache License 2.0](/LICENSE)
