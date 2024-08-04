# Storing Terraform Remote State in GCS with State Locking Enabled

## Prerequisites

- **Google Cloud SDK**: Installed and authenticated.
- **Terraform**: Installed.
- **GCP Project**: An existing project.
- **Service Account**: A service account with appropriate permissions.

## Steps

### 1. Create a GCS Bucket with Versioning

1. Open the [Google Cloud Console](https://console.cloud.google.com/).
2. Navigate to **Storage** > **Browser**.
3. Click **Create bucket**.
4. Provide a unique name for your bucket and select a region.
5. Configure the bucket settings, and in the **Choose how to control access to objects** section, select **Uniform**.
6. Enable **Object Versioning** in the **Advanced settings** section.
7. Click **Create**.

### 2. Set Up Terraform

Create a director lab4 and navivate to it
```bash 
mkdir lab4 && cd lab4
```
Create a files named `main.tf`, `provider.tf` and `backend.tf`
```bash
vi main.tf
```
```hcl
resource "google_compute_instance" "vm_instance" {
  name         = "terraform-instance-test"
  machine_type = "g1-small"

  boot_disk {
    initialize_params {
      image = "debian-12-bookworm-v20240709"
    }
  }

  network_interface {
    # A default network is created for all GCP projects
    network = "default1"
    access_config {
    }
  }
}
```
```bash
vi provider.tf
```
```hcl
provider "google" {
  project     = "deloitte-team2"
  zone        = "us-central1-c"
  region      = "us-central1"
}
```
```bash
vi backend.tf
```
```hcl
terraform {
  backend "gcs" {
    bucket  = "terraform-backend-opentext"
    prefix  = "terraform/state"
  }
}
```
Replace `terraform-backend-opentext` with the name of your GCS bucket.

### 3. Initialize Terraform

Initialize the backend with the following command:

```sh
terraform init
```

Terraform will configure the remote backend and migrate your state file to the GCS bucket. This step also sets up state locking.

### 6. Apply Your Terraform Configuration

1. Run the following command to apply your Terraform configuration:

    ```sh
    terraform apply
    ```

    This will use the remote state stored in the GCS bucket with state locking enabled.

## Additional Tips

- **State Locking**: Terraform automatically manages state locking using GCS by creating a lock file in the specified bucket. No additional configuration is required as long as you have set up the backend properly.
- **Monitoring State Locking**: You can monitor the lock status by checking for lock files in your GCS bucket. Terraform lock files have the `.tflock` extension.

By following these steps, you ensure that your Terraform state is securely stored in GCS with state locking enabled, allowing for safe and concurrent access to the state file.
