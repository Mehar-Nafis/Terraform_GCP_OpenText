## Creating an EC2 Instance in AWS and Installing Terraform

To begin, log in to GCP Console.

### Task-1: LAunch a Ubuntu VM and Install Terraform
* Navigate to `VM Instances`
* Click on `CREATE INSTANCE`
* Name : TerraformServer`
* Region : Of Your choice
* Zone : Any
* Machine : e2-medium
* Boot disk-image : `Ubuntu 24.04 LTS`
* Boot disk-Size : `10 GB`
* Once Launched, `ssh` into the instance

Once the VM is ready, follow the below Commands to perform lab:
```
sudo apt update
```
```
sudo apt install wget unzip -y
```
```
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
```
```
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
```
```
sudo apt update && sudo apt install terraform
```
```
terraform
```
```
terraform -v
```

### Task-2: Install Required Packages  
```
snap install google-cloud-cli --classic
```
```
gcloud init
```
```
gcloud auth application-default login
```
