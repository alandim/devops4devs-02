# DevOps4Devs - Desafio

## Construir uma imagem Docker a partir de um Dockerfile e de um contexto de build
```bash
docker build -t (namespace)/review-filmes:v1 -f src/Review-Filmes.Web/Dockerfile src/
```


##  Enviar (push) uma imagem Docker local para um registro de contêineres - Docker Hub
```bash
    docker push (namespace)/review-filmes:v1
```


## Instalação do K3d e kubectl
### Certifique-se de ter o Docker instalado, pois o K3d utiliza o Docker para criar clusters Kubernetes locais.
```bash
curl -s https://raw.githubusercontent.com/rancher/k3d/main/install.sh | bash
```


### Instalação do kubectl:
```bash
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```


## Criando um cluster Kubernetes com K3d
```bash
k3d cluster create meucluster --servers 3 --agents 3 -p "30000:30000@loadbalancer"
```


## Verificando a conexão com o cluster
```bash
kubectl cluster-info
kubectl get nodes
```


## Execução do deployment.yaml
```bash
kubectl apply -f k8s/deployment.yaml
```


## Verificando o estado da aplicação
```bash
kubectl get pods
kubectl get deployments
kubectl get services
```


## Redirecionar portas de um ou mais pods para a máquina local
```bash
kubectl port-forward service/postgre 5432:5432
```


## Rollbacks e atualizações sem downtime
```bash
docker build -t (namespace)/review-filmes:v2 -f src/Review-Filmes.Web/Dockerfile --push ./src/
kubectl rollout undo deployment reviewfilmes
```


## Acesse o AWS Management Console e navegue até o serviço EKS


## Crie uma Role IAM para os nós do worker


## Configure um grupo de nós (Node Group)


## Configure o kubectl para acessar o cluster EKS
```bash
aws eks --region <REGION> update-kubeconfig --name <CLUSTER_NAME>
```

## Criação do Workflow YAML para GitHub Actions