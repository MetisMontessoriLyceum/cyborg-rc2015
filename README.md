# TeamCyborg
###### robocup junior 2015

### how the robot follows the line

   as line sensors we use the [Light Sensor Array](http://www.mindsensors.com/index.php?module=pagemaster&PAGE_user_op=view_page&PAGE_id=168 "mindsensors.com") and a normal [Lego Light Sensor](http://shop.lego.com/en-NL/Light-Sensor-9844 "lego.com").

   first, the robot calculates the position of the line:
   ```c
int error = 350 - (sensor[0] + sensor[1]*100 + sensor[2]*200 ... ) / (sensor[0] + sensor[1] + sensor[2] ... );
   ```
   > **note:** that the values are reversed, so black is 100 and white is 0
   
   then, it does the `error * Kp` and runs the motors with that.

### gap vs line lost

   when the line is not directly under the line sensor array the error is -350,
   in this case, we look at what happend *before* the robot lost the line to
   determine if the line was lost or if ther is a gap
