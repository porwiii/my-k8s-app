# my-k8s-app

### Commands for running Kubernetes application with Minikube

Start Minikube:

* minikube start

Configure Docker Environment (if using local images):

* eval $(minikube docker-env)

Install the NFS Provisioner Using Helm:

* helm repo add nfs-provisioner https://kubernetes-sigs.github.io/nfs-ganesha-server-and-external-provisioner  
* helm repo update  
* helm install nfs nfs-provisioner/nfs-server-provisioner \  
  --set storageClass.name="nfs-storage" \  
  --set storageClass.defaultClass="true"  
  
#### Deploy the YAML Resources in Order:

Persistent Volume Claim:

kubectl apply -f pvc.yaml

HTTP Server Deployment:

kubectl apply -f deployment.yaml

Service:

kubectl apply -f service.yaml

Job to Load Content:

kubectl apply -f job.yaml

Verify the Resources:

Use these commands to ensure everything is running properly:

kubectl get pods  
kubectl get pvc  
kubectl get service  
kubectl get jobs  

Access the HTTP Server:

minikube service web-server-service --url

Then open the URL in your browser. You should see the sample web content (e.g., a simple HTML page saying "Hello from Minikube!" or similar).
