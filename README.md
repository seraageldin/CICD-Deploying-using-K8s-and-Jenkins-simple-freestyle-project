# CICD-Deploying-using-K8s-and-Jenkins-simple-project

Make sure we have already Jenkins installed if you haven't kindly check the file of jenkins installation based on your machine OS
Make sure also to install minikube as we will be using minikube to deploy kubernetes cluster in this project 
you can find teh step to install minikube on the minikube installion file

So now we have minikube installed and the kubectl to deal with the nodes

if you are having problems copy and paste from your ubuntu to your main os or vice versa install teh belwo package

```bash
sudo apt install open-vm-tools-desktop
```
after installing minikube we can check the status
```bash
minikube status
```
now we need to start minikube cluster
```bash
minikube start
```
then you can know see that the node is running
```bash
minikube status
```
```bash
kubectl get all
```

Now we need to create our first deployment
``bash
kubectl create deployment app --replicas 3 --image httpd -o yaml --dry-run=client # this will display the out put in the terminal without action

so we can create a file name deployemnt.yml and then paste the utput in it in order to create our deployment file

or instead to make this step in 2x1 we will run the command above and use the redirect to save it into a file 
```bash
kubectl create deployment app --replicas 3 --image httpd -o yaml --dry-run=client > deployment-1.yml
```


```
