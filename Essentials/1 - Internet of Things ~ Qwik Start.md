# Internet of Things - Qwik Start

    Project ID : qwiklabs-gcp-01-f8db20383f61
    export PID="qwiklabs-gcp-01-f8db20383f61"
- [ ] 
    ```
    
    openssl req -x509 -newkey rsa:2048 -keyout rsa_private.pem -nodes -out rsa_cert.pem -subj "/CN=unused"
    cat rsa_cert.pem

    ```


---
---


- [ ] Go to Pub-Sub Topics
    ```
    https://console.cloud.google.com/cloudpubsub/topic/list
    ```

- [ ] **CREATE TOPIC** --> ID : "cloud-builds"
	```
    cloud-builds
	```
- click **CREATE TOPIC**

---
---


- [ ] New Tab --> IoT Core
    ```
    https://console.cloud.google.com/iot/registries
    ```

	- Registry ID --> **COPY & PASTE** --> "my-registry"
	```
	my-registry
	```
	- Select Region --> us-central1
	- Click on Show Advanced Option
	- Uncheck HTTP
	- Click on CREATE



---

- [ ] Create Device
    ```
    https://console.cloud.google.com/iot/locations/us-central1/registries/my-registry/devices
    ```

- [ ] Follow Steps 
    - Device ID : 
        ```
        my-device
        ```
    - click communicaiton, cloud logging,authentication
    
    - Under Authentication (optional)
    - select 3rd Option >>> RS 256_ X5 09
    - Paste Key
    - click **CREATE**

---

- [ ] Run Following commands

    ```
    git clone https://github.com/googleapis/nodejs-iot
    
    cd nodejs-iot/samples/mqtt_example
    
    cp ../../../rsa_private.pem .
    
    npm install
    
    gcloud pubsub subscriptions create     projects/$PID/subscriptions/my-subscription    --topic=projects/$PID/topics/cloud-builds
    
    wget https://pki.goog/roots.pem
    
    node cloudiot_mqtt_example_nodejs.js \
    mqttDeviceDemo \
    --projectId=$PID \
    --cloudRegion=us-central1 \
    --registryId=my-registry \
    --deviceId=my-device \
    --privateKeyFile=rsa_private.pem \
    --numMessages=25 \
    --algorithm=RS256 \
    --serverCertFile=roots.pem \
    --mqttBridgePort=443

    gcloud pubsub subscriptions pull --auto-ack \
    projects/$PID/subscriptions/my-subscription
    ```






Google Cloud IoT platform, provides a complete solution for collecting, processing, analyzing, and visualizing IoT data in real time to support improved operational efficiency.

True


---
---
---

# Check Summary : 4

- [ ] Create a device registry
- [ ] Add a device to the registry
- [ ] Add a public key to the device
- [ ] Create a subscription



-