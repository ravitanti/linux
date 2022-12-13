<h1>CMPE 283 Assignments</h1>
<h3>By Ravi Kumar Tanti and Saurabh Ramesh Warathe</h3>

<h2>Assignment-03</h2>

<h3>Work done by Ravi (015267200):</h3>
I edited the cpuid.c code block for eax=0x4FFFFFFE to return the number of exits for a specific exit reason and return the value in eax register. I then ran the make command again to verify output through cpuid command in neested VM and dmesg command in the host VM.

<h3>Work done by Saurabh (015267226):</h3>
I edited the cpuid.c code block for eax=0x4FFFFFFF to return the time spent processing the exit number provided in ecx and return the high 32 bits in %ebx and low 32-bit in %ecx. I then commited this code change to the GitHub folder CMPE-283-Assignment-3

<h3>Steps followed:</h3>
    
1. Run the assignment-2 environment. <br>
    
2. Navigate to ~/linux/arch/x86/kvm/cpuid.c and edit the code block. Put another if..else condition for when eax = 0x4FFFFFFE. <br>
	  
	
		else if(eax == 0x4FFFFFFE)
        	{
		
			//reasons not in SDM
			if(ecx==35 || ecx==38 || ecx==42 || ecx==65 || ecx>68 || ecx<0){
				printk(KERN_INFO "exit reason number = %u not defined by SDM",ecx);
				eax=0;
				ebx=0;
				ecx=0;
				edx=0xFFFFFFFF;
			}
			else if( ecx==5 || ecx==6 || ecx==11 || ecx==17 ||  ecx==35 || ecx==38 || ecx==42 || ecx==66){
					printk(KERN_INFO"exit reason number =%u not enabled in KVM",ecx);
					eax=ebx=ecx=edx=0x00000000;
				}
			else{
					printk(KERN_INFO "CPUID(0x4FFFFFFE), exit number=%u exits=%d\n",ecx,exit_counter[(int)ecx]);
					eax=exit_counter[(int)ecx];
					ebx=ecx=edx=0;
				}
	  	}

3. Make the necessary changes in vmx.c as well (variable declarations)<br>
4. Make changes for code block and write if..else condition for when eax = 0x4FFFFFFF. <br>
	  
		else if(eax == 0x4FFFFFFF)
			{
			if(ecx==35 || ecx==38 || ecx==42 || ecx==65 || ecx>68 || ecx<0){
				printk(KERN_INFO "exit reason number = %u not defined by SDM",ecx);
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
	  
We noticed that the count increased in our case. Below are the screenshots for all exit reason. The highest exit count is currently 1024 for exit number 7. <br>
<img src="https://user-images.githubusercontent.com/70660489/207248188-4f2a64e7-ed3e-405b-ab9b-6179c57bc247.png"><br>

		  
We did another reboot to see the change in count of exits. The exit count increased as well.<br>
		  
                           
<h4>Question-4</h4>
	  
The most frequent exits were noticed for exit reason =7.<br>
	  

There were many exit reasons with 0 exits (least frequent).<br>
	

<h4>Other Output Screenshots </h4>

<li> Output of cpuid command for ebx(high 32-bit) and ecx(low 32-bit) values when eax=0x4FFFFFFF. <br>
  


<li> dmesg output of test4 script for ebx(high 32-bit) and ecx(low 32-bit) values when eax=0x4FFFFFFF. Full dmesg logs is in the test4.txt file in CMPE-283-Assignment-3 folder.<br>
  

