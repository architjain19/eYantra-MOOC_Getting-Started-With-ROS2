# Writing a Transform Listner (Python)

> **Goal: Learn how to use tf2 to get access to frame transformations.**

In previous tutorials we created a tf2 broadcaster node to publish an offset pose of a `base_link` to tf2 w.r.t. a child frame `obj_1`. This tutorial assumes you have gone through the [tf2 broadcaster tutorial (Python)](python_tf_broadcaster.md)

In this tutorial we’ll create a tf2 listener to start using tf2.

### Writing the listner node in python:

```sh
import rclpy
from rclpy.node import Node
from tf2_ros.buffer import Buffer
from tf2_ros import TransformException
from tf2_ros.transform_listener import TransformListener


class FrameListener(Node):

    def __init__(self):

        super().__init__('sample_tf2_frame_listener')                                                   # node initialisation
        self.tf_buffer = Buffer()                                                                       # initializing transform buffer object
        self.tf_listener = TransformListener(self.tf_buffer, self)                                      # initializing transform listner object
        self.timer = self.create_timer(1.0, self.on_timer)                                              # call 'on_timer' function every second

    def on_timer(self):

        from_frame_rel = 'obj_1'                                                                        # frame from which transfrom has been sent
        to_frame_rel = 'base_link'                                                                      # frame to which transfrom has been sent

        try:
            t = self.tf_buffer.lookup_transform( to_frame_rel, from_frame_rel, rclpy.time.Time())       # look up for the transformation between 'obj_1' and 'base_link' frames
            self.get_logger().info(f'Successfully received data!')
        except TransformException as e:
            self.get_logger().info(f'Could not transform {to_frame_rel} to {from_frame_rel}: {e}')
            return

        # Logging transform data...
        self.get_logger().info(f'Translation X:  {t.transform.translation.x}')
        self.get_logger().info(f'Translation Y:  {t.transform.translation.y}')
        self.get_logger().info(f'Translation Z:  {t.transform.translation.z}')
        self.get_logger().info(f'Rotation X:  {t.transform.rotation.x}')                                # NOTE: rotations are in quaternions
        self.get_logger().info(f'Rotation Y:  {t.transform.rotation.y}')
        self.get_logger().info(f'Rotation Z:  {t.transform.rotation.z}')
        self.get_logger().info(f'Rotation W:  {t.transform.rotation.w}')
        

def main():
    rclpy.init()
    node = FrameListener()
    try:
        rclpy.spin(node)
    except KeyboardInterrupt:
        pass

    rclpy.shutdown()
```

### Examine the code:
- Now, let’s take a look at the code that is relevant to get access to frame transformations. The `tf2_ros` package provides an implementation of a `TransformListener` to help make the task of receiving transforms easier.
    ```sh
    from tf2_ros.transform_listener import TransformListener
    ```

- Here, we create a `TransformListener` object. Once the listener is created, it starts receiving tf2 transformations over the wire, and buffers them for up to 10 seconds.
    ```sh
    self.tf_listener = TransformListener(self.tf_buffer, self)
    ```

- Finally, we query the listener for a specific transformation. We call lookup_transform method with following arguments:
    1. Target frame
    2. Source frame
    3. The time at which we want to transform

    Providing `rclpy.time.Time()` will just get us the latest available transform. All this is wrapped in a try-except block to handle possible exceptions.
    
    ```sh
    t = self.tf_buffer.lookup_transform(to_frame_rel, from_frame_rel, rclpy.time.Time())
    ```


</br>

---

### References:

> You can overview following example codes and documentation provided officially by ROS. It explains how to listen tf using tf2ros.
> - [Write a listner (Python)](https://docs.ros.org/en/humble/Tutorials/Intermediate/Tf2/Writing-A-Tf2-Listener-Py.html)
> - [Write a listner (C++)](https://docs.ros.org/en/humble/Tutorials/Intermediate/Tf2/Writing-A-Tf2-Listener-Cpp.html)
