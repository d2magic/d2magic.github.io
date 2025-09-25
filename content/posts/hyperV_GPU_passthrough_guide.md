+++
date = '2025-09-25T10:24:15+08:00'
draft = false
title = 'Hyper-V GPU Passthrough Guide'
Categories = ["D2r Tools"]
Tags =["D2r Bot","DB Bot" ,"GID Bot"]
+++
## Hyper-V Manager Virtual Machine & GPU Passthrough Guide

This guide will assume you already have Hyper-V installed. See [**this guide here**](https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v) to learn how. Please note you can still [**enable this on windows home edition**](https://www.xda-developers.com/how-to-install-hyper-v-windows-11-home/#:~:text=Open the Settings app and,may have to restart afterwards.).

Install Hyper-V

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250829556.png)

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250831776.png)

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250830487.png)

You will need to have virtualization enabled in your BIOS. [**Click Here**](https://support.microsoft.com/en-us/windows/enable-virtualization-on-windows-11-pcs-c5578302-6e43-4b4b-a449-8ced115f58e1) to learn how.

**60gb of free space is required**

NOTE: AMD CPU laptops with integrated graphics & a dedicated Nvidia card may have issues. You may need to disable your integrated graphics for passthrough to work.

Check by opening task manager clicking the performance tab & then CPU. Look for *Virtualization: Enabled*

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250832342.png)

 

### 1. Open Hyper-V manager & create a new virtual machine

Open Hyper-V manager

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250833944.png)

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250834646.png)

Name your virtual machine. It is recommended you change the location the VM is stored.

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250835513.png)

Select Generation 2

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250836821.png)

Uncheck dynamic memory & allocate a sufficient amount of memory to the VM. Recommended 4gb-6gb

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250836482.png)

Select Default Switch

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250837167.png)

Set your disk size to at least 60gb and ensure the .vhdx file is saved in the same location as the VM.

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250841094.png)

Select a windows .iso for the VM to use. You need to use windows version 2004 for this to work. Windows 2004 is used specifically in this case and a ISO can be found [**HERE**](https://archive.org/details/windows-2004).

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250841037.png)

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250844798.png)

Select Finish

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250844791.png)

### 2. Open hyper-V manager select the newly created VM & then click settings.

Open Hyper-V  settings for dbbot (VM Name)

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250848343.png)

Assign a proper amount of cores. 2-6 recommended

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250927025.png)

Ensure that Enable checkpoints is **UNCHECKED**

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250851193.png)

Ensure Secure boot is **UNCHECKED**

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250851491.png)

Go back to Hyper-v manager & right click the newly created VM. Select **START**. Double click the VM to connect to it.

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250928993.png)

You should now see a screen like this. Press ANY key as fast as you can.
If you see Start PXE over IPv4 you NEED to restart the VM & press a key before this shows up.

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250928696.png)

Begin installing windows. 

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250930724.png)

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250929828.png)

Once windows is installed TURN OFF the VM.

 

### 3. Right click & open PowerShell ISE as Administrator.

Once open in the lower blue area type set-executionpolicy unrestricted
Hit enter & then click yes to all

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250932958.png)

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250933734.png)

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250933000.png)

Download **[GPUDrivers.zip](http://cnlinux.synology.me:5000/sharing/FKiJYgMoo)** & extract them in the same folder as your VM files.
Now goto File -> open then open the Update-VMGpuPartitionDriver.ps1 file.

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250955214.png)

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250943613.png)

Change VMName to the name of your VM. Leave GPU as AUTO

Click Run or hit F5 on your keyboard. The program should run successfully as shown here. Once this is done you have copied over your drivers to the VM.

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509250955256.png)

Now we want to enable passthrough. 

Now goto File -> open then open the VMGpuPartitionDriver.ps1 file. Click Run or hit F5 on your keyboard

Remember to change the name of your VM.

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509251002626.png)

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509251002806.png)



Start your VM and ensure passthrough worked by opening the device manger then expanding the display tab. You should now see your video card listed in the devices.

![](https://raw.githubusercontent.com/cnlinuxcode/typora/master/202509251006854.png)

## Good luck!

------
{{< quote "#e6ffe6" "#004d00" "#008000" >}}
<p> D2r Bot for sale at <a href="https://d2bin.com" target="_blank" > https://www.d2bin.com/ </a></p>
<p>Buy cheap D2r Itmes at <a href="https://d2mule.com" target="_blank"> https://www.d2mule.com/ </a>(Discount Coupon Code: d2mule) </p>

<p> Join our Discord Server:<a href="https://discord.gg/3kaNAgdxgf" target="_blank"> https://discord.gg/3kaNAgdxgf </a></p>
<p> Lowest price promise – if you find it cheaper, we’ll match it!</p>
{{< /quote >}}
