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
sudo apt install terraform
```
```
terraform
```
```
terraform -v
```

### Task-2: Install Required Packages and login to Ubuntu server using Credentials. 
```
sudo apt-get install python3-pip -y
```
```
sudo pip3 install awscli --break-system-packages
```
```
aws configure
```
* When it prompts for Credentials, Enter the Keys as example shown below
  
| `Access Key ID.` | `Secret Access Key ID.` |
| ------------------ | ------------------------- |
| AKIAIOSFODNN7EXAMPLE | wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY |

##### Note: If Credentials are not available generate from AWS IAM Service
Once LoggedIn check the account access
```
aws s3 ls
```
`Or` Use below command to check whether it is authenticated.
```
aws iam list-users
```
### Task-3: Now we are ready to perform the labs
Create directory as Lab1 & create local file
```
mkdir Lab1 && cd Lab1
```
```
vi local.tf
```
```
resource "local_file" "myfile" {

  filename = "/home/ubuntu/test.txt"
  content  = "wel come to terraform"
}
```
```
terraform init
```
```
terraform plan
```
```
terraform apply
```
To check whether the file is created follow the command

```
cd /home/ubuntu
ls
```
```
cat test.txt
```
Once Verified, you can destroy the File by changing it to the Lab1 Directory
```
cd Lab1
```
```
terraform destroy
```
```
cd ~
rm -rf Lab1
```
