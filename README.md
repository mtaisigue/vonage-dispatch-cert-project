# Messages & Dispatch API Certification Project

This repo contains the code for the Messages & Dispatch API Certification

## Prerequisites

* Create a Vonage Application with Messages enabled
* Link a Facebook page with the application - business (FB_SENDER_ID)
* A second Facebook account - normal user (FB_RECIPIENT_ID)
* Link Vonage on your FB Page

   - visit https://messenger.nexmo.com
   - follow the instructions
   - copy the "external id" of the page you selected -- you will need it later

* Link FB on your Vonage App

   - go to your Vonage Dashboard
   - locate your application
   - Under "Linked External Accounts" identify your FB Page and click "Link"

* A Vonage Phone Number linked to the Vonage App you are using

## Running the app

First clone the repo and install dependencies:

```
git clone https://github.com/mtaisigue/vonage-dispatch-cert-project.git
cd vonage-dispatch-cert-project
npm install
```

Next, copy env-example to .env and enter your information

* `NEXMO_API_KEY`: <Your nexmo API>
* `NEXMO_API_SECRET`: <Your nexmo API secret>
* `NEXMO_APPLICATION_ID`: <Your nexmo app ID>
* `NEXMO_APPLICATION_PRIVATE_KEY_PATH`: <The private key file location>
* `FB_SENDER_ID`: <Your FB page id, linked to your nexmo app>
* `FB_RECIPIENT_ID`: <The id of the facebook account you want to send messages to>
* `FROM_NUMBER`: <Your nexmo vitual number>
* `TO_NUMBER`: <Your regular phone number>

Start the application by running `node server.js`

Start ngrok to make the webhooks available publicly by running `ngrok http 3000`

Update the application webhooks with the url provided by ngrok plus /webhooks/inbound and /webhooks/status (e.g. http://ngrok_url/webhooks/inboud and http://ngrok_url/webhooks/status)

Note: At this point as facebook user should start a conversation with the business, so from your narmal facebook account send a message to the bussiness page. This will start the conversation and also give you the real FB_RECIPIENT_ID to update that variable. after this stept is completed you shouls continue with the next step. 

To trigger the message, send a POST request to `webhooks/send` as follows

```
curl -X POST -H "Content-Type: application/json" \
 -d '{"message":"This is a Facebook Messenger message sent from the Dispatch API"}' \
 http://localhost:3000/webhooks/send
```

Don't open the SMS in your phone yet and wait 90 seconds for the message arrive to your Facebook account.
