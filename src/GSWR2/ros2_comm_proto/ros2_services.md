<!-- <center><img src="http://mooc.e-yantra.org/img/eYantra_logo.svg" alt="e-yantra_logo" style="scale:75%;" /></center> -->

<style>
.back{
	position: fixed;
	width: 250px;
	height: 250px;
	top: 50%;
	left: 50%;
    margin-top: auto; 
    margin-left: auto; 
	opacity: 0.15;
    z-index: -1;
	}
</style>
<!-- <img src="http://mooc.e-yantra.org/img/EyantraLogoMini.png" class="back"> -->

<center>
    <h1>Understanding ROS2 Services</h1>
</center>

---

### Concept and Functionality

#### What are ROS2 Services?

> ROS2 (Robot Operating System 2) is an open-source framework for building robotic applications. Within this framework, services provide a means of communication between nodes that allows for request-response interactions. Unlike topics, which are used for streaming data, services are designed for discrete transactions.
>
> A ROS2 service consists of two parts:
> - **Service Server**: This node offers a service.
> - **Service Client**: This node calls the service and waits for a response.
> 
> Services are synchronous by nature. When a client sends a request, it waits for the server to process the request and send back a response before continuing.

#### How do they differ from Topics?

> - **Nature of Communication**:
>   - **Topics**: Used for continuous data streams, supporting many-to-many communication. Nodes can publish to or subscribe from a topic independently.
>   - **Services**: Used for request-response interactions, supporting one-to-one communication. A client sends a request to a server, which processes it and returns a response.
> 
> - **Use Cases**:
>   - **Topics**: Suitable for sensor data streaming, telemetry, and other continuous data flows.
>   - **Services**: Suitable for commands, configuration changes, or any operation that requires a response after processing.
> 
> - **Behavior**:
>   - **Topics**: Asynchronous communication where publishers and subscribers do not wait for each other.
>   - **Services**: Synchronous communication where the client waits for the server’s response.

### Practical Example

#### Implementing a Service Server and Client

> Let’s implement a simple example where a service server will add two integers sent by a client and return the result.

##### Service Definition

> First, define a service in an IDL (Interface Definition Language) file. Create a file named `AddTwoInts.srv`:

```plaintext
int64 a
int64 b
---
int64 sum
```

##### Implementing the Service Server

> Create a Python script for the service server.

```python
# add_two_ints_server.py

import rclpy
from rclpy.node import Node
from example_interfaces.srv import AddTwoInts

class AddTwoIntsServer(Node):
    def __init__(self):
        super().__init__('add_two_ints_server')
        self.srv = self.create_service(AddTwoInts, 'add_two_ints', self.add_two_ints_callback)
    
    def add_two_ints_callback(self, request, response):
        response.sum = request.a + request.b
        self.get_logger().info(f'Incoming request\na: {request.a} b: {request.b}')
        self.get_logger().info(f'Sending back response: {response.sum}')
        return response

def main(args=None):
    rclpy.init(args=args)
    node = AddTwoIntsServer()
    rclpy.spin(node)
    rclpy.shutdown()

if __name__ == '__main__':
    main()
```

##### Implementing the Service Client

> Create a Python script for the service client.

```python
# add_two_ints_client.py

import sys
import rclpy
from rclpy.node import Node
from example_interfaces.srv import AddTwoInts

class AddTwoIntsClient(Node):
    def __init__(self):
        super().__init__('add_two_ints_client')
        self.cli = self.create_client(AddTwoInts, 'add_two_ints')
        while not self.cli.wait_for_service(timeout_sec=1.0):
            self.get_logger().info('service not available, waiting again...')
        self.req = AddTwoInts.Request()

    def send_request(self):
        self.req.a = int(sys.argv[1])
        self.req.b = int(sys.argv[2])
        self.future = self.cli.call_async(self.req)

def main(args=None):
    rclpy.init(args=args)
    client = AddTwoIntsClient()
    client.send_request()

    while rclpy.ok():
        rclpy.spin_once(client)
        if client.future.done():
            try:
                response = client.future.result()
            except Exception as e:
                client.get_logger().info('Service call failed %r' % (e,))
            else:
                client.get_logger().info(f'Result: {response.sum}')
            break

    client.destroy_node()
    rclpy.shutdown()

if __name__ == '__main__':
    main()
```

> To run these scripts, save them in your workspace, and then execute the following commands in separate terminals:

```sh
# Terminal 1: Run the server
ros2 run your_package_name add_two_ints_server

# Terminal 2: Run the client with arguments
ros2 run your_package_name add_two_ints_client 3 5
```

### ROS CLI Commands

> ROS2 provides a rich set of command-line tools to interact with services. Here are some common commands to list, call, and find services.

#### Listing Services

> To list all available services, use the following command:
> 
> ```sh
> ros2 service list
> ```

#### Calling a Service

> To call a service and pass parameters, use the following command:
> 
> ```sh
> ros2 service call /add_two_ints example_interfaces/srv/AddTwoInts "{a: 3, b: 5}"
> ```

#### Finding Service Types

> To find the type of a specific service, use:
> 
> ```sh
> ros2 service type /add_two_ints
> ```

#### Describing a Service

> To get details about a service type, including the request and response fields, use:
> 
> ```sh
> ros2 interface show example_interfaces/srv/AddTwoInts
> ```

### Conclusion

> *ROS2 services provide a structured way to implement request-response communication between nodes, complementing the asynchronous data flow provided by topics. By understanding the differences between services and topics, and leveraging the provided ROS2 CLI commands, developers can effectively build and debug ROS2 applications. The example provided demonstrates the basic implementation of a service server and client, serving as a foundation for more complex service interactions in your robotics projects.*

-------