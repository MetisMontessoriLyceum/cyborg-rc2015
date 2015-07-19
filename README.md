# TeamCyborg
###### robocup junior 2015

## how the robot follows the line

   As line sensors we use the [Light Sensor Array](http://www.mindsensors.com/index.php?module=pagemaster&PAGE_user_op=view_page&PAGE_id=168 "mindsensors.com") and a normal [Lego Light Sensor](http://shop.lego.com/en-NL/Light-Sensor-9844 "lego.com").

   First, the robot calculates the position of the line:
   ```c
int error = 350 - (sensor[0] + sensor[1]*100 + sensor[2]*200 ... ) / (sensor[0] + sensor[1] + sensor[2] ... );
   ```
   > **note:** that the values are reversed, so black is 100 and white is 0
   
   Then, it does the `error * Kp` and runs the motors with that.

## gap vs line lost

   When the line is not directly under the line sensor array the error is -350,
   in this case, we look at what happend *before* the robot lost the line to
   determine if the line was lost or if ther is a gap.

## calibration

   For calibration we use the following formula I came up with:
   ```c
sensor = (sensor - cali.light) * (100 / (cali.dark - cali.light));
   ```
   Then, you simply remove the values above 100 and below 0:
   ```c
if (sensor > 100) {
	sensor = 100;
}
else if (sensor < 0) {
	sensor = 0;
}
   ```
   > **note:** make sure you use a `float` as datatype of the sensor

## obstacle

   Ones we detect an obstacle we compare what the robot sees left with what the robot sees right.
   Then we turn to the side that is the furtest away.

   ```c
for (int i; i<2; i++) {
   ```
      Now we simply go forward until the robot drived past the obstacle (we detect this with the lego ultra sonic sensor),
      and turn 90 degrees.
   ```c
}
   ```

   All we need to do now is move forward tilt we see a line and then turn to the same direction as the oritional turn.

## ramp

We do the detection of the ramp width a Accelerometer, compass & gyrosensor in one form www.mindsensors.com

## calibration

   The built in calibration rutene wasn't quick anof, so we made une ourer self,
   It is very simple:

   Since we are never ask to start the robot on the hill we can salfy asume that the floor is flat where we start.
   So when the program starts we see what the start tilt X and Y are, and safe it to a public `int`.
