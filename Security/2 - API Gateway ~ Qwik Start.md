# API Gateway: Qwik Start


```
https://console.cloud.google.com/apis/library/apigateway.googleapis.com
```

---

```
https://console.cloud.google.com/apis/credentials
```

```
export API_KEY=
```
---

```
git clone https://github.com/GoogleCloudPlatform/nodejs-docs-samples.git

cd nodejs-docs-samples/functions/helloworld/

gcloud functions deploy helloGET --runtime nodejs10 --trigger-http --allow-unauthenticated

export PROJECT_ID=$(gcloud config get-value project)

curl -v https://us-central1-${PROJECT_ID}.cloudfunctions.net/helloGET

cd ~

echo "# openapi2-functions.yaml
swagger: '2.0'
info:
  title: API_ID description
  description: Sample API on API Gateway with a Google Cloud Functions backend
  version: 1.0.0
schemes:
  - https
produces:
  - application/json
paths:
  /hello:
    get:
      summary: Greet a user
      operationId: hello
      x-google-backend:
        address: https://us-central1-PROJECT_ID.cloudfunctions.net/helloGET
      responses:
       '200':
          description: A successful response
          schema:
            type: string" > openapi2-functions.yaml


export API_ID="hello-world-$(cat /dev/urandom | tr -dc 'a-z' | fold -w ${1:-8} | head -n 1)"


sed -i "s/API_ID/${API_ID}/g" openapi2-functions.yaml
sed -i "s/PROJECT_ID/$PROJECT_ID/g" openapi2-functions.yaml

export API_ID="hello-world-$(cat /dev/urandom | tr -dc 'a-z' | fold -w ${1:-8} | head -n 1)"
echo "Hello World API"
echo $API_ID

cloudshell download $HOME/openapi2-functions.yaml


echo "Hello World Config"
echo "Hello Gateway"


```


---

Creating API Gateway
```
https://console.cloud.google.com/api-gateway/gateway/create
```


Display Name : 
```
Hello World API
```

```
Hello World Config
```







---

```
export GATEWAY_URL=$(gcloud api-gateway gateways describe hello-gateway --location us-central1 --format json | jq -r .defaultHostname)

echo $GATEWAY_URL

curl -s -w "\n" https://$GATEWAY_URL/hello

```

---

```
gcloud api-gateway apis list --format json | jq -r .[0].managedService | cut -d'/' -f6


echo "# openapi2-functions.yaml
swagger: '2.0'
info:
  title: API_ID description
  description: Sample API on API Gateway with a Google Cloud Functions backend
  version: 1.0.0
schemes:
  - https
produces:
  - application/json
paths:
  /hello:
    get:
      summary: Greet a user
      operationId: hello
      x-google-backend:
        address: https://us-central1-PROJECT_ID.cloudfunctions.net/helloGET
      security:
        - api_key: []
      responses:
       '200':
          description: A successful response
          schema:
            type: string
securityDefinitions:
  api_key:
    type: \"apiKey\"
    name: \"key\"
    in: \"query\"
" > openapi2-functions2.yaml



sed -i "s/API_ID/${API_ID}/g" openapi2-functions2.yaml
sed -i "s/PROJECT_ID/$PROJECT_ID/g" openapi2-functions2.yaml

cloudshell download $HOME/openapi2-functions2.yaml



echo "Hello Config"
```

---

```
https://console.cloud.google.com/api-gateway/gateway/hello-gateway/location/us-central1/edit
```

```
Hello Config
```
---


```
export GATEWAY_URL=$(gcloud api-gateway gateways describe hello-gateway --location us-central1 --format json | jq -r .defaultHostname)
curl -sL $GATEWAY_URL/hello

curl -sL -w "\n" $GATEWAY_URL/hello?key=$API_KEY
```
