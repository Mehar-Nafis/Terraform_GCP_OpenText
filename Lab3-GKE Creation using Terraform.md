### Task1: Launching your first GKE Cluster using Terraform
```
cd ~
mkdir Lab3
```
```
vi provider.tf
```
```hcl
provider "google" {
  project     = "deloitte-team2"
  zone        = "us-central1-c"
  region      = "us-central1"
}
```
```
vi main.tf
```
```hcl

resource "google_container_cluster" "gke-cluster" {
  name               = "ninad-gke-cluster"
  network            = "default1"
  location             = "us-central1-c"
  initial_node_count = 1
  deletion_protection = false
}

resource "google_container_node_pool" "extra-pool" {
  name               = "extra-node-pool"
  location             = "us-central1-c"
  cluster            = google_container_cluster.gke-cluster.name
  initial_node_count = 2
}

```
Save the file using "ESCAPE + :wq!"
```
terraform init
```
```
terraform fmt
```
```
terraform validate
```
```
terraform plan
```
```
terraform apply
```
```
#List the files
ls 
```
To see what is saved in `terraform.tfstate` use the below command.

```
terraform show
```
Navigate from the Console to `Kubernetes Cluster` to view the created cluster.
The nodes are visible on the Compute Engine Dashboard.

### Task2: Connecting to the Cluster
```
sudo snap install kubectl --classic
```
Use the `terraform destroy` command for cleaning the infrastructure used in this lab
```
terraform destroy
```
Finally, verify that the resources are deleted in the Console.
```
cd ~
rm -rf Lab3
```
