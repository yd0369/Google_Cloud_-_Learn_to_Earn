```
gcloud compute firewall-rules create app-allow-http --direction=INGRESS --priority=1000 --network=my-internal-app --action=ALLOW --rules=tcp:80 --source-ranges=0.0.0.0/0 --target-tags=lb-backend

gcloud compute firewall-rules create app-allow-health-check --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp --source-ranges=130.211.0.0/22,35.191.0.0/16 --target-tags=lb-backend

gcloud beta compute instance-templates create instance-template-1 --machine-type=n1-standard-1 --subnet=projects/$DEVSHELL_PROJECT_ID/regions/us-central1/subnetworks/subnet-a --network-tier=PREMIUM --metadata=startup-script-url=gs://cloud-training/gcpnet/ilb/startup.sh --maintenance-policy=MIGRATE --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append --region=us-central1 --tags=lb-backend --image=debian-10-buster-v20210916 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-balanced --no-shielded-secure-boot --no-shielded-vtpm --no-shielded-integrity-monitoring --reservation-affinity=any

gcloud beta compute instance-templates create instance-template-2 --machine-type=n1-standard-1 --subnet=projects/$DEVSHELL_PROJECT_ID/regions/us-central1/subnetworks/subnet-b --network-tier=PREMIUM --metadata=startup-script-url=gs://cloud-training/gcpnet/ilb/startup.sh --maintenance-policy=MIGRATE --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append --region=us-central1 --tags=lb-backend --image=debian-10-buster-v20210916 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-balanced --no-shielded-secure-boot --no-shielded-vtpm --no-shielded-integrity-monitoring --reservation-affinity=any

gcloud compute instance-groups managed create instance-group-1 --base-instance-name=instance-group-1 --template=instance-template-1 --size=1 --zone=us-central1-a

gcloud beta compute instance-groups managed set-autoscaling "instance-group-1" --zone "us-central1-a" --cool-down-period "45" --max-num-replicas "5" --min-num-replicas "1" --target-cpu-utilization "0.8" --mode "on"


gcloud compute instance-groups managed create instance-group-2 --base-instance-name=instance-group-2 --template=instance-template-2 --size=1 --zone=us-central1-a

gcloud beta compute instance-groups managed set-autoscaling "instance-group-2" --zone "us-central1-a" --cool-down-period "45" --max-num-replicas "5" --min-num-replicas "1" --target-cpu-utilization "0.8" --mode "on"

gcloud compute instances create utility-vm --zone=us-central1-a --machine-type=f1-micro --network-interface=network-tier=PREMIUM,subnet=default --network-interface=network-tier=PREMIUM,private-network-ip=10.10.20.50,subnet=subnet-a --maintenance-policy=MIGRATE --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append --create-disk=auto-delete=yes,boot=yes,device-name=utility-vm,image=projects/debian-cloud/global/images/debian-10-buster-v20210916,mode=rw,size=10,type=projects/$DEVSHELL_PROJECT_ID/zones/us-central1-a/diskTypes/pd-balanced --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --reservation-affinity=any
```



```
my-ilb
```

```
my-ilb-health-check
```

```
my-ilb-ip
```

```
10.10.30.5
```