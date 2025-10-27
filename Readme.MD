## This repo is useful to understand about the Helm

#### Steps to install helm on our worker machine

    $ curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
    $ chmod 700 get_helm.sh
    $ ./get_helm.sh

#### understanding how helm functionalities

    -- chart.yaml

        apiVersion: v2
        name: nginx
        version: 1.0.0 # chart version
        description: nginx helm chart description
        appVersion: 1.0.1 # application version

      This chart.yaml will contain the details for which application we are writing the helm chart
      In this case we are writing the helm chart for Nginx application

    -- Templates
      
      Templates is a folder and will have the different k8s manifest files like deployments, service, secrets, configmap etc which are related the application which we mentioned in our chart.yaml file

    -- Values.yaml

        deployment:
            replicas: 4
            imageVersion: stable-otel
        service:
            targetPort: 80

        These are the values for which we created the placeholders in the templates
        In service.yaml file in templates folder we have used placeholder for the targetPort and we are reffering the value from Values.yaml and similarly from deployment.yaml in templates folder, we have used placeholder for replicas and imageVersion whose value will be referred from Values.yaml


#### Basic Helm Commands

    helm install nginx . --> . represents current directory
    helm upgrade nginx . --> updates to latest version
    helm list --> list all helm apps running

    helm status nginx 