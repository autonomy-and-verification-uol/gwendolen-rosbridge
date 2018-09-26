# gwendolen-rosbridge
Gwendolen environment that allows agents to publish/subscribe to ROS topics using rosbridge.

We are using the [java_rosbridge](https://github.com/h2r/java_rosbridge) library to connect to rosbridge using Java code.

To test:
1. Install [MCAPL](https://sourceforge.net/projects/mcapl/) using the Eclipse method, and make sure it is working
2. Copy `java_rosbridge_all.jar` to `lib/3rdparty folder` in MCAPL
3. Edit `.classpath` found in the root of MCAPL, and add the line `<classpathentry kind="lib" path="lib/3rdparty/java_rosbridge_all.jar"/>`
4. Copy the `src` folder to MCAPL root
5. Start ROS with rosbridge in a terminal using `roslaunch rosbridge_server rosbridge_websocket.launch`
6. Open another terminal and use the command `rostopic echo /java_to_ros` (this is where messages from Gwendolen will appear)
7. In Eclipse, go to `src/examples/gwendolen/ros`, right-click hello.ail, select run as > run configurations, type run-AIL in the search box (should be there if MCAPL was installed correctly), and click on run
⋅⋅⋅* You should see the messages from Gwendolen agents in the terminal from step 6
8. To test the subscriber, open another terminal and type `rostopic pub ros_to_java std_msgs/String "hello from ros"`
⋅⋅⋅* You should see "hello from ros" in the Eclipse terminal
