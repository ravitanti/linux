<h1>CMPE 283 Assignments - 02</h1>
<h3>By Ravi Kumar Tanti and Saurabh Ramesh Warathe</h3>

<h2>Assignment-01</h2>

<h3>Work done by Ravi (015267200):</h3>
I worked with Saurabh for this assignment. On my machine, I began setting up the environment for assignment 02. I started building the kernel and encountered which i solved by installing all the dependencies. Then I edited the cpuid.c and added if..else condition in the kvm_emulate_cpuid block code. I encountered the error of undefined variable when I use U32 therefore I reinitialized it by using atomic variables After Saurabh committed the changes he made to vmx.c, I rebuilt the kernel and committed it to the GitHub repo inside /arch/x86/kvm after a successful built. I also installed KVM on the hypervisor so that a guest VM can be created and test script can be executed on that.



<h3>Steps followed:</h3>
1. Made Clone of linux source code and cloned it on local system. <br>
2. Update the files arch/x86/kvm/vmx/vmx.c and arch/x86/kvm/cpuid.c <br>
3. Install all the dependencies required for build. <br>
4. Rebuild the kernel using make modules command and make INSTALL_MOD_STRIP=1 modules_install && make install. <br>
5. Run lsmod | grep kvm to check if the kvm modules are preloaded. <br>
6. If they are already present remove them using rmmod kvm and rmmod kvm_intel commands. <br>
7. Run modprobe kvm and modprobe kvm_intel commands to reload edited kvm modules. <br>
8. Run the commands listed below from the host terminal in order to enable the kvm module in the host and install the required packages. <br>
      sudo apt install qemu qemu-kvm qemu-system qemu-utils <br>
      sudo apt install libvirt-clients libvirt-daemon-system virtinst <br>
9. Launch Virtual Machine Manager using virt-manager command, and inside the host, create a new VM. (as a prerequisite, download the iso file or guest VM). <br>
10. Install Guest(debian 11) OS once the VM is created and login to the nested VM. <br>
11. Install CPUID using sudo apt install cpuid if it is an Ubuntu VM. <br>
12. Install gcc in the nested VM.  <br>
12. Ran the test file form the nested VM to print the output.  <br>
