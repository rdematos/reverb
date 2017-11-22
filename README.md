Reverb
======


## What?

Reverb is library for getting the utterance history text output from the Alexa companion app.

### Usage


For now, Reverb requires you to get extract some data by hand.
These are the "Cookie" header and the device serial number. These
can both be easily acquired using the Developer Tools that come
with Chrome. Simply open [the Alexa companion web app](http://alexa.amazon.com)
and open the Network tab of the developer tools. Click on the
Filter icon (it looks a bit like a funnel) and filter down to
"WebSockets." Then, refresh the page.

There should be a single entry in the list pointing to
`dp-gw-na-js.amazon.com`. Select that and go to the "Headers" tab.
The serial number you want will be the `x-amz-device-serial`
parameter under "Query String Parameters," and the "Cookie"
is the (potentially huge) string next to `Cookie:` under
"Request Headers."

Now that you have those, it's simple to get access to the
Echo's transcriptions of your requests:

```javascript
var Reverb = require('reverb');
new Reverb({
    cookie: // The Cookie retrieved above
  , serial: // The serial retrieved above
}).on('ready', function() {
    // this is emitted when the connection is
    //  established and the hands have been shaked
    console.log("Ready!");
}).on('activity', function(activity) {
    // parse the transcription and do something
    //  with it here
    console.log("You said:", activity.summary);
});
```
