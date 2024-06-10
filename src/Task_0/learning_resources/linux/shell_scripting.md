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
    <h1>Shell Scripting</h1>
</center>

---

</br>

* You have learned in the previous section that UNIX shells can take commands from a file also. Such files are called **shell scripts**.

  

* In this section we will explore how to write your own shell scripts. We will discuss only those things which will be required to successfully complete upcoming eYRC Tasks. 



## Shebang (UNIX)

* In UNIX, shebang is a line which is added at the beginning of any script that you want to run as a standalone executable.

* The line should starts with `#!`.

* A shebang tells the shell which interpreter to use and its location in order to execute the script. For example,

  * If I write a script for Bash Shell then I would have to include the following at the beginning of the script.

    ```sh
    #!/bin/bash
    ```

  * If I write a script for Python then I would have to include the following at the beginning of the script.

    ```sh
    #!/usr/bin/env python3
    ```

* A shebang gives the script the ability to be executed as an executable.

</br>

---