# Step 1: Setup

1. Set up a **Virtual Machine**. Look for **Create a resource**, and then find Virtual Machine, and click Virtual Machine. You can also find the Virtual Machine icon from the Home screen, enter it, and then choose **create** in the top left of the menu bar.

![Screenshot of where to set up the VM](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step1_vm1.png)

There are a variety of ways to get to the same destination. Choose to set up a **Virtual Machine hosted on Azure**.

![Screenshot of alternate way to set up VM](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step1_vm2.png)

This will bring you to the **Create a Virtual Machine** page. 
- Next, where it says **Resource Group**, click **create new** and name it something relevant to your project. This allows us to manage our cloud resources as a group instead of individually. For this project, I just called mine *HoneyPot*. 

![Screenshot of resource group set-up](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step1_vm3.png)

- Then give the VM a name: unoriginally, I chose HoneyPotVM.
- Leave the default values that auto-populate when you the **image**. For this lab, I'm using **Windows 10 Pro, Version 22H2-64 Gen2 (free services eligible)**
- Next, we must create the **Administrator Account**.
Just choose something that you'll remember, because this is the information we'll need to log into the **Virtual Machine** later.

- At the bottom left, check the box to confirm licensing.
- Then move on to the next section located at the bottom labled **Next: Disks>**
![Screenshot of skipping Disk Section set-up](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step1_vm4.png)
- Bypass the **Disks** page and move onto **Networking**.

On the **Networking** page, look for the section called **NIC network security group**.
![Screenshot of network page set-up](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step1_vm5.png)
- *This* is like the **Firewall** for the **Virtual Machine**. Let's set this to *Advanced*.
- Directly underneath that, we're going to create a new network security group in **Configure network security group**.
