<h1>CMPE 283 Assignments 01</h1>
<h3>By Ravi Kumar Tanti and Saurabh Ramesh Warathe</h3>

<h2>Assignment-01</h2>

<h3>Work done by Ravi (015267200):</h3>
I worked with Saurabh for this assignment. On my machine, I retrieved the .c program which was updated by Saurabh and added definitions for the different capability info regions by referring the latest Intel SDM. I also added four remaining rdmsr VM features code. I then created an Ubuntu 22.04.1 VM on my laptop through VMWare Workstation 15. I installed required packages onto it but faced multiple issues on the VM while executing make command, Therefore to overcome we reinstalled the headers and make and rebooted which solved our problem. <br>

<h3>Work done by Saurabh (015267226):</h3>
Along with Ravi I started by downloading the Makefile and the .c file on the VM, and added structs and definitions looking up in SDM for different capability region, added remaining msrs for each capability and also report_capability. For testing the code, i performed "make" command, to make the module, and inserted the module using insmod (using .ko file created) in kernel, and tracking the "dmesg". Initially there was a permission error, which we resolved using "sudo dmesg" command. I then created the git repo for the assignment, and i along with Ravi started pushing our code to the repository.<br>

<h3>Steps followed:</h3>
1. Installed VMware Workstation 15.<br>
2. Installed Linux Ububtu 22.04.1 with nested capabilities and given RAM of 8GB, disk space of 120GB and 8 Cores of processor. <br>
3. Verified if nested virtulisation is installed properly by checking sys/module/intel_/nested. <br>
4. Retrieve the starter .c file and Mekefile from canvas. <br>
5. Add the remaining code sections to the file.(struct, definitions and vm features)<br>
6. Installed GCC. <br>
7. Add capabilities structs based on info from SDM and make calls to rdmsr and report_capibility in the .c file. <br>
8. In the directory of the .c file and make file call 'sudo make'<br>
9. Call 'sudo ismode ./cmpe283-1.ko'. <br>
10. Call sudo dmesg to see capabilities. <br>


<h4>Screenshot of Output-</h4><br>
      <br>
      <img src="https://user-images.githubusercontent.com/97319236/206943246-acc66283-9c6a-4511-bea4-9f4994448579.png"><br>

      <img src="![2](https://user-images.githubusercontent.com/97319236/206943304-2f2340ce-fa8a-4c6a-8e08-d2843f095951.png)"><br>

      <img src="![3](https://user-images.githubusercontent.com/97319236/206943325-6400ff79-052f-44ea-9b60-fc733c24a4e8.png)"><br>

      <img src="![4](https://user-images.githubusercontent.com/97319236/206943351-70cfe269-8dd5-4729-b10d-0cb68f3390ca.png)"><br>

      <img src="![5](https://user-images.githubusercontent.com/97319236/206943388-b0e3e074-4be7-4ec1-be25-85232463c9f5.png)"><br>
   
  
