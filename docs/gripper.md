# Gripper

Run with:
```bash
node eg/gripper.js
```


```javascript
var five = require("johnny-five"),
  compulsive = require("compulsive"),
  wrist, gripper, motion, repeater;

(new five.Board()).on("ready", function() {

    // Create a new `gripper` hardware instance.
    // This example allows the gripper module to
    // create a completely default instance

    wrist = new five.Servo(9);
    gripper = new five.Gripper(10);


    function slice() {
      wrist.to(100);

      compulsive.wait(100, function() {
        wrist.to(120);
      });
    }

    function chop() {
      compulsive.loop(200, function(loop) {
        if (!repeater) {
          repeater = loop;
        }
        slice();
      });
    }

    // Inject the `gripper` hardware into
    // the Repl instance's context;
    // allows direct command line access
    this.repl.inject({
      w: wrist,
      g: gripper,
      chop: chop,
      slice: slice
    });


    motion = new five.IR.Motion(7);

    // gripper.open()
    //
    // gripper.close()
    //
    // gripper.set([0-10])
    //
    //
    // g.*() from REPL
    //
    //
    motion.on("motionstart", function(err, ts) {
      chop();
    });

    // "motionstart" events are fired following a "motionstart event
    // when no movement has occurred in X ms
    motion.on("motionend", function(err, ts) {
      if (repeater) {
        repeater.stop();
        repeater = null;
      }
    });



  });


```


## Breadboard/Illustration


![docs/breadboard/gripper.png](breadboard/gripper.png)

- [Parallax Boe-Bot Gripper](http://www.parallax.com/Portals/0/Downloads/docs/prod/acc/GripperManual-v3.0.pdf)
- [DFRobot LG-NS Gripper](http://www.dfrobot.com/index.php?route=product/product&filter_name=gripper&product_id=628#.UCvGymNST_k)



## License
Copyright (c) 2012, 2013, 2014 Rick Waldron <waldron.rick@gmail.com>
Licensed under the MIT license.
Copyright (c) 2014, 2015 The Johnny-Five Contributors
Licensed under the MIT license.
