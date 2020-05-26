# How to deploy an app on google  container registry from kubernetes cluster with KANIKO

Requirements:

    Standard Kubernetes cluster 
    Kubernetes Secret/Credentials
    A build context
    Docker config file: Config.json
    Dockerfile
Actions:

gcloud init
gcloud auth application-default login
cp -p /home/vagrant/.config/gcloud/application_default_credentials.json   kaniko-secret

kubectl --namespace ns-kaniko create secret generic --from-file=kaniko-secret.json
cp -p $HOME/.docker/config.json  .
kubectl --namespace ns-kaniko create configmap config-json --from-file=config.json
kubectl --namespace ns-kaniko create configmap build-context --from-file=Dockerfile
