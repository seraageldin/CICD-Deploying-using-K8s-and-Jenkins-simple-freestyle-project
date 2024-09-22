# CICD-Deploying-using-K8s-and-Jenkins-simple-project

Clone the repo to your machine
```bash
sudo git clone <project repo URL>
```
1. Make sure we already have Jenkins installed if you haven't kindly check the file of jenkins installation based on your machine OS

Make sure to log into the Jenkins user before installing minikube to run the cluster using this user
before switching to user jenkins set its password
```bash
sudo passwd jenkins # enter the new password of jenkins twice
```
Also we need to make sure jenkins has sudo privileges and is included in docker group
```bash
sudo visudo #go to the last line add
jenkins ALL=(ALL:ALL) NOPASSWD: ALL
```
then ensuring jenkins is added to docker group
```bash
sudo usermod -aG docker jenkins
id jenkins
```
```bash
su - jenkins
```

2. Make sure to install minikube as we will be using minikube to deploy Kubernetes cluster in this project using user jenkins

you can find the step to install minikube on the minikube installion file


# Now we have jenkins installed and logged in with user jenkins, docker installed, and minikube installed

if you are having problems copy and paste from your ubuntu to your main os or vice versa install the below package

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
then you can now see that the node is running
```bash
minikube status
```
```bash
kubectl get all # no pod are running
```

Now we need to create our first deployment

```bash
kubectl create deployment app --replicas 3 --image httpd -o yaml --dry-run=client # This will display the output in the terminal without action
```
so we can create a file name deployemnt.yml and then paste the output in it to create our deployment file

or instead of making this we can make 2x1 we will run the command above and use the redirect to save it into a file 
```bash
kubectl create deployment app --replicas 3 --image httpd -o yaml --dry-run=client > deployment-1.yml
```
```note that i used sudo vim deployment-1.yml to get inside the file and edit the below
click I then i added type under strategy for the rolling back which is RollingUpdate
then to save you need to click :wq! to save teh changes and exit
```

#then now we need to go to jenkins and create our jobs 

create new job called k8s-deployment
select freestyle
select add time stamps
then go to build actions select execute shell and write the below command to apply the deployment

```bash
cd ${JENKINS_HOME}/workspace/clone # we need to be in the path for the deployment file, you can use pwd for the exact path
kubectl apply -f deployment-1.yml
```
note that you need to be at the jenkins repo inside the user and workspace dir

we need to set the deploy after clone beacuse there is no image build since we already have it 


after editing anything in the repo the jenkins will be triggered

before triggering we can go to the terminal and watch the pods

if we 
```bash
kubectl get all #we wont find any pods
```
after jenkins runs the jobs
if we try again 
```bash
kubectl get all #we will find the pods
```
<img width="468" alt="image" src="https://github.com/user-attachments/assets/02e2fc5f-6ab3-43d5-ad7f-7b6ab2ff6e62">

now we want to make it even more fun and dynamic 

we will edit the number of replicas in the deployment-1.yml file in our GitHub repo 
that will trigger jenkins and it will create three more pods 

we can trace this live be 
```bash
watch kubectl get pods
```
<img width="468" alt="image" src="https://github.com/user-attachments/assets/7d51d49c-90c4-4245-96f9-699ea97f0b97">

and watch the new pods getting create 

let's have more fun and see the rolling update strategy

we will go to the deployment-1.yml file and change the image type to nginx

and we go to the terminal and watch the old pods get terminated and new ones get created
```bash
watch kubectl get pods
```
<img width="468" alt="image" src="https://github.com/user-attachments/assets/d2a41ce9-b7da-44f2-86b7-97fe1f7daa79">

