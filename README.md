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

# 2.Deploying and Managing Application

# Workload Deployment

```apiVersion: apps/v1
kind: Deployment
metadata:
name: word-puzzle-game
spec:
replicas: 6
selector:
matchLabels:
app: word-puzzle-game
template
metadata
labels
app: word-puzzle-game
spec
containers
-name game-container
image
ports
-containerPort:
```

# Autoscaling
HPA YAML
```apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
name: word-puzzle-game-hpa
spec:
scaleTargetRef:
apiVersion: apps/v1
kind: Deployment
name: word-puzzle-game
min-replicas: 4
max-replicas: 20
metrics:
-type: resource
resource:
name: cpu
target:
type: utilization
averageUtilization: 70
```

# Practical Guide: Buiding & Managing Iac with Terraform and Terramate

# 1.Setting Up a Terraform Project

Googlemain.tf used to develop a Google cloud VM instance

provider "google" {
project = "my-wordpuzzleapp-project"
region = "europe-west3"
}

resource "google_compute_instance" "default" {
name = "vm-instance"
machine_type = "e2-large"
zone = "europe-west3-b"

boot_disk {
initialize params
image
}
}

network_interface
network = "default"
access_config {}
}
}

# CI/CD Integration

Github Actions

jobs
terraform
runs-ons: macos-latest
steps
- uses: actions/checkout@v3 //Checks repo
- name: Install Terramate
- run: |
  curl sSL https://terramate.io/install.sh | bash
- shell: bash //default bash

- name: Terramate Terraform Plan
- run: |
 terramate run terraform plan
- shell: bash


