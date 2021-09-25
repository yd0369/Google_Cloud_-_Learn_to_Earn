```
gcloud beta compute ssh --zone "us-central1-a" "blue"

```

```
sudo apt-get install nginx-light -y
sudo sed -i 's/<h1>Welcome to nginx/<h1>Welcome to the blue server/g' /var/www/html/index.nginx-debian.html

```


```
gcloud beta compute ssh --zone "us-central1-a" "green"

```

```
sudo apt-get install nginx-light -y
sudo sed -i 's/<h1>Welcome to nginx/<h1>Welcome to the green server/g' /var/www/html/index.nginx-debian.html

```


```
gcloud beta compute instances create blue --zone=us-central1-a --machine-type=e2-medium --subnet=default --network-tier=PREMIUM --maintenance-policy=MIGRATE --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append --tags=web-server --image=debian-10-buster-v20210916 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-balanced --boot-disk-device-name=blue --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --reservation-affinity=any
gcloud beta compute instances create green --zone=us-central1-a --machine-type=e2-medium --subnet=default --network-tier=PREMIUM --maintenance-policy=MIGRATE --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append --image=debian-10-buster-v20210916 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-balanced --boot-disk-device-name=blue --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --reservation-affinity=any
gcloud compute firewall-rules create allow-http-web-server --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:80,icmp --source-ranges=0.0.0.0/0 --target-tags=web-server
gcloud compute instances create test-vm --machine-type=f1-micro --subnet=default --zone=us-central1-a
gcloud iam service-accounts create network-admin --display-name "Network-admin"

```