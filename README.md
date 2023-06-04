# WhatsApp-API BETA

**Changelog**: [View Changelog](https://github.com/Neotastisch/WhatsApp-API/blob/main/Changelog.md)<br>
**Swagger**: [API Swagger Documentation](https://api.neotastisch.de/swagger/)

**BaseURL**: https://api.neotastisch.de

**Support and Updates**: [Discord](https://discord.gg/pZKFGWVvfF)

[TOS](https://github.com/Neotastisch/WhatsApp-API/blob/main/Terms_of_service.md) [Privacy Policy](https://github.com/Neotastisch/WhatsApp-API/blob/main/Privacy_Policy.md) [Usage Policy](https://github.com/Neotastisch/WhatsApp-API/blob/main/Usage_Policy.md)

Welcome to the documentation for the WhatsApp-API BETA. This API allows you to send and receive messages through WhatsApp. Please note that this module is currently in beta, and occasional bugs may occur. It is crucial to use this API responsibly and refrain from providing any personal information. Although the API is offered free of charge, we kindly request that you comply with our guidelines to avoid service discontinuation or potential bans.

## Sending Messages

To send a message, send a `GET` request to the following endpoint:

```
GET /send?number=[TELEPHONENUMBER]&msg=[MESSAGE]&method=whatsapp
```

Replace `[TELEPHONENUMBER]` with the desired recipient's phone number (e.g., 441134960000)(Without + and spaces). Replace `[MESSAGE]` with the content of the message you wish to send. The sender's IP address will be automatically included in the message to prevent abuse. Please note that there is a 10-second cooldown period between each request to prevent misuse.

Here's an example of sending a message using Node.js and Axios:

```javascript
const axios = require('axios');

const phoneNumber = '441134960000'; // Replace with the desired recipient's phone number (Without + and spaces)
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

To receive messages, you need to register a webhook by sending a `GET` request to the following endpoint:

You can include the following variables in the webhook URL:
- `?msg?`: The content of the message (for new messages, empty for reactions)
- `?from?`: The phone number of the message sender
- `?msgid?`: The ID of the message (for new messages or the message ID of the reacted message)
- `?reaction?`: The reaction (if any). The message content will still be passed in the webhook URL.
- `?type?`: The type of message, either "reaction" or "message"

Replace `[TELEPHONENUMBER]` with the phone number for which you want to register the webhook. Replace `[WEBHOOK URL]` with the URL of the webhook endpoint where you want to receive incoming messages. The received message will be included as a query parameter `msg` in the webhook URL.

To authorize your identity, type `AUTHORIZE` in WhatsApp.

To remove the webhook, simply type `WEBHOOK DELETE` in WhatsApp.

```http
GET /webhook?number=[TELEPHONENUMBER]&webhook=[WEBHOOK URL]&method=whatsapp                                        
```

Feel free to explore the [Changelog](https://github.com/Neotastisch/WhatsApp-API/blob/main/Changelog.md) for updates and improvements to the API. For detailed API specifications, refer to the [Swagger documentation](https://api.neotastisch.de/swagger/).

If you have any further questions or require assistance, please do not

 hesitate to reach out to us on [Discord](https://discord.gg/pZKFGWVvfF).
