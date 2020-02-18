apt install build-dep xen<br/>
apt install build-dep qemu<br/>
git clone https://github.com/xen-project/xen.git<br/>
patch -p1 < xen.patch<br/>
<br/>
This also requires a patch to SeaBios to detect the new hypervisor string.
<br/>
Add<br/>

 if (strcmp(signature, "XenVMMXenVMM") == 0 || strcmp(signature, "ZenZenZenZen" == 0))<br/>
	
at line 72 of xen.c removing<br/>

 if (strcmp(signature, "XenVMMXenVMM") == 0)<br/>

Follow instructions on both githubs for general building and installation instructions. <br/>
