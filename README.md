# kandy-cpaas2-sample-sms-node-red

This is a sms application where a user can send an sms. Subscribe sms notification and receive real-time sms events (inbound, outbound etc notification).
## Development
These instructions will get you a copy of the project. Running on your local machine for development and testing purposes.

### Prerequisites
Your system should have the following installed to complete pass this project:
- [NodeJS](https://nodejs.org/en/) >= 10.15.0
- Chrome browser - Last 3 major version

### Setup
1. To setup the project repository, run these commands
```bash
git clone https://github.com/hclsampleapps/kandy-cpaas2-sample-sms-node-red.git
cd kandy-cpaas2-sample-sms-node-red
```
2. To install nodered, run these commands
```bash
npm install -g --unsafe-perm node-red
```

### Installation
1. To install dependencies, run
```bash
npm install @kandy-io/node-red-contrib-cpaas-sdk
```
2. To start the server, run
```bash
node-red
```

### Branching strategy
To learn about the branching strategy, contribution & coding conventions followed in the project. Please refer [GitFlow based branching strategy for your project repository](https://gist.github.com/ribbon-abku/10d3fc1cff5c35a2df401196678e258a)

## Usage
The application comprises of simple flows of send code and code verification.
- Open the localhost url in the browser. On the right side click on three bar menu and then click on import. Select the file `sms.json` from the repository and then import.
- Click on `Deploy` for deployment of flow.

### Section 1 - Send SMS

- Double click on `Send SMS` node. Edit the `CPaaS Credentials`.
- Choose any `Authentication type` and enter the other fields. And then click on `Update` button.
- Choose the `method` verification type by email or sms. And enter the `Destination address` in case of sms. And in case of email enter the `Subject` of email also.
- Click on `Done` button.
- Click on`Inject` node of `Send SMS` for send sms.

### Section 2 - SMS notification
This represents the subscription to SMS notification and can found on the top right section. Here a Webhook URL is to added.

As incoming notifications are to received by the local server. There is a need of a web server to be running and that web server to have a public IP address. Use this it recommended to install and use [ngrok](https://ngrok.com/).

- Double click on `Analyse Notification` node. Edit the `CPaaS Credentials`.
- Enter the Webhook url and destination address.

#### How to use ngrok

Once `ngrok` installed, run the following command

```bash
ngrok http 5000
```

Where 5000 is the default `PORT` where the flask app runs. You need to run the ngrok command mentioning the exact port.
Once `ngrok` starts forwarding the `localhost`, you would find a similar kind of message in your screen.

```bash
ngrok by @inconshreveable                                                                  (Ctrl+C to quit)

Session Status                online
Session Expires               7 hours, 58 minutes
Update                        update available (version 2.3.34, Ctrl-U to update)
Version                       2.3.28
Region                        United States (us)
Web Interface                 http://127.0.0.1:4040
Forwarding                    http://29de1e3e.ngrok.io -> http://localhost:3001
Forwarding                    https://29de1e3e.ngrok.io -> http://localhost:5000

Connections                   ttl     opn     rt1     rt5     p50     p90
                              0       0       0.00    0.00    0.00    0.00
```

After this the usage part of `ngrok` done and we got out public domain. Let's shift out attention to the notification subscription.

Copy the `forwarding` domain and paste it to in the `Webhook host URL` input field.
Click `Subscribe` a notification channel would created with the above domain. That described in the `.env` file (PHONE_NUMBER) and all the sms notifications would start coming in.

**Note**: While entering the ngrok domain and subscribing, make sure that there is not forward slash at the end of the domain.

- **Correct** `https://29de1e3e.ngrok.io`
- **Incorrect** `https://29de1e3e.ngrok.io/`
