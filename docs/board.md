# Board

Run with:
```bash
node eg/board.js
```


```javascript
var five = require("johnny-five");

// The board's pins will not be accessible until
// the board has reported that it is ready
five.Board().on("ready", function() {
  var val = 0;

  // Set pin 13 to OUTPUT mode
  this.pinMode(13, 1);

  // Create a loop to "flash/blink/strobe" an led
  this.loop(100, function() {
    this.digitalWrite(13, (val = val ? 0 : 1));
  });
});


// Schematic
// http://arduino.cc/en/uploads/Tutorial/ExampleCircuit_bb.png

```


## Breadboard/Illustration


![docs/breadboard/board.png](breadboard/board.png)





## License
Copyright (c) 2012, 2013, 2014 Rick Waldron <waldron.rick@gmail.com>
Licensed under the MIT license.
Copyright (c) 2014, 2015 The Johnny-Five Contributors
Licensed under the MIT license.
