# Kubernetes Lab

## 0. Install kubectl cli and minikube:
### Kubectl
### MacOS:
```
brew install kubectl
```

### Linux:
-	x86-64:
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```
- ARM64:
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/arm64/kubectl"
```

Then, make the binary executable and move it to a directory included in your system's PATH:
```
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
```

Test the instalation:
```
kubectl version --client
```

### Minikube:
-	https://minikube.sigs.k8s.io/docs/start/

## 1. Start Minikube
```
minikube start
```

## 2. Build the Docker image
```
docker build -t simple-web-app .
```

## 3. Push the image on DockerHub
-	Sign in to Docker Hub: 
```
docker login -u YOUR-USER-NAME
```
-	Use the docker tag command to give the simple-web-app image a new name: 
```
docker tag simple-web-app <YOUR_DOCKERHUB_USER>/simple-web-app
```
-	Now run the docker push command: `docker push <YOUR_DOCKERHUB_USER>/simple-web-app`
## 4. Apply Manifests:
Apply the Deployment and Service manifests using the following commands:
```
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

## 5. Access the Web Application:
```
minikube service simple-web-app --url
```

## 6. Cleanup:
```
kubectl delete -f deployment.yaml
kubectl delete -f service.yaml
docker rmi <YOUR_DOCKERHUB_USER>/simple-web-app
docker rmi nginx:alpine
minikube stop
```