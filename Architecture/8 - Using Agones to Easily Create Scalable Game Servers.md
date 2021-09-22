# Using Agones to Easily Create Scalable Game Servers

=========================================================================================



qwiklabs-gcp-03-f95dcff12a51




=======================================================================================


gcloud config set compute/zone us-central1-a
export CLUSTER_NAME="lusture"


gcloud beta compute instances create agones-test-vm --zone=us-central1-a --machine-type=e2-medium --subnet=default --network-tier=PREMIUM --maintenance-policy=MIGRATE --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append --image=debian-10-buster-v20210916 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-balanced --boot-disk-device-name=agones-test-vm --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --reservation-affinity=any

gcloud container clusters create $CLUSTER_NAME \
  --no-enable-legacy-authorization \
  --tags=game-server \
  --scopes=gke-default \
  --num-nodes=3 \
  --machine-type=n1-standard-2 \
  --region=us-central1-a


gcloud config set container/cluster $CLUSTER_NAME
gcloud container clusters get-credentials --region=us-central1-a $CLUSTER_NAME


gcloud compute firewall-rules create game-server-firewall \
  --allow udp:7000-8000 \
  --target-tags game-server \
  --description "Firewall to allow game server udp traffic"

  kubectl create clusterrolebinding cluster-admin-binding \
  --clusterrole cluster-admin --user `gcloud config get-value account`

kubectl create namespace agones-system


kubectl apply -f https://raw.githubusercontent.com/GoogleCloudPlatform/agones/release-1.6.0/install/yaml/install.yaml

kubectl create -f https://raw.githubusercontent.com/googleforgames/agones/release-1.6.0/examples/simple-udp/gameserver.yaml

kubectl get pods

kubectl create -f https://raw.githubusercontent.com/googleforgames/agones/release-1.6.0/examples/simple-udp/gameserver.yaml

kubectl get gameservers

=============================================================



https://ssh.cloud.google.com/projects/qwiklabs-gcp-03-f95dcff12a51/zones/us-central1-a/instances/agones-test-vm


sudo apt install netcat -y
nc -u 










---
---
---



Create a Kubernetes cluster
Create a firewall rule to allow the UDP traffic
Enable creation of RBAC resources
Create agones-system namespace and install Agones with YAML
Create a GameServer
Create a new VM instance
Shut down the GameServer

