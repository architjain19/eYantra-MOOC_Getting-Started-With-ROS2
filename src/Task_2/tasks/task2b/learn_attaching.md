# Attaching to the rack 
---

## Concept

Since our ebot is docked properly it should be close (**<0.3 m**) to the rack

In the actual hardware, we are going to use Eletromagnet mounted on the ebot to attach the rack.

Similarly, here we are using a Gazebo Plugin to attach the rack with the ebot in simulation.

>Remember to change this in Stage 2 (Hardware implementation)

---

## Steps 

1) To attach the link, **The ebot should be very close (<0.3m) from the rack it won't attach**
    ```
    ros2 service call /ATTACH_LINK linkattacher_msgs/srv/AttachLink "{model1_name: 'ebot', link1_name: 'ebot_base_link', model2_name: 'rack1', link2_name: 'link'}"
    ```

    here:
    ```
    "{
        model1_name: 'ebot',               >>Don't change this
        link1_name: 'ebot_base_link',      >>Don't change this
        model2_name: 'rack1',              >> Just change this with the rack model name
        link2_name: 'link'                 >>Don't change this
        
        }"
    ```

2) To detach the link 
    ```
    ros2 service call /DETACH_LINK linkattacher_msgs/srv/DetachLink "{model1_name: 'ebot', link1_name: 'ebot_base_link', model2_name: 'rack1', link2_name: 'link'}"
    ```

    here:
    ```
    "{
        model1_name: 'ebot',               >>Don't change this
        link1_name: 'ebot_base_link',      >>Don't change this
        model2_name: 'rack1',              >> Just change this with the rack model name
        link2_name: 'link'                 >>Don't change this
        
        }"
    ```
---


> You can create python client using (sample snippet, similarly do for `DetachLink`):
> ```python
> from linkattacher_msgs.srv import AttachLink
>
> link_attach_cli = self.create_client(AttachLink, '/ATTACH_LINK')
>
>  while not self.link_attach_cli.wait_for_service(timeout_sec=1.0):
>       self.get_logger().info('Link attacher service not available, waiting again...')
>
> req = AttachLink.Request()
> req.model1_name =  'ebot'     
> req.link1_name  = 'ebot_base_link'       
> req.model2_name =  <Specify the rack name>       
> req.link2_name  = 'link'  
>
> link_attach_cli.call_async(req)
>
> ```



---

### Here is the example video of attaching to a rack,

<iframe width="700" height="400"
    src="https://www.youtube.com/embed/REMsQhp56fs?si=2B8qLsg4bCtOeqzy">
</iframe> 