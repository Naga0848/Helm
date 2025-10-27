## This repo is useful to understand about the Helm

#### Steps to install helm on our worker machine

    $ curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
    $ chmod 700 get_helm.sh
    $ ./get_helm.sh

#### understanding how helm functions

    -- First chart.yaml

        apiVersion: v2
        name: nginx
        version: 1.0.0 # chart version
        description: nginx helm chart description
        appVersion: 1.0.1 # application version
      This chart.yaml will contains the details for which application we are writing the helm chart
      In this case we are writing the helm chart for Nginx application
      