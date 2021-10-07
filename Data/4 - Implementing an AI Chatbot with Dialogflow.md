```
https://google.qwiklabs.com/focuses/634?catalog_rank=%7B%22rank%22%3A2%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog
```

---
---
---

```
https://console.cloud.google.com/marketplace/product/google/dialogflow.googleapis.com
```

```
https://console.cloud.google.com/datastore/welcome
```


```
https://dialogflow.cloud.google.com/
```


- Agent name: 
  ```
  Helpdesk
  ```
- Default Time zone: America/Denver
- Google Project: Your Project ID


---
### Create Intent

```
Submit Ticket
```

---

- Under Training Phase :
    ```
    Ticket
    ```

    ```
    Submit ticket
    ```

    ```
    Problem
    ```

    ```
    Issue
    ```

    ```
    I want to submit a ticket
    ```

    ```
    I have a problem
    ```
---

- Under Responses

    ```
    Sure! I can help you with that. Please provide your name for the ticket.
    ```

---

### Create a Followup for Submit Ticket [Submit Ticket - custom]

```
Submit Ticket - collect name
```

- Training phrases

```
My name is Lily
```

- Under Responses 

```
Thanks $person! Now describe your issue.
```


---

### Create a Followup for Submit Ticket [Submit Ticket - collect name - custom]

```
Submit Ticket - collect description
```

- Training phrases

```
My name is Lily
```

- Under Responses 

```
Thanks $person! Now describe your issue.
```




---
---
---

## Under Fullfilment



```
'use strict';
const http = require('http');
// Imports the Google Cloud client library
const Datastore = require('@google-cloud/datastore');
// Your Google Cloud Platform project ID
const projectId = '@@@';
// Instantiates a client
const datastore = Datastore({
  projectId: projectId
});
// The kind for the new entity
const kind = 'ticket';
exports.dialogflowFirebaseFulfillment = (req, res) => {
  console.log('Dialogflow Request body: ' + JSON.stringify(req.body));
  // Get the city and date from the request
  let ticketDescription = req.body.queryResult['queryText']; // incidence is a required param
  //let name = req.body.result.contexts[0].parameters['person.original'];
  let username = req.body.queryResult.outputContexts[1].parameters['person.original'];
  let phone_number = req.body.queryResult.outputContexts[1].parameters['phone-number.original'];
  console.log('description is ' +ticketDescription);
  console.log('name is '+ username);
  console.log('phone number is '+ phone_number);
  function randomIntInc (low, high) {
    return Math.floor(Math.random() * (high - low + 1) + low);
  }
  let ticketnum = randomIntInc(11111,99999);
  // The Cloud Datastore key for the new entity
  const taskKey = datastore.key(kind);
  // Prepares the new entity
  const task = {
    key: taskKey,
    data: {
      description: ticketDescription,
      username: username,
      phoneNumber: phone_number,
      ticketNumber: ticketnum
    }
  };
  console.log("incidence is  " , task);
  // Saves the entity
  datastore.save(task)
  .then(() => {
    console.log(`Saved ${task.key}: ${task.data.description}`);
    res.setHeader('Content-Type', 'application/json');
    //Response to send to Dialogflow
    res.send(JSON.stringify({ 'fulfillmentText': "I have successfully logged your ticket, the ticket number is " + ticketnum + ". Someone from the helpdesk will reach out to you within 24 hours."}));
    //res.send(JSON.stringify({ 'fulfillmentText': "I have successfully logged your ticket, the ticket number is " + ticketnum + ". Someone from the helpdesk will reach out to you within 24 hours.", 'fulfillmentMessages': "I have successfully logged your ticket, the ticket number is " + ticketnum +  ". Someone from the helpdesk will reach out to you within 24 hours."}));
  })
  .catch((err) => {
    console.error('ERROR:', err);
    res.setHeader('Content-Type', 'application/json');
    res.send(JSON.stringify({ 'speech': "Error occurred while saving, try again later", 'displayText': "Error occurred while saving, try again later" }));    
  });
};
```




```
{
  "name": "dialogflowFirebaseFulfillment",
  "description": "This is the default fulfillment for a Dialogflow agents using Cloud Functions for Firebase",
  "version": "0.0.1",
  "private": true,
  "license": "Apache Version 2.0",
  "author": "Google Inc.",
  "engines": {
    "node": "10"
  },
  "scripts": {
    "start": "firebase serve --only functions:dialogflowFirebaseFulfillment",
    "deploy": "firebase deploy --only functions:dialogflowFirebaseFulfillment"
  },
  "dependencies": {
    "actions-on-google": "^2.2.0",
    "firebase-admin": "^5.13.1",
    "firebase-functions": "^2.0.2",
    "dialogflow": "^0.6.0",
    "dialogflow-fulfillment": "^0.5.0",
    "@google-cloud/datastore": "^1.1.0"
  }
}
```