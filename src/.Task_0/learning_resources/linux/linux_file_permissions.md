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
    <h1>Linux File Permissions</h1>
</center>

---

</br>

* Like most of the modern operating systems, Linux is a multi-user OS hence extra layer of security is added to prevent users to access each other confidential files.
 
* Linux divides authorization into two levels,

  * Ownership

  * Permission
  
* Each file and directory has three user based permission groups,

  1. `owner`

  2. `group`

  3. `all`

* Each file or directory has three basic permission types,

  1. `read`

  2. `write`

  3. `execute`

* Linux File Permissions is a vast topic but you need not have to master it to succeed in this eYRC Theme. The only thing you need to keep in mind that unlike Windows were programs with `.exe` extension can be executed, in UNIX/Linux, files with **execute** permission can only be executed/run by the user.  

* To make a file executable in Linux following command can be used,

  ```sh
  sudo chmod +x <file_name>
  ```

<br>

----------------

#### References

1. [Understanding Linux File Permissions](https://www.linux.com/training-tutorials/understanding-linux-file-permissions/)
2. [Unix / Linux - File Permission / Access Modes](https://www.tutorialspoint.com/unix/unix-file-permission.htm)

</br>

---