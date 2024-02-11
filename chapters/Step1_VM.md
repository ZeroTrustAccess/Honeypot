# Chapter 1: Virtual Machine Creation Story

1. The **First Thing** I needed to do was set up a **Virtual Machine**. I found **Create a resource**, and then Virtual Machine, on my Azure account home screen, and clicked Virtual Machine. Its also possible to find the Virtual Machine icon in other places from the Home screen, enter it, and then choose **create** in the top left of the menu bar.

![Screenshot of where to set up the VM](https://github.com/ZeroTrustAccess/Honeypot/blob/main/all_images/step1_vm1.png)

There are a variety of ways to get to the same destination. I chose to set up a **Virtual Machine hosted on Azure**.

![Screenshot of alternate way to set up VM](https://github.com/ZeroTrustAccess/Honeypot/blob/main/all_images/step1_vm2.png)

This will bring you to the **Create a Virtual Machine** page. 
- Next, where it said **Resource Group**, I clicked **create new** and named it something relevant to the project. This allowed me to manage the cloud resources as a group instead of individually. For this project, I just called mine *HoneyPot*. 

![Screenshot of resource group set-up](https://github.com/ZeroTrustAccess/Honeypot/blob/main/all_images/step1_vm3.png)

- Then I gave the VM a name: unoriginally, I chose HoneyPotVM.
- I left the default values that auto-populate when you choose the **image**. For this lab, I'm using **Windows 10 Pro, Version 22H2-64 Gen2 (free services eligible)**
- Next, I created the **Administrator Account**.
I just chose something that I would remember, because this is the information I'll need to log into the **Virtual Machine** later.

- At the bottom left, I checked the box to confirm licensing.
- I moved on to the next section located at the bottom labled **Next: Disks>**
![Screenshot of skipping Disk Section set-up](https://github.com/ZeroTrustAccess/Honeypot/blob/main/all_images/step1_vm4.png)
- Bypassing the **Disks** page, I went straight onto **Networking**.

On the **Networking** page, I found a section called **NIC network security group**.
![Screenshot of network page set-up](https://github.com/ZeroTrustAccess/Honeypot/blob/main/all_images/step1_vm5.png)
- *This* is like the **Firewall** for the **Virtual Machine**. I set this to *Advanced*.
- Directly underneath that, I needed to create a new network security group in **Configure network security group**.

There's a default rule already set when creating the **network security group**.
![Screenshot of network security group set-up](https://github.com/ZeroTrustAccess/Honeypot/blob/main/all_images/step1_vm6.png)
- I deleted that rule, and created my own custom inbound rule to allow for anything to get into the **VM**.

- In the *Destination port ranges* box, I entered an asterisk (*) for anything, and any protocol.
- I changed the **Priority** from 1000 to 100, and then gave the rule a **name**.

  The name doesn't actually matter, but I like to name things based on either proximity, or relevance in function.
  ![Screenshot of firewall configuration set-up](https://github.com/ZeroTrustAccess/Honeypot/blob/main/all_images/step1_vm7.png)
  I went with something dramatic. **DANGER-EVERYTHING_ALLOWED**.

  The idea of doing this was exciting, because before my deep-dive into technology and learning **cybersecurity**, I had no idea the possible danger that the *raw internet* could inflict. I had never done anything like this before, and always lived safely behind a firewall of sorts.
  - The next step was to **Review and Create** the **Virtual Machine**, by clicking *ok* to create the rule, and then Review and Create in the bottom left corner. This brought me to the review screen which displayed the cost of my VM.

 ![Screenshot of vm set up cost](https://github.com/ZeroTrustAccess/Honeypot/blob/main/all_images/step1_vm8.png)

 I thought this was incredibly neat. Since I had never done anything like this before, I had no idea what to expect as far as the cost. It was my understanding that the Free Azure account came with *credits*, and that the lab I was undertaking wouldn't *actually* cost me anything to do. But it was neat to see it was actually much cheaper than I had expected. (This is good for me, because while I have always considered myself a fast-learner, I've found that over the years I tend to do things more slowly and deliberately. Less error that way.)

![Screenshot of vm set-up](https://github.com/ZeroTrustAccess/Honeypot/blob/main/all_images/step1_vm9.png)

 After clicking create, my **Virtual Machine** began it's journey through *creation*. This was strangely exciting, and sort of hammered-home the feeling of being nerdy, in a sense. While the **Virtural Machine** was being deployed, it was time to move on to the next step in my lab.

 ...make a [Logs Analytics Workspace](https://github.com/ZeroTrustAccess/Honeypot/blob/main/chapters/Step2_LAW.md)
 
