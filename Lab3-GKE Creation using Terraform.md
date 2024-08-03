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
