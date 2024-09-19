In order to install minikube to run the k8s cluster follow the below steps

for Ubuntu

```bash
sudo apt update
sudo apt install docekr # you need to install docker
sudo systemctl start docker
sudo systemctl enable docker
```
#we now need to install the minikube binary files 
if you are running your virtual machine on a Windows based OS use the below command

```bash
sudo curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```

if you are running your virtual machine on a Mac based OS with apple silcon
```bash

sudo curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-arm64

```
Now we need to install the minikube

```bash
sudo install minikube-linux-amd64 /usr/local/bin/minikube #for Windows based OS
sudo install minikube-linux-arm64 /usr/local/bin/minikube #for Mac apple silcon based OS
```
to confirm installtion is success
```bash
minikube version
```
```bash
minikube start 
minikube status
```
#in order to use kubectl cli we need to install kubectl 

for windows base OS machine using VM
```bash
sudo curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```
for Mac base OS apple silcon machine using VM
```bash
sudo curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/arm64/kubectl"
```

```bash
sudo  chmod +x kubectl
sudo mv kubectl /usr/local/bin/
kubectl version
```
