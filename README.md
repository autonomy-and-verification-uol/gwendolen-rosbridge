# gwendolen-rosbridge
Gwendolen environment that allows agents to publish/subscribe to ROS topics using rosbridge.

We are using the [java_rosbridge](https://github.com/h2r/java_rosbridge) library to connect to rosbridge using Java code.

To test:
1. Install [MCAPL](https://sourceforge.net/projects/mcapl/) using the Eclipse method, and make sure it is working
2. Install ROS, any version, and make sure it is working
3. Install [Rosbridge](http://wiki.ros.org/rosbridge_suite/Tutorials/RunningRosbridge) for the ROS version that you installed (and make sure it is working!)
4. Copy `java_rosbridge_all.jar` to `lib/3rdparty folder` in MCAPL
5. Edit `.classpath` found in the root of MCAPL, and add the line `<classpathentry kind="lib" path="lib/3rdparty/java_rosbridge_all.jar"/>`
6. Copy the `src/examples/gwendolen/ros` folder to MCAPL root
7. Start ROS with rosbridge in a terminal using `roslaunch rosbridge_server rosbridge_websocket.launch`
8. Open another terminal and use the command `rostopic echo /java_to_ros` (this is where messages from Gwendolen will appear)
9. In Eclipse, go to `src/examples/gwendolen/ros`, right-click hello.ail, select run as > run configurations, type run-AIL in the search box (should be there if MCAPL was installed correctly), and click on run
   * You should see the messages from Gwendolen agents in the terminal from step 6
10. To test the subscriber, open another terminal and type `rostopic pub ros_to_java std_msgs/String "hello from ros"`
   * You should see "hello from ros" in the Eclipse terminal

If you require extra message types, clone the code from [java_rosbridge](https://github.com/h2r/java_rosbridge), add the messages you require (`src/ros/msgs`), run `mvn package` and copy the newly generated jar `target/java_rosbridge-2.0.2-jar-with-dependencies.jar` to `lib/3rdparty folder` in MCAPL, rename it to `java_rosbridge_all.jar` and overwrite it.

## Message types available in the current jar:
- actionlib_msgs: GoalId (Time stamp, String id)
- geometry_msgs: Twist (Vector3 linear, Vector3 angular)
- geometry_msgs: Vector3 (double x, double y, double z)
- move_base_msgs: MoveBaseActionResult (Header header, Status status, Result result)
- move_base_msgs: Result ()
- move_base_msgs: Status (GoalId goal_id, String status, String text)
- sensor_msgs: Image(Header header, int height, int width, String encoding, int is_bigendian, int step, byte[] data) 
- std_msgs: Header(int seq, Time stamp, String frame_id)
- std_msgs: PrimitiveMsg(data)
- std_msgs: Time(int secs, int nsecs)
