
https://dialogflow.cloud.google.com/

Agent Name: pigeon-travel

Default Time Zone: America/Denver

Google Project: use your lab Project ID



---
---



# Create Intent 

name.reservation

Can I change my name on my reservation?

Sure I can help you to change your name on the reservation. Can I have your first name?



name.reservation-getname

sam

@sys.given-name

---
---

- required: true
- parameter name: 
``` 
reservationnumber
```
- entity: 
```
@sys.number
```
- value: 
```
$reservationnumber
```
- prompts: 
```
What is your reservation number?
```


---

- required: true
- parameter name: 
``` 
newname
```
- entity: 
```
@sys.person
```
- value: 
```
$newname
```
- prompts: 
```
What is the NEW NAME for the reservation?
```

---

```
Thank you $given-name. I have changed the name on reservation number $reservationnumber to be $newname.
```