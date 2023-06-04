# WhatsApp-API BETA

**Changelog**: [View Changelog](https://github.com/Neotastisch/WhatsApp-API/blob/main/changelog.md)<br>
**Swagger**: [API Swagger Documentation](https://api.neotastisch.de/swagger/)

**BaseURL**: https://api.neotastisch.de

**Support and Updates**: [Discord](https://discord.gg/pZKFGWVvfF)

Welcome to the documentation for the WhatsApp-API BETA. This API enables you to send and receive messages through WhatsApp. Please note that this module is still a work in progress, so please expect occasional bugs. It is important to exercise caution while using this API and avoid providing personal information. While the API is provided for free, we kindly request that you use it responsibly to prevent service discontinuation or potential bans.

## Sending Messages

To send a message, make a `GET` request to the following endpoint:

```
GET /send?number=[TELEPHONENUMBER]&msg=[MESSAGE]&method=whatsapp
```

Replace `[TELEPHONENUMBER]` with the desired phone number you want to send the message to (e.g., 441134960000). Replace `[MESSAGE]` with the content of the message you want to send. The sender's IP address will be automatically attached to the message to prevent abuse. Please note that there is a 10-second cooldown period between each request to prevent abuse.

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

To receive messages, you need to register a webhook by making a `GET` request to the following endpoint:

You can define the following variables in the webhook URL:
- `?msg?`: The message content (either new message or the message that was reacted to)
- `?from?`: The number of the person who sent the message
- `?reaction?`: The reaction (if any). The message content will still be passed to the URL.
- `?type?`: The type of message, either "reaction" or "message"

Replace `[TELEPHONENUMBER]` with the phone number you want to register the webhook for. Replace `[WEBHOOK URL]` with the URL of the webhook endpoint where you want to receive the incoming messages. The received message will be included as a query parameter `msg` in the webhook URL.

To authorize your identity, type `AUTHORIZE` in WhatsApp.

To remove the webhook, simply write `WEBHOOK DELETE` in WhatsApp.

```http
GET /webhook?number=[TELEPHONENUMBER]&webhook=[WEBHOOK URL]&method=whatsapp                                        
```

Feel free to explore the [Changelog](https://github.com/Neotastisch/WhatsApp-API/blob/main/changelog.md) for updates and improvements to the API. You can also refer to the [Swagger documentation](https://api.neotastisch.de/swagger/) for detailed API specifications.

If you have any further questions or need assistance, please don't hesitate to reach out to us.
