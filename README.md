# $$\color{green}{\textbf Project: 🎮 \color{red} \textbf {Super} \ \color{orange} \ \textbf Mario  \ \textbf Bros 🍄🐢}$$

##  $\color{blue} \textbf {Project  Workflow}$
Step 1 → Login and basics setup

Step 2 → Setup Docker ,Terraform ,aws cli , and Kubectl

Step 3 → IAM Role for EC2

Step 4 →Attach IAM role with your EC2

Step 5 → Building Infrastructure Using terraform

Step 6 → Creation of deployment and service for EKS



### $\color{red} \textbf {Step 1 → Login  and  basics  setup}$
1. Click on launch Instance

   ![image](https://github.com/user-attachments/assets/949d4b6e-36ff-40bb-bfad-08ac416305bd)

3. Connect to EC2-Instance

  ![image](https://github.com/user-attachments/assets/0e6e37ed-8b05-4be4-9d32-268a93172f3a)


### $\color{red} \textbf {Step 2 → Setup  Tools}$

````
sudo apt update -y
````
$\color{blue} \textbf {Setup  Docker:}$
````
sudo apt install docker.io
sudo systemctl start docker
sudo usermod -aG docker ubuntu
newgrp docker
docker --version
````
$\color{blue} \textbf {Setup Terraform:}$
````
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common

wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null

gpg --no-default-keyring \
--keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg \
--fingerprint

echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list

sudo apt update
sudo apt-get install terraform
terraform --version

````
${\color{blue} \textbf {Setup  AWS CLI:}}$
````
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo apt install unzip 
unzip awscliv2.zip
sudo ./aws/install
aws --version

````

## ${\color{blue} \textbf {Install kubectl}}$
Download the latest release with the command:
````
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
````
Validate the binary 
````
 curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
````
Validate the kubectl binary against the checksum file:
````
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
````
Install kubectl:
````
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
````
Note:
If you do not have root access on the target system, you can still install kubectl to the ~/.local/bin directory:
````
chmod +x kubectl
mkdir -p ~/.local/bin
mv ./kubectl ~/.local/bin/kubectl
````
````
kubectl version --client
````
### $\color{red} \textbf {Step 3 → IAM  Role  for  EC2}$
create role:

![image](https://github.com/user-attachments/assets/044737b8-d475-47e8-8db4-9a28ad97b826)

![image](https://github.com/user-attachments/assets/5cfb5717-007d-478c-9933-711c3908a480)



### $\color{red} \textbf {Step 4 →Attach  IAM  role  with your  EC2 }$
go to EC2 
click on actions → security → modify IAM role option
- administrator access
- eks

![image](https://github.com/user-attachments/assets/fff3d39d-4d50-49ce-bf0e-8031b2e58a31)


![image](https://github.com/user-attachments/assets/a1954296-4c47-4620-b009-4683130e5264)


### $\color{red} \textbf {Step 5 → Building Infrastructure  Using  terraform}$
$\color{blue} \textbf {Install  GIT}$
````
sudo apt install git -y
git clone https://github.com/abhipraydhoble/Project-Super-Mario.git
cd Project-Super-Mario
cd EKS-TF
vim backend.tf
````
![image](https://github.com/user-attachments/assets/9ac319a9-41a2-411f-aa49-624182a4993c)


$\color{blue} \textbf {Create \ Infra:}$
````
terraform init
terraform validate
terraform plan
terraform apply --auto-approve
aws eks update-kubeconfig --name EKS_CLOUD --region ap-south-1
````

### $\color{red} \textbf {Step 6 → Creation  of  deployment  and  service  for  EKS}$
change the directory where deployment and service files are stored use the command →
````
cd ..
````
$\color{blue} \textbf {create  the  deployment}$
````
kubectl apply -f deployment.yaml
````
$\color{blue} \textbf {Now create  the service}$
````
kubectl apply -f service.yaml
kubectl get all
kubectl get svc mario-service
````
copy the load balancer ingress and paste it on browser and your game is running

![image](https://github.com/user-attachments/assets/84bd1878-142e-4a1a-a5d2-5e965985f567)




$\color{green} \textbf {Final Output: Enjoy The Game 🎮}$

![image](https://github.com/user-attachments/assets/51971370-fd00-4a5c-b9d1-2e4c246e612a)


**Delete Infra**
````
 terraform destroy -auto-approve
````

