# Cloud Functions: Qwik Start - Command Line


```
export id="
```


--- 



```
mkdir gcf_hello_world
cd gcf_hello_world
echo "/**
* Background Cloud Function to be triggered by Pub/Sub.
* This function is exported by index.js, and executed when
* the trigger topic receives a message.
*
* @param {object} data The event payload.
* @param {object} context The event metadata.
*/
exports.helloWorld = (data, context) => {
const pubSubMessage = data;
const name = pubSubMessage.data
    ? Buffer.from(pubSubMessage.data, 'base64').toString() : \"Hello World\";
console.log(\`My Cloud Function: \${name}\`);
};" > index.js

gsutil mb -p $id gs://$id

gcloud functions deploy helloWorld --stage-bucket $id --trigger-topic hello_world --runtime nodejs8

```