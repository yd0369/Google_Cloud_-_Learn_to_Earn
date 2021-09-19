# Cloud Monitoring: Qwik Start



Enter the new Project ID : qwiklabs-gcp-02-ed520e82c97c

---
---

### Create a Compute Engine Instance



- [ ] Create a Compute Engine instance
    ```
    gcloud beta compute --project=qwiklabs-gcp-02-ed520e82c97c instances create lamp-1-vm --zone=us-central1-a --machine-type=n1-standard-2 --subnet=default --network-tier=PREMIUM --maintenance-policy=MIGRATE --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append --tags=http-server --image=debian-10-buster-v20210916 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-balanced --boot-disk-device-name=lamp-1-vm --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --reservation-affinity=any
    ```


- [OPTIONAL] Check by Going to Compute Engine > VM INstances
    ```
    https://console.cloud.google.com/compute/instances
    ```

- [ ] **Hit that "Create a Compute Engine instance (zone: us-central1-a)"**

---
---

### Add Apache2 HTTP Server to your instance

- [ ] SSH to lamp-1-vm
    ```
    https://ssh.cloud.google.com/projects/qwiklabs-gcp-02-ed520e82c97c/zones/us-central1-a/instances/lamp-1-vm
    ```

- [ ] Run following commands in VM
    ```
    curl -sSO https://dl.google.com/cloudagents/add-monitoring-agent-repo.sh
    sudo bash add-monitoring-agent-repo.sh
    curl -sSO https://dl.google.com/cloudagents/add-logging-agent-repo.sh
    sudo bash add-logging-agent-repo.sh
    sudo apt-get update
    sudo apt-get install apache2 php7.0 stackdriver-agent google-fluentd -y
    sudo service apache2 restart
    ```


- [ ] **Hit that "Add Apache2 HTTP Server to your instance"**
- [ ] **Hit that "Get a success response over External IP of VM instance"**
---
---


### Create an uptime check 

- [ ] Go to Monitioring > Uptime Check
    ```
    https://console.cloud.google.com/monitoring/uptime
    ```

- [ ] Fill Following Details

    + CREATE UPTIME CHECK
    - Title : 
        ```
        Lamp Uptime Check
        ```
    - Click Next
    - Under **Resource Type** select **Instance**
    - **Instance*** >> lamp-1-vm
    - [ x2 ] Click next 
    - click CREATE

- [ ] **Hit that "Create an uptime check and alerting policy"**




---
---
---


# Overall Checks : 4


- Create a Compute Engine instance

- Add Apache2 HTTP Server to your instance

- Get a success response over External IP of VM instance

- Create an uptime check and alerting policy.