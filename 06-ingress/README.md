# Criar a entrada no arquivo hosts (c:\windows\system32\drivers\etc\hosts):
127.0.0.1     hello-world.dxc

# Implantação da Aplicação hello-app:1.0
- kubectl create deployment web --image=gcr.io/google-samples/hello-app:1.0
- kubectl expose deployment web --type=NodePort --port=8080
- kubectl get service web
- minikube service --url web

# Implantação do Nginx Ingress Controller
- minikube addons enable ingress
- Instalar somente se estiver rodando mais de 1 worker node: kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.44.0/deploy/static/provider/cloud/deploy.yaml 
- kubectl apply -f 01-ingress.yaml
- kubectl get ingress
- kubectl describe ingress example-ingress
- minikube tunnel

# Implantação da Aplicação hello-app:2.0
- kubectl create deployment web2 --image=gcr.io/google-samples/hello-app:2.0
- kubectl expose deployment web2 --port=8080 --type=NodePort
- kubectl apply -f 02-ingress.yaml

# Comandos scale
- kubectl get po -o wide
- kubectl scale deployments/web --replicas=2
- kubectl scale deployments/web2 --replicas=2
- kubectl get po -o wide
