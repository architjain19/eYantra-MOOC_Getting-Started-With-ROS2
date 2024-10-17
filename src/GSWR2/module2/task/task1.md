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
	<h1>Task 1</h1>
</center>

---

### *Task Statement:*

Create a ROS2 package named `ros2mooc` with the following components: 

1. **Package Structure**: Organize the package to include a `task1/` directory containing an `__init__.py` file and a new node script named `success_node.py`.
- The package structure should look like this:
```
ros2mooc/
├── src/
    ├── hello_world/
    └── task1/        
	    ├── task1/
        │   ├── __init__.py
        │   └── success_node.py
        ├── resource/
        ├── test/
        ├── package.xml
        ├── setup.cfg
        └── setup.py

```
2. **Node Functionality**: Implement the `success_node.py` script to print "Package created successfully" when executed.
3. **Package Configuration**: Ensure that the package includes necessary configuration files (`package.xml`, `setup.cfg`, and `setup.py`) to facilitate the building and running of the ROS2 node.

Expected Output:
```
[INFO] [success_node]: Package created successfully
```