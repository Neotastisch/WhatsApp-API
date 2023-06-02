# WhatsApp-API BETA



[Changelog](https://github.com/Neotastisch/WhatsApp-API/blob/main/changelog.md)
[Swagger](https://api.neotastisch.de/swagger/)



The first **FREE** WhatsApp API for sending and recieving messages



**Please note:** This module is still Work-In-Progress, expect bugs
**Disclaimer:**
I highly suggest not putting in personal information
Im not responsible for any problems that may occur. Please use it responsable, as this service may else be disconntinued and you banned.


## Sending messages

```js
https://api.neotastisch.de/send?number=[TELEPHONENUMBER]&msg=[MESSAGE]&method=whatsapp
```
-> Replace [TELEPHONENUMBER] with your number. Example: 441134960000
-> Replace [MESSAGE] with your desired message.
The User, which this message was sent to, will automaticly get the IP Adress of the sender to avoid abuse.
This API also has a 10Second Cooldown between each request to avoid abuse.

##Example in Node.JS using Axios (Sending)
```js
const axios = require('axios');

const phoneNumber = '441134960000'; // Replace with your phone number
const message = 'Hello world'; // Replace with your desired message

// Function to send the message
async function sendMessage() {
  try {
    const response = await axios.get("https://api.neotastisch.de/send", {
      params: {
        number: phoneNumber,
        msg: message,
        method: 'whatsapp'
      }
    });
  } catch (error) {
    console.error('An error occurred while sending the message:', error);
  }
}

// Call the function to send the message
sendMessage();                           
```


## Recieving messages

Register a webhook
```js
  https://api.neotastisch.de/webhook?number=[TELEPHONENUMBER]&webhook=[WEBHOOK URL]&method=whatsapp                                        
```
*?msg? will be replaced with the recieved message.*





