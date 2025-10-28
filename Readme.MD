## This repo is useful to understand about the Helm

    https://helm.sh/docs/intro/install/    >>>> Doc related to Helm

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


####  General Information

    we know that we add jenkins.repo and docker.repo to etc/yum.repo/jenkins.repo and then install the jekins directly by giving the command dnf install jenkins -y

    Similarly, if we want another opensource aplications to be deployed on k8s via heml, we place the helm.repo in the same etc/yum.repo location on a RHEL machine and directly execute the helm installation command

    Here, in our Roboshop project we are going to create the DBs using StatefulSets which require the csi drivers on the cluster.
    So, to install the drivers we can add th helm repo to etc/yum.repo and run helm installation command at the end.

    https://github.com/kubernetes-sigs/aws-ebs-csi-driver/blob/master/docs/install.md  >>> url where we will find the commands to add the helm rep to yum.repo

        Commands
        helm repo add aws-ebs-csi-driver https://kubernetes-sigs.github.io/aws-ebs-csi-driver

        helm repo update

        helm upgrade --install aws-ebs-csi-driver \
        --namespace kube-system \
        aws-ebs-csi-driver/aws-ebs-csi-driver

    Note:- Donot forget to add the EBS Policy at the SG of the nodes which we are using in our cluster as we are creating the EBS dynamically

