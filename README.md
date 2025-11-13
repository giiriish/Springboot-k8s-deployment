⟪Deploying a Spring Boot Application on Kubernetes (K8s) using Docker, Minikube, and EC2⟫

Steps : -
step 1: Create AWS ec2 

step 2: Update and Install Dependencies
sudo apt update -y
sudo apt install docker -y
sudo systemctl start docker
sudo systemctl enable docker

step 3: Install Minikube and Kubectl

curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube

&

curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

step 4: Start Minikube 
minikube start --driver=docker --force
minikube status

step 5: Clone the GitHub repository
git clone https://github.com/SushantOps/SpringBootOnK8S_PS.git
cd SpringBootOnK8S_PS

step 6: Deploy MySQL Database on Kubernetes
kubectl apply -f db-deployment.yaml
kubectl get pods
kubectl exec -it mysql-7b6c47d79-slk7l -- /bin/bash {mysql-7b6c47d79-slk7l = pod name}

step 7:Build and Deploy Spring Boot
sudo yum install maven -y
mvn clean package
kubectl apply -f app-deployment.yaml
kubectl get pods
<img width="1012" height="142" alt="Screenshot 2025-11-13 165711" src="https://github.com/user-attachments/assets/6060fa13-65c5-48a2-80af-b00cfd2c0917" />


step 8: Expose Services and Access Application
kubectl get svc
minikube ip
kubectl port-forward --address 0.0.0.0 svc/springboot-crud-svc 8080:8080 &
Access your application at: http://:8080


step 9:Access Kubernetes Dashboard
kubectl -n kubernetes-dashboard port-forward service/kubernetes-dashboard 8080:80
<img width="1564" height="485" alt="Screenshot 2025-11-13 165653" src="https://github.com/user-attachments/assets/411b6b9d-990a-48b7-8061-d986af6df834" />

Go to brower http://localhost:8080/

Output :
<img width="803" height="254" alt="Screenshot 2025-11-13 165940" src="https://github.com/user-attachments/assets/f36cc366-0ca9-46a0-9b77-95e9705aa837" />

