# Writing a Broadcaster (Python)

> You can refer this tutorial as reference for [Introduction to Tf2](https://docs.ros.org/en/humble/Tutorials/Intermediate/Tf2/Introduction-To-Tf2.html) which might help you understand basics of transforms. *(It's official documentation from ROS)*


### Writing the broadcaster node in python:

```sh
import rclpy
from rclpy.node import Node
from tf2_ros import TransformBroadcaster
from geometry_msgs.msg import TransformStamped

class FixedFrameBroadcaster(Node):

    def __init__(self):

        super().__init__('sample_tf2_broadcaster')                              # node initialisation
        self.tf_broadcaster = TransformBroadcaster(self)                        # initializing transform broadcaster object
        self.timer = self.create_timer(0.1, self.broadcast_timer_callback)      # timer based function which iterates on defined time interval

    def broadcast_timer_callback(self):

        t = TransformStamped()
        t.header.stamp = self.get_clock().now().to_msg()                        # select transform time stamp as current clock time
        # frame IDs
        t.header.frame_id = 'base_link'                                         # parent frame link with whom to send transform
        t.child_frame_id = 'obj_1'                                              # child frame link from where to send transfrom
        # translation
        t.transform.translation.x = 0.0
        t.transform.translation.y = 2.0                                         # distance offset in Y axis of 2 units
        t.transform.translation.z = 0.0
        # rotation
        t.transform.rotation.x = 0.0
        t.transform.rotation.y = 0.0
        t.transform.rotation.z = 0.0
        t.transform.rotation.w = 1.0                                            # rotation 0 degrees

        self.tf_broadcaster.sendTransform(t)                                    # publish transform as defined in 't'


def main():
    rclpy.init()
    node = FixedFrameBroadcaster()
    try:
        rclpy.spin(node)
    except KeyboardInterrupt:
        pass

    rclpy.shutdown()
```

### Examine the code:

- Here we create a new transform, from the parent `base_link` to the new child `obj_1`. The `obj_1` frame is 2 meters offset in y axis in terms of the `base_link` frame.

    ```sh
    t = TransformStamped()

    t.header.stamp = self.get_clock().now().to_msg()
    t.header.frame_id = 'base_link'
    t.child_frame_id = 'obj_1'
    t.transform.translation.x = 0.0
    t.transform.translation.y = 2.0
    t.transform.translation.z = 0.0
    ```

- The orientation for the new child frame is at 0 degrees as we haven't changed the rotation part of code and kept it as-

    ```sh
    t.transform.rotation.x = 0.0
    t.transform.rotation.y = 0.0
    t.transform.rotation.z = 0.0
    t.transform.rotation.w = 1.0
    ```

- Finally broadcasting TF using `sendTransform()` method-

    ```sh
    self.tf_broadcaster.sendTransform(t)    # where t is defined above
    ```

</br>

---

### References:

> You can overview following example codes and documentation provided officially by ROS. It explains how to broadcast tf using various methods.
> - [Write a broadcaster (Python)](https://docs.ros.org/en/humble/Tutorials/Intermediate/Tf2/Writing-A-Tf2-Broadcaster-Py.html)
> - [Adding a frame (Python)](https://docs.ros.org/en/humble/Tutorials/Intermediate/Tf2/Adding-A-Frame-Py.html)
> - [Introduction to Tf](https://docs.ros.org/en/humble/Tutorials/Intermediate/Tf2/Introduction-To-Tf2.html)

> There are some other examples for C++ and static transfroms too.
> - [Writing a tf2 static broadcaster (Python)](https://docs.ros.org/en/humble/Tutorials/Intermediate/Tf2/Writing-A-Tf2-Static-Broadcaster-Py.html)
> - [Write a broadcaster (C++)](https://docs.ros.org/en/humble/Tutorials/Intermediate/Tf2/Writing-A-Tf2-Broadcaster-Cpp.html)
> - [Adding a frame (C++)](https://docs.ros.org/en/humble/Tutorials/Intermediate/Tf2/Adding-A-Frame-Cpp.html)
