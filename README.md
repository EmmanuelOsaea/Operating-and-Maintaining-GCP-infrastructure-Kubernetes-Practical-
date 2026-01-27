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
}

# 2. Deploying and Managing Application

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
