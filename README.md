# 1.Setting Up and Managing GKE Clusters

# Terraform utilised to create a GKE

```resource "google_container_cluster" "primary" {
name.                    = "my_cluster"
location.                = "europe-west3" #Berlin region
initial_node_count       = 6

node_config {
machine_type = "e2-large"
oauth_scopes = [https://www.googleapis.com/auth/cloud-platform"]
}

autoscaling {
enabled         = true
min_node_count = 2
max_node_count = 10
}
}```
