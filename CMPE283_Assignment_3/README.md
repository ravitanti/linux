<h1>CMPE 283 Assignments</h1>
<h3>By Ravi Kumar Tanti and Saurabh Ramesh Warathe</h3>

<h2>Assignment-03</h2>

<h3>Work done by Ravi (015267200):</h3>

<h3>Work done by Saurabh (015267226):</h3>


<h3>Steps followed:</h3>
    
1. Run the assignment-2 environment. <br>
    
2. Navigate to ~/linux/arch/x86/kvm/cpuid.c and edit the code block. Put another if..else condition for when eax = 0x4FFFFFFE. <br>
	  
	  else if(eax == 0x4FFFFFFE)
        {

		//reasons not in SDM
		if(ecx==35 || ecx==38 || ecx==42 || ecx<0){
			printk(KERN_INFO "exit reason number = %u not defined by SDM",ecx);
			eax=0;
			ebx=0;
			ecx=0;
			edx=0xFFFFFFFF;
		}
		else if( ecx==5 || ecx==6 || ecx==11 || ecx==17 ||  ecx==35 || ecx==38 || ecx==42 || ecx==66){
				printk(KERN_INFO"CPUID(0x4FFFFFFE), exit reason number =%u not enabled in KVM",ecx);
				eax=ebx=ecx=edx=0;
			}
		else{
				printk(KERN_INFO "CPUID(0x4FFFFFFE), exit number=%u exits=%d\n",ecx,arch_atomic_read(&exit_Reason[ecx]));
				eax=atomic_read(&exit_Reason[(int)ecx]);
				ebx=ecx=edx=0;
			}
		}

3. Make the necessary changes in vmx.c as well (variable declarations)<br>
4. Make changes for code block and write if..else condition for when eax = 0x4FFFFFFF. <br>
	  
  else if(eax == 0x4FFFFFFF)
	{
		if(ecx==35 || ecx==38 || ecx==42 || ecx<0){
          printk(KERN_INFO "CPUID(0x4FFFFFFF), exit reason number = %u not defined by SDM",ecx);
          eax=0;
          ebx=0;
          ecx=0;
          edx=0xFFFFFFFF;
     }
     else if( ecx==5 || ecx==6 || ecx==11 || ecx==17 ||  ecx==35 || ecx==38 || ecx==42 || ecx==66){
          printk(KERN_INFO"exit reason number =%u not enabled in KVM",ecx);
          eax=ebx=ecx=edx=0;
		}

		else{
          printk(KERN_INFO "CPUID(0x4FFFFFFF), exits number=%u",ecx);
          ebx = (atomic64_read(&time_taken) >>32);
          printk(KERN_INFO "Higher 32-bits-EBX %u",ebx);
          ecx = (atomic64_read (&time_taken));
          printk(KERN_INFO "Lower 32-bits-ECX %u",ecx);
          edx = 0;
		}
	}	
     
                                                                     
5. Save the changes and run the below commands in order as mentioned.<br>
    ``` sudo make -j 16 modules ``` <br>
    ``` sudo make -j 16 ```                                                             
    ``` sudo make INSTALL_MOD_STRIP=1 modules_install ```                                                          
    ``` rmmod kvm_intel ```<br>
    ``` rmmod kvm ```<br>
    ``` modprobe kvm_intel ``` <br>
    ``` modprobe kvm ``` <br>
                                                                     
6. Now run the nested VM and run test script or ``` cpuid -l 0x0x4FFFFFFE -s <exit reason> ``` to verify output for different exit reasons.<br>   
    
7. Run dmesg in the host VM to get output. <br>  
	 
<h3>Answer to Questions:</h3>
	  <h4>Question-3</h4>
	  
We noticed that the count increased at a stable rate. Below are the screenshots for exit reason=0. The exit count is currently *******. <br>
	  
		  
We did another reboot to see the increase in count of exits. The exit count raised to 24070 which is exactly the double of what it was previously. <br>
		  

	  
We did one more reboot to find tha rate of increase. The number of exits is now ******** . Which is three times of the first output. Which conculdes that the number of exits is increasing at a stable rate.<br>


For exit reason=0, the number of exits increase by approximately ** on each boot.<br>	  
                           
<h4>Question-4</h4>
	  
The most frequent exits were noticed for exit reason =***.<br>
	  

There were many exit reasons with 0 exits (least frequent). The full dmesg output is in the test3.txt /CMPE-283-Assignment-3 folder.	  <br>
	

<h4>Other Output Screenshots </h4>

<li> Output of cpuid command for ebx(high 32-bit) and ecx(low 32-bit) values when eax=0x4ffffffc. <br>
  


<li> dmesg output of test4 script for ebx(high 32-bit) and ecx(low 32-bit) values when eax=0x4FFFFFFF. Full dmesg logs is in the test4.txt file in CMPE-283-Assignment-3 folder.<br>
  


<h1>Assignment-04</h1>

<h3>Work done by Kajal (015210884):</h3>
We started working on GCP instance on which Assignment 3 was finished. I worked on performance when using shadow paging to illustrate the different exit frequencies and types. I removed the kvm-intel module and reloaded with parameter ept=0 and recorded the total exit count information in shadow.txt file.(https://github.com/kajaldhanotia/linux/blob/master/CMPE-283-Assignment-4/shadow.txt)
    
<h3>Work done by Sumeet (015252003):</h3>
We started working on GCP instance on which Assignment 3 was finished. I worked on performance when using nested paging to illustrate the different exit frequencies and types. I recorded the total exit count information in nested.txt file.(https://github.com/kajaldhanotia/linux/blob/master/CMPE-283-Assignment-4/nested.txt)
	
<h3>Question 2: Include a sample of your print of exit count output from dmesg from “with ept” and “without ept”.</h3>

<h4> Output when EPT=0 (Shadow Paging)</h4>


	
See full output here: 
	
<h4> Output when EPT = non zero (Nested Paging)</h4>
	



See full output here: 

  
  
