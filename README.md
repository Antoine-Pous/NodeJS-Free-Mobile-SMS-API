Free Mobile SMS API
============
This package allow you to send SMS to your Free Mobile phone for monitoring.

## Requirements

1. You need an activated Free Mobile phone number
2. The option "Notifications par SMS" must be activated on the [account settings page](https://mobile.free.fr/moncompte/index.php?page=options)

## Dependencies
- [ssl-root-cas] (https://www.npmjs.org/package/ssl-root-cas)

**Currently the Free's server haven't public key on his certificate, so the SSL certificate couldn't be validated and trusted! I have reported this issue the Oct 7th 2014 to their staff. ssl-root-cas is implemented and functional for the day when they will deploy a patch for this vulnerability. Meanwhile the `rejectUnauthorized` option should remain disabled for the module to work properly :(**

## License
This node module is licensed under [GNU LGPL v3] (http://www.gnu.org/licenses/lgpl.txt).


## Installation
```
npm install free-mobile-sms-api
```

## Usage

Send SMS:
```javascript
var sms = require('free-mobile-sms-api');

sms.account(12345678,'myPrivateKey');
sms.send("Hello world!");
```

All errors/success can be handled with event listener:
```javascript
sms.on('sms:error', function(e) {
  console.log(e.code + ": " + e.msg);
});

sms.on('sms:success', function(data) {
  console.log("Success! :D");
});
```

## Codes:
- 200 Success
- 400 One of needed parameters is missed or incorrect
- 402 Too many requests sent, please wait few time
- 403 Access denied, check your credentials
- 500 SMS API got an internal error, try again later
