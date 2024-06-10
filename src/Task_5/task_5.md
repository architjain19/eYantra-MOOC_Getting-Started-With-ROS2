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
    <h1>Welcome to Task 5</h1>
</center>

---

</br>

> *The aim of Task 5 is to get you glimps of mini theme implementation of eYRC Cosmo Logistics. Get hands on with remote hardware to work towards full theme implementation.*

---


### This task is combination of *two* parts:

### A) **Remote Hardware Task - eBot navigation and docking**
*Attach and detach two racks present in the arena*

### B) **Remote Hardware Task - Pick and Place single package**
*Pick and place the aruco box from three racks using remote hardware and camera*

<p></p>


## Formula:

The team's total score is calculated using the following formula

> **Total_marks** = (900-T) \* 0.4 + ACI \* 10 + ACP \* 50 + ACD \* 50 + ECN \* 50 + ECP \* 20 + ECD \* 50 - P \* 25 + B \* 300

The abbreviation details are as follows:

> **T: Total time** taken for the run. If it is found to be greater
> than 900 seconds or no valid run, then the marks for the time will
> be made zero.
>
> **Valid Run:** A run is considered valid if the team is able to
> place at least one box on the drop table.
>
> **ACI: Arm Correct Identification**, parameter is increased when the
> TF is correctly published pointing to the Aruco marker's centre
> position. The maximum value of this parameter is 3.
>
> **ACP: Arm Correct Position**, parameter increases when the package
> is picked up using the magnetic gripper on the arm. The maximum
> value of this parameter is 3.
>
> **ACD: Arm Correct Drop**, parameter increases when the package is
> dropped on the table kept behind the arm. The maximum value of
> this parameter is 3.
>
> **ECN: eBot Correct Navigation**, parameter increases when the eBot
> is within the desired perimeter of the rack. Repeated attempts to
> enter into the area of the same rack will not yield to any
> additional marks. The maximum value of this parameter is 2.
>
> **ECP: eBot Correct Pick**, parameter increases when the eBot has
> correctly docked and attached the rack with the eBot using magnet.
> The maximum value of this parameter is 2.
>
> **ECD: eBot Correct Drop**, parameter increases when the eBot has
> correctly dropped the rack in front of the arm. The maximum value
> of this parameter is 2.
>
> **P: Penalty**, parameter increases for any point given in the theme
> rules penalty section.
>
> **B: Bonus**, is a binary parameter. It will be considered as one,
> if the team completes the given task of navigation and placing specified boxes on
> the drop table without any penalty.

> **NOTE:** 
> - Detection and recognition of package boxes other than the
specified ones will yield no marks.
> - This score will be evaluated and assigned during slots. While, the marks will be converted to a mark out of 100 at the end of task 5 for final elimination. The grading will be relative therefore the highest scored team will be having 100 marks.

</br>

---
