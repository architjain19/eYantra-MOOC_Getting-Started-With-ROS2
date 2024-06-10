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
    <h1>Deadlines</h1>
</center>

<script>
// Define task deadlines and their corresponding element IDs
var taskDeadlines = [
  {
    name: "Task 0",
    deadline: new Date("18 Sep, 2023 23:59:59").getTime(),
    elementId: "task0",
  },
  {
    name: "Coding Contest",
    deadline: new Date("1 Oct, 2023 23:59:00").getTime(),
    elementId: "coding_contest",
  },
  {
    name: "Task 1A",
    deadline: new Date("16 Oct, 2023 23:59:00").getTime(),
    elementId: "task_1a",
  },
  {
    name: "Task 1B",
    deadline: new Date("16 Oct, 2023 23:59:00").getTime(),
    elementId: "task_1b",
  },
  {
    name: "Task 1C",
    deadline: new Date("16 Oct, 2023 23:59:00").getTime(),
    elementId: "task_1c",
  },
  {
    name: "Task 2A",
    deadline: new Date("10 Nov, 2023 23:59:00").getTime(),
    elementId: "task_2a",
  },
  {
    name: "Task 2B",
    deadline: new Date("10 Nov, 2023 23:59:00").getTime(),
    elementId: "task_2b",
  },
];

// Function to update the countdown for each task
function updateCountdown(task) {
  var x = setInterval(function() {
    var now = new Date().getTime();
    var distance = task.deadline - now;
    var days = Math.floor(distance / (1000 * 60 * 60 * 24));
    var hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
    var minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
    var seconds = Math.floor((distance % (1000 * 60)) / 1000);
    var countdownText = days + "d " + hours + "h " + minutes + "m " + seconds + "s ";
    
    document.getElementById(task.elementId).innerHTML = countdownText;
    
    if (distance < 0) {
      clearInterval(x);
      document.getElementById(task.elementId).innerHTML = "-";
    }
  }, 1000);
}

// Loop through the task deadlines and update countdowns for each task
taskDeadlines.forEach(function(task) {
  updateCountdown(task);
});
</script>


<br>

<table style="width:100%">

<tr style="background-color: var(--quote-bg);">
    <th>#</th>
    <th>Task</th>
    <th>Start Date</th>
    <th>End Date</th>
    <th>Duration</th>
    <th>Time Remaining</th>
</tr>


<tr>
  <td align="center">
    <p>1</p>
  </td>
  <td align="center">
    <p><a href="Task_0/task_0.md">Task 0</a></p>
  </td>
  <td align="center">
    <p>05 Sep 2023</p>
  </td>
  <td align="center">
    <p>18 Sep 2023</p>
  </td>
  <td align="center">
    <p>2 Weeks</p>
  </td>
  <td align="center">
    <p id="task0"></p>
  </td>
</tr>

<tr>
  <td align="center">
    <p>2</p>
  </td>
  <td align="center">
    <p><a href="./coding_contest.md">Coding Contest</a></p>
  </td>
  <td align="center">
    <p>05 Sep 2023</p>
  </td>
  <td align="center">
    <p>01 Oct 2023</p>
  </td>
  <td align="center">
    <p>~4 Weeks</p>
  </td>
  <td align="center">
    <p id="coding_contest"></p>
  </td>
</tr>

<tr>
  <td align="center">
    <p>3</p>
  </td>
  <td align="center">
    <p><a href="./Task_1/tasks/task1a/task1a.md">Task 1A</a></p>
  </td>
  <td align="center">
    <p>19 Sep 2023</p>
  </td>
  <td align="center">
    <p>16 Oct 2023</p>
  </td>
  <td align="center">
    <p>~4 Weeks</p>
  </td>
  <td align="center">
    <p id="task_1a"></p>
  </td>
</tr>

<tr>
  <td align="center">
    <p>4</p>
  </td>
  <td align="center">
    <p><a href="./Task_1/tasks/task1b/task1b.md">Task 1B</a></p>
  </td>
  <td align="center">
    <p>19 Sep 2023</p>
  </td>
  <td align="center">
    <p>16 Oct 2023</p>
  </td>
  <td align="center">
    <p>~4 Weeks</p>
  </td>
  <td align="center">
    <p id="task_1b"></p>
  </td>
</tr>

<tr>
  <td align="center">
    <p>5</p>
  </td>
  <td align="center">
    <p><a href="./Task_1/tasks/task1c/task1c.md">Task 1C</a></p>
  </td>
  <td align="center">
    <p>19 Sep 2023</p>
  </td>
  <td align="center">
    <p>16 Oct 2023</p>
  </td>
  <td align="center">
    <p>~4 Weeks</p>
  </td>
  <td align="center">
    <p id="task_1c"></p>
  </td>
</tr>

<tr>
  <td align="center">
    <p>6</p>
  </td>
  <td align="center">
    <p><a href="./Task_2/tasks/task2a/task2a.md">Task 2A</a></p>
  </td>
  <td align="center">
    <p>17 Oct 2023</p>
  </td>
  <td align="center">
    <p>10 Nov 2023</p>
  </td>
  <td align="center">
    <p>~4 Weeks</p>
  </td>
  <td align="center">
    <p id="task_2a"></p>
  </td>
</tr>

<tr>
  <td align="center">
    <p>7</p>
  </td>
  <td align="center">
    <p><a href="./Task_2/tasks/task2b/task2b.md">Task 2B</a></p>
  </td>
  <td align="center">
    <p>17 Oct 2023</p>
  </td>
  <td align="center">
    <p>10 Nov 2023</p>
  </td>
  <td align="center">
    <p>~4 Weeks</p>
  </td>
  <td align="center">
    <p id="task_2b"></p>
  </td>
</tr>

</table>