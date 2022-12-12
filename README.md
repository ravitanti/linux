<h1>CMPE 283 Virtulization</h1>
<h3>By Ravi Kumar Tanti and Saurabh Ramesh Warathe</h3>

<h3>Steps followed:</h3>
1. Installed VMware Workstation 15.<br>
2. Installed Linux Ububtu 22.04.1 with nested capabilities and given RAM of 8GB, disk space of 120GB and 8 Cores of processor.<br>
3. Verified if nested virtulisation is installed properly by checking sys/module/intel_/nested.<br>
4. Retrieve the starter .c file and Mekefile from canvas.<br>
5. Add the remaining code sections to the file.(struct, definitions and vm features)<br>
6. Installed GCC.<br>
7. Add capabilities structs based on info from SDM and make calls to rdmsr and report_capibility in the .c file.<br>
8. In the directory of the .c file and make file call 'sudo make'<br>
9. Call 'sudo ismode ./cmpe283-1.ko'.<br>
10. Call sudo dmesg to see capabilities.<br>
11. Made Clone of linux source code and cloned it on local system. <br>
12. Update the files ```arch/x86/kvm/vmx/vmx.c``` and ```arch/x86/kvm/cpuid.c``` <br>
13. Install all the dependencies required for build. <br>
14. Rebuild the kernel using ```make modules``` command and ```make INSTALL_MOD_STRIP=1 modules_install && make install```. <br>
15. Run ```lsmod | grep kvm``` to check if the kvm modules are preloaded. <br>
16. If they are already present remove them using ```rmmod kvm``` and ```rmmod kvm_intel``` commands. <br>
17. Run ```modprobe kvm``` and ```modprobe kvm_intel``` commands to reload edited kvm modules. <br>
18. Run the commands listed below from the host terminal in order to enable the kvm module in the host and install the required packages. (<a href="https://www.tecmint.com/install-kvm-on-ubuntu/">ref</a>) <br>
      ```sudo apt install qemu qemu-kvm qemu-system qemu-utils``` <br>
      ```sudo apt install libvirt-clients libvirt-daemon-system virtinst``` <br>
19. Launch Virtual Machine Manager using ```virt-manager``` command, and inside the host, create a new VM. (as a prerequisite, download the iso file or guest VM). <br>
20. Install Guest(debian 11) OS once the VM is created and login to the nested VM. <br>
21. Install CPUID using ```sudo apt install cpuid``` if it is an Ubuntu VM. <br>
22. Install gcc in the nested VM.  <br>
32. Ran the test file form the nested VM to print the output.  <br>

<h3>Assingment 01</h3> <a href="https://github.com/ravitanti/linux/tree/master/CMPE283_Assingment_1">ref</a> <br>
<h3>Assingment 02</h3> <a href="https://github.com/ravitanti/linux/tree/master/CMPE283_Assingment_2">ref</a> <br>
<h3>Assingment 03</h3> <a href="dem">ref</a> <br>


