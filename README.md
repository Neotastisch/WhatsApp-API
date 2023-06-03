# WhatsApp-API BETA

[Changelog](https://github.com/Neotastisch/WhatsApp-API/blob/main/changelog.md)<br>
[Swagger](https://api.neotastisch.de/swagger/)

Welcome to the documentation for the WhatsApp-API BETA. This API allows you to send and receive messages through WhatsApp. Please note that this module is still a work in progress, so expect bugs. It is important to be cautious while using this API and avoid providing personal information. The API is provided for free, but please use it responsibly to avoid service discontinuation and potential bans.

## Sending Messages

To send a message, you can make a request to the following endpoint:

```http
GET /send?number=[TELEPHONENUMBER]&msg=[MESSAGE]&method=whatsapp
```

Replace `[TELEPHONENUMBER]` with the desired phone number you want to send the message to (e.g., 441134960000). Replace `[MESSAGE]` with the content of the message you want to send. The IP address of the sender will be automatically attached to the message to prevent abuse. Please note that there is a 10-second cooldown between each request to prevent abuse.

Here's an example of sending a message using Node.js and Axios:

```javascript
const axios = require('axios');

const phoneNumber = '441134960000'; // Replace with the desired phone number
const message = 'Hello world'; // Replace with the desired message

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

sendMessage();                           
```

## Receiving Messages

To receive messages, you need to register a webhook by making a request to the following endpoint:

There are a few variables you can define in the webhook URL: 
- Message Content: `?msg=`
- Author: `?from=`

```http
GET /webhook?number=[TELEPHONENUMBER]&webhook=[WEBHOOK URL]&method=whatsapp                                        
```

After that, type `AUTHORIZE` in WhatsApp to verify your identity.

If you want to remove the webhook, simply write `WEBHOOK DELETE` in WhatsApp.

Replace `[TELEPHONENUMBER]` with the phone number you want to register the webhook for. Replace `[WEBHOOK URL]` with the URL of the webhook endpoint where you want to receive the incoming messages. The received message will be included as a query parameter `msg` in the webhook URL.

Feel free to explore the [Changelog](https://github.com/Neotastisch/WhatsApp-API/blob/main/changelog.md) for updates and improvements to the API. You can also refer to the [Swagger documentation](https://api.neotastisch.de/swagger/) for detailed API specifications.

If you have any further questions or need assistance, please let us know.
