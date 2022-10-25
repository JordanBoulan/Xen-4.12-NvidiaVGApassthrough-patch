UPDATE: You can use LibVMI with Xen (KVM event support does not yet exist) to capture CPUID event/VM Exits and return the CPUID of your chooosing at runtime in the callback, - without compiling xen or seabios youself yourself. You can look at the example in the LibVMI repo. This will incur a small performance overhead. Manual patching as shown in this repo may have a slight performance advantage in the unlikely case that your VM calls CPUID constantly.<br/>

You can use this as an example to patch newer versions of xen, but the patch and exact locations in files will need updating.<br/><br/>

EDIT: In Reference to the issue posted, make sure you don't have spoof and viridian enabled at the same time.<br/><br/>

apt build-dep xen<br/>
apt build-dep qemu<br/>
git clone https://github.com/xen-project/xen.git<br/>
patch -p1 < xen.patch<br/>
<br/>
This also requires a tiny one-line patch to SeaBios to detect the new hypervisor string.
<br/>
Add<br/>

 if (strcmp(signature, "XenVMMXenVMM") == 0 || strcmp(signature, "ZenZenZenZen" == 0))<br/>
	
at line 72 of xen.c removing<br/>

 if (strcmp(signature, "XenVMMXenVMM") == 0)<br/>

Follow instructions on both githubs for general building and installation instructions. <br/>
