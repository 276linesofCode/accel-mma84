#Accelerometer
Driver for the accel-mma84 Tessel accelerometer module ([MMA8452Q](http://www.freescale.com/files/sensors/doc/data_sheet/MMA8452Q.pdf)).

##Installation
```sh
npm install accel-mma84
```

##Example
```js
/*********************************************
This basic accelerometer example logs a stream
of x, y, and z data from the accelerometer
*********************************************/

var tessel = require('tessel');
var accel = require('accel-mma84').use(tessel.port("A"));

// Initialize the accelerometer.
accel.on('ready', function () {
	// Stream accelerometer data
  accel.on('data', function (xyz) {
    console.log("x:", xyz[0].toFixed(2),
      "y:", xyz[1].toFixed(2),
      "z:", xyz[2].toFixed(2));
  });
});

accel.on('error', function(err) {
  console.log('error connecting', err);
});

setInterval(function(){}, 20000);
```

##Methods

*  **`accel`.getAcceleration(callback(err, xyz))** Gets the acceleration from the device, outputs as array [x, y, z].

*  **`accel`.setOutputRate(rateInHz, callback(err))** Sets the output rate of the data (1.56-800 Hz).

*  **`accel`.availableOutputRates()** Logs the available interrupt rates in Hz.

*  **`accel`.setScaleRange(scaleRange, callback(err))** Sets the accelerometer to read up to 2, 4, or 8 Gs of acceleration (smaller range = better precision).

*  **`accel`.availableScaleRanges()** Logs the available accelerometer ranges (in units of Gs).

*  **`accel`.enableDataInterrupts(trueOrFalse, callback(err))** Enables or disables data interrupts. Set the first param truthy to enable, false to disable.

##Events

* *ready*

* *error*

* *data*

##Further Examples

* [Average (more advanced use)](https://github.com/tessel/modules/blob/master/accel-mma84/examples/average.js)

## License

MIT
