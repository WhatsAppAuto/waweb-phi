# WAWEB-phi
![npm](https://img.shields.io/npm/v/waweb-phi)  ![NPM](https://img.shields.io/npm/l/waweb-phi) ![GitHub last commit](https://img.shields.io/github/last-commit/oqhadev/waweb-phi)

WAWEB-phi is library for controlling whatsapp web for nodejs,
inspired from [whatsapp-web.js](https://github.com/pedroslopez/whatsapp-web.js) and WAPI.js


What is the difference? This library uses wapi.js which contains features such as sending pictures, sending to numbers that are not in the contact list
and many more

## Installation
NPM
```bash
npm install waweb-phi 
```
YARN
```bash
yarn add waweb-phi 
```

## Usage

```js
const wa = require('waweb-phi')

const client = new wa({
    puppeteer: { headless: false }

});


client.initialize();
```



## Example
```js
const wa = require('waweb-phi')

const client = new wa({
    puppeteer: { headless: false }

});


client.initialize();


client.on('qr', (qr) => {
    console.log('QR RECEIVED', qr);

});

client.on('authenticated', (session) => {
    console.log('AUTHENTICATED', session);

});

client.on('auth_failure', msg => {
    console.error('AUTHENTICATION FAILURE', msg);


})

client.on('ready', () => {
    console.log('READY');




    setTimeout(() => {
        console.log("Send Message");

        var today = new Date();
        var time = today.getHours() + ":" + today.getMinutes() + ":" + today.getSeconds();
        client.sendMessageToID("6289506096398@c.us", `test ${time}`).then((r) => { //send to people who not already in chat or not listed on your contact
            console.log("sendMessageToID",r)
        })
        client.sendMessage("6289506096398@c.us", `test ${time}`).then((r) => {  
            console.log("sendMessage",r)
        })
        client.getBatteryLevel().then((r) => {
            console.log("getBatteryLevel", r)
        }) 
    }, 2000);




});

client.on('message', async msg => {
    console.log('MESSAGE RECEIVED', msg);

});

client.on('disconnected', () => {

    console.log('Client was logged out');
})

```

## Update
- 27/01/2020 (v0.1.12 > v0.1.13) add authTimeout option + change default authTimeout value from 5000ms to 10000ms , for detail check example.js
- 17/01/2020 (v0.1.11) fix selector qr/qrvalue/keep phoneimage update 

## Todo
- [x] add checkNumberStatus
- [x] SendMessageToID (send message to who not in contact list)
- [x] sendMessage and sendMessageToID Return Promise (Succes or not)
- [x] event on getBroadcast (this things is already embeded on event `On Message`")
- [x] getBatteryLevel (this things is already embeded on event `On Message`")
- [x] Implement all WAPI.js Function : Discontinue, just using client instance



## Legal
This code is in no way affiliated with, authorized, maintained, sponsored or endorsed by WhatsApp or any of its affiliates or subsidiaries. This is an independent and unofficial software. Use at your own risk. Commercial use of this code/repo is strictly prohibited.

## License
[APACHE v2](https://www.apache.org/licenses/LICENSE-2.0.txt)



made with 💗 