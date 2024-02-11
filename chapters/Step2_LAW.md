# Chapter 2: Laying Down the LAW (Logs Analytics Workspace)

The purpose of this is to ingest the logs from the **VM** I created in Step1, to create my own **custom log** that displays the geographic location of the attackers.
- I searched "log" in the search bar at the top to find the link to create my **Logs Analytics Workspace** (which I will refer to as LAW)

![Screenshot of searching for log in Azure](https://github.com/ZeroTrustAccess/Honeypot/blob/main/all_images/step2_law1.png)

After clicking the *Create analytics workspace* button, on the next screen I only made two adjustments.
- Under Resource group, I chose the Resource Group I created when I creaeted the VM.
- Then I created a name for the LAW, cleverly named law-honepot.

![Screenshot of searching for log in Azure](https://github.com/ZeroTrustAccess/Honeypot/blob/main/all_images/step2_law2.png)

After clicking create and validate, I had to click create again once it was validated to actually deploy the LAW.

Next,  we need to access the Azure security center. The importance of this is to enable the ability to gather logs from the **VM**. \

*Note*
In the intial lab from Josh Madakor which I used to guide me through this project, the set-up was a little different. Microsoft has since adjust and updated their Azure platform, and so if anyone else were to follow the same tutorial, they would be confused (as I was first) to find that there was no *Security Center* you could choose from in the search bar at the top.

Instead, by typing "security center" in the search bar at the top, there is a new option below under "Marketplace" called **Azure Security Center**.

![Screenshot of searching for security center in Azure](https://github.com/ZeroTrustAccess/Honeypot/blob/main/all_images/step2_law2.5.png)

This opens up another screen that's tied to the free Azure subscription. To proceed, I just had to click the **Open Defender for Cloud** button at the bottom left of the screen. This finally brought me to the new revamped security center.

![Screenshot of defender for cloud in Azure](https://github.com/ZeroTrustAccess/Honeypot/blob/main/all_images/step2_law3.png)

From there, the next step was to find the **Environment Settings** located in the bottom of the left toolbar.

![Screenshot of finding environment settings in defender cloud in Azure](https://github.com/ZeroTrustAccess/Honeypot/blob/main/all_images/step2_law4.png)

- On this screen, I clicked the dropdown arrow next to my Azure subscription, which revealed **law-honeypot**, the LAW I just created. I then clicked that.

![Screenshot of finding environment settings in defender cloud in Azure](https://github.com/ZeroTrustAccess/Honeypot/blob/main/all_images/step2_law5.png)

- On this screen, I only enabled 2 of the 3 options. I turned on **Foundational CPSM** and **Servers**, but left the SQL Servers on Machines off, because I didn't need to do anything with SQL Servers for this lab.

![Screenshot of defender settings in Azure](https://github.com/ZeroTrustAccess/Honeypot/blob/main/all_images/step2_law6.png)

I saved my choices by clicking the "floppy disk" save icon at the top of the screen, and then moved on to the **Data Collections** section, in the left menu.

![Screenshot of finding save and data collection settings in defender cloud in Azure](https://github.com/ZeroTrustAccess/Honeypot/blob/main/all_images/step2_law7.png)

In the **Data Collections** section, I just chose to collect **All Events** and then saved.

![Screenshot of finding save and data collection settings in defender cloud in Azure](https://github.com/ZeroTrustAccess/Honeypot/blob/main/all_images/step2_law8.png)

The Next step was to go back to **Logs Analystics Workspace** (LAW), and connect it to the **Virtual Machine** (VM).

Back at the **LAW**, I clicked "law-honeypot" (which was the LAW I created) 

![Screenshot of connection law to vm](https://github.com/ZeroTrustAccess/Honeypot/blob/main/all_images/step2_law9.png)

and that opened up another menu on the side. From there I had to scroll down a little, and choose **Virtual Machines (depreciated)** under the section labeled **Classic**.

![Screenshot of connecting law to vm in Azure](https://github.com/ZeroTrustAccess/Honeypot/blob/main/all_images/step2_law10.png)

This showed the VM which I created earlier. I clicked that, then clicked **Connect** on the left side.

![Screenshot of connecting law to vm in Azure](https://github.com/ZeroTrustAccess/Honeypot/blob/main/all_images/step2_law11.png)

![Screenshot of connecting law to vm in Azure](https://github.com/ZeroTrustAccess/Honeypot/blob/main/all_images/step2_law12.png)

From here, it was time to set up my **SIEM**, [Microsoft Sentinel](https://github.com/ZeroTrustAccess/Honepot/blob/main/chapter/Step3_Sent.md).
