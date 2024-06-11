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
    <h1>Linux File Commands</h1>
</center>

---

</br>

## The Linux Terminal

* In UNIX, terminal is a text interface to interact with the OS. There are list of commands which user can use to interact with the OS.

  

* Terminal is also called shell or console.

  

* Command Prompt and Powershell are two such kind of interface provided by Windows OS.

  

* In Ubuntu and most of the UNIX based OS a particular type of shell called **Bash** which is one kind of UNIX shell, is launched when you open any Terminal program. **Zsh** is another such popular shell for UNIX.

  

* These UNIX shell like Bash and Zsh are command processors which takes commands from user, interprets it and executes the commands with the help of the underlying OS.

  

* UNIX shells can also read commands from a file. Such kind of files are called **Shell Scripts**. In the next section we will explore this.

  

* One such shell script is **.bashrc** which resides in `/home/` directory. This shell script runs everytime you open an instance of Bash shell.

  

* In **Ubuntu** you can press `Ctrl + Alt + T` to open up an instance of the terminal.



## Common Linux Commands

### sudo

* In UNIX a **superuser** or **root** is a user which has unrestricted access to all the commands, files, folders and resources of the system.

  

* If you want to run any command as a superuser you need to prefix that command with `sudo`.

  

* eg: `sudo chmod +x hello.sh`



### ls

| Command  | Function                                                     |
| -------- | ------------------------------------------------------------ |
| `ls`     | List the files and folders in the current directory          |
| `ls -l`  | `-l` flag is used with `ls` to list files and folders in the current directory with their permissions. |
| `ls -la` | `-la` flag is used to list all the files and folders including hidden ones with their permissions. |



### mkdir

| Usage                   | Result                                                       |
| ----------------------- | ------------------------------------------------------------ |
| `mkdir folder1 folder2` | This command will create two folders, folder1 and folder2 in current directory. |



### cd

| Usage            | Result                                                       |
| ---------------- | ------------------------------------------------------------ |
| `cd ~`           | This will take to to `/home/` directory. In UNIX, tilde `~`  is used to represent home directory. |
| `cd ~/colcon_ws` | This will take you inside a folder named colcon_ws in home directory |



### echo

| Usage                       | Result                                                       |
| --------------------------- | ------------------------------------------------------------ |
| `echo "hello"`              | This will print the string `hello` in the terminal.          |
| `echo "hello" >> file.txt ` | This will append the string `hello` at the end of `file.txt`. This won't overwrite anything. |
| `echo "hello" > file.txt `  | This will append the string `hello` at the beginning of `file.txt`. This will overwrite. |



### find

| Command                                  | Function                                                     |
| ---------------------------------------- | ------------------------------------------------------------ |
| `find . -type d -name "dir_name_start*"` | List the files and folders in the current directory starting with "dir_name_start". |
| `find . -type f -name "file_name.*"`     | Search for files starting with "file_name" with unknown extension. |



### grep

* Search for *"text"* string inside any type of file.

  ```sh
  grep -rnw "text"
  ```

  

* Highlight & Show only the pre-defined text in the output of a command

  ```sh
  colcon build | grep "pkg_my_ros"
  ```



### which

* This command is used to find the location of an executable available to shell.

  ```sh
  which python
  
  # Output
  /usr/bin/python
  ```

  

### pwd

* This will print out the path of current directory you are in.

  ```sh
  pwd
  ```

  

### cat

* This will print the content of `file.txt` with line numbers, in the terminal.

  ```sh
  cat -n file.txt
  ```

  

### man

* This is very useful command in UNIX. If you are not sure how to use any command just call `man`.

* `man` stands for manual.

  ```sh
  man which
  
  man cat
  
  man find
  
  man grep
  
  man man
  ```

</br>

---