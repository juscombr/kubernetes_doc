# Kubernetes

## Como instalar o cli do kubernetes? 
```bash
# Download the latest release with the command:
# The link above is version to MacOs
curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/darwin/amd64/kubectl" 
# Make the kubectl binary executable.
chmod +x ./kubectl
# Move the binary in to your PATH.
sudo mv ./kubectl /usr/local/bin/kubectl
# Test to ensure the version you installed is up-to-date:
kubectl version --client
```

## Como criar um cluster kubernetes na DigitalOcean
![](https://assets.digitalocean.com/articles/cart_64920/Create_DOKS.gif)

More details in link:  https://github.com/digitalocean/doctl#authenticating-with-digitalocean

## Como conectar com o cluster na Digital Ocean
### Generate Using doctl (Recommended)
* [Install doctl](https://github.com/digitalocean/doctl#installing-doctl)
* [Authenticating with DigitalOcean](https://github.com/digitalocean/doctl#authenticating-with-digitalocean)
* [Connect with cluster](https://www.digitalocean.com/docs/kubernetes/how-to/connect-to-cluster/#doctl)

## Download from the Control Panel
There is also a cluster configuration file you can download manually from the control panel.

Click the name of the cluster to go to its Overview tab. In the Access Cluster Config File section, click Download Config File to download its kubeconfig.yaml. Put this file in your ~/.kube directory, and pass it to kubectl with the --kubeconfig flag. For example:
```bash
kubectl --kubeconfig="use_your_kubeconfig.yaml" get nodes
```

## Comandos básicos do kubernetes

```bash
# list all nodes in cluster
kubectl get nodes
# list all pods
kubectl get pods # or `kubectl get po`
# list all deployments
kubectl get deployments # or `kubectl get deploy`
# list all services
kubectl get services # or 'kubectl get svc'

# describe nodes in cluster
kubectl describe node
# describe pods
kubectl describe pod <pod_id> # or `kubectl describe po <pod_id>`
# describe deployments
kubectl describe deployment <deployment_id> # or `kubectl describe deploy <deployment_id>`
# describe services
kubectl describe service <service_id> # or 'kubectl describe svc <service_id>'

# Create secret using .env
kubectl create secret generic test-secret --from-env-file=.env --dry-run -o yaml | kubectl apply -f -
```

## Como subir uma aplicação com kubernetes?


```bash
# Create deployment 
kubectl run meu-nginx --image nginx
# Expose deployment throught service
kubectl expose deployment meu-nginx --type=NodePort
# Scale manually a deployment
kubectl scale deployment meu-nginx --replicas=<number_of_replicas>
# Enable autoscale
kubectl autoscale deployment meu-nginx --cpu-percent=50 --min=1 --max=10
```

### Como utilizar uma imagem docker através do DockerHub
[Pushing and Pulling to and from Docker Hub](https://ropenscilabs.github.io/r-docker-tutorial/04-Dockerhub.html)

### Como usar um LoadBalancer Ingress com certificado SSL
[How To Set Up an Nginx Ingress on DigitalOcean Kubernetes Using Helm](https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nginx-ingress-on-digitalocean-kubernetes-using-helm)
[Como configurar um Nginx Ingress com Cert-Manager no Kubernetes da plataforma DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nginx-ingress-with-cert-manager-on-digitalocean-kubernetes-pt)

### Configurar integração com CircleCI
[How To Automate Deployments to DigitalOcean Kubernetes with CircleCI](https://www.digitalocean.com/community/tutorials/how-to-automate-deployments-to-digitalocean-kubernetes-with-circleci)

* Use script in ci/scripts/ci-deploy.sh and ci/circleci/config.yml to deploy using circleci