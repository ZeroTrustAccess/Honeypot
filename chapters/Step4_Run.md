# Step 4: Journey into the Machine

Inside the VM, the first thing I did was went to the search bar at the bottom of the screen, to find and open the **Event Viewer**.

![screenshot of vm screen](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step4_run1.png)

Once the Even Viewer was open, on the menu bar on the left I clicked **Windows Logs** and from that dropdown chose **Security**.

![screenshot of event viewer on vm](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step4_run2.png)

These are the events of my VM. The first thing that I want to take a look at (after adjusting the window sizes and doing a bit of organzing by name) is the logs with the **Event ID 4625** which is from my original attempt to log in to the VM, and I incorrectly typed the password. This *Audit Failure* is actually showing the login failure attempt.

![screenshot of event viewer on vm](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step4_run3.png)

This is particularly interesting to me because this is going to the sort of thing I'll be looking for in the logs once the VM becomes more discoverable, and people start actually attacking the machine.

On this screenshot you can see 3 distinct things:
1. This here is the username that I or the malicious actor used/would use to try and login to the VM.
2. This here (which I have censored) shows the name of the workstation from which the failed login attempt came from. In this instance it was from me.
3. And here, shows my IP address. This is also where I'll be finding the attacker's IP addresses from.

![screenshot of event viewer on vm](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step4_run4.png)

The log doesn't divulge any information other than the IP address, but programically using Powershell and the website **ipgeolocation.io**, where the IP address will be posted to the API, and it will then display more detailed information as far as location that we can use!

From there, I will use this data gathered from ipgeolocation.io to create my own **custom log** which I will then send to the **Logs Analytics Workspace**. 
Then, I will use **Sentinel** to read the lattitude and longitude from the data and plot on a map the locations of the attackers. 

I will need to disable the firewall for the virtual machine so that it will be discoverable to attackers on the internet, and I started this process by going back to the **Start Menu** on my actual computer (not the VM) and opening up the command prompt. (if you don't know how to do this, just type "cmd" in the search box)

In the command prompt, I want to ping the IP address of the VM. I will then follow up this command with -t, because in this instance, -t after pinging an IP address just specifies that the ping should continue sending **echo request** messages until interuptted. This is known as a continuous ping. It can be stopped by pressing **CTRL C** in the command prompt.

![screenshot of command prompt](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step4_run5.png)

From here, it's evident that immediately several time out requests happen.

![screenshot of command prompt](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step4_run6.png)

From here I'm going to go back into the VM, and do something incredibly dangerous. But it's okay because it's a VM.

In the search bar at the bottom, I'm going to type "wf.msc" This is so I can disable the Firewall to the VM, and open it up to attack.

![screenshot of command prompt](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step4_run7.png)

In the screenshot you'll see, I first when to the **Windows Defender Firewall Properties**, and then selected to turn the **Firewall state** to off, on the **Public Profile!

![screenshot of command prompt](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step4_run10.png)

Once this was done, my echo request from my ping on my acutal machine started to display data and no longer showed timeout requests, meaning it worked!

![screenshot of command prompt](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step4_run9.png)

Now, I need to download a **Powershell Script**, from a github link. 
- I had to open **Edge** on **the VM**, and went to the following link: https://github.com/joshmadakor1/Sentinel-Lab/blob/main/Custom_Security_Log_Exporter.ps1
- This is the Custom Security Log Exporter script from Josh Madakor that I will use to send the logs.

  ## IMPORTANT TO NOTE
  If you intend to follow along and do this lab, you must pay attention to do the things in the VM that you mean to in the VM, and not on your actual machine. This would be catastrophic.

On the VM, I went to think link, and then highlighted the script that Mr. Madakor had posted, and copied it.

![screenshot of copying script](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step4_run11.png)

Next **On the VM**, I went to the search and typed "powershell ise" and opened Powershell ISE.
![screenshot of accessing powershell ise](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step4_run12.png)

Once open, I clicked **new** and then pasted the script.

![screenshot of new script](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step4_run13.png)

Then I saved it to the desktop of the VM as log_exporter.

![screenshot of saving new script](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step4_run14.png)

To make this Script work, and filter the logs for me using the ipgeoloctation.io site, I needed to first get the **API KEY** from the VM, to copy and paste into Line 2 of the script.

![screenshot of script api key line 2](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step4_run15.png)

To do this, I had to head to the website ipgeolocation.io *within* the VM.

![screenshot of ipgeolocatin site](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step4_run16.png)

I then had to sign up for an account with ipgeolocation.io. I found it easiest to just sign up with my google account. Once that was created, I got my API key by clicking on Dashboard, and then copying the key that was right at top of the dashboard.

What this script does, is it goes into the Event Viewer and retrieves all of the *Failed Audit* logs, grabs the IP addresses, then gets the geolocation data from the io website, and converts it into a new log.

This log will then be created in the file path listed just below that. It will then create the log file with some sample geolocations that I will use to train the **LAW**.

![screenshot of powershell](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step4_run17.png)

To see the log file, all I had to do was open the file explorer, head over to C:, and View the Hidden Files, because the ProgramData folder was a hidden folder.

![screenshot file explorer](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step4_run18.png)

- Next, I had to create a custom log within **LAW**. In Azure, I navigated back to the Logs Analytics Workspace, then:
  1. choose my honeypot
  2. From the menu on the left, I selected *Tables*
  3. Then *Create*
  4. Then chose to create **MMA-Based** custom log.
 
![screenshot of custom log creation](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step_run19.png)

The first thing the custom log asks for is a sample log. To get that, I went back into the VM, went to the location where the failed attempts were being logged (C:/Program Data) and opened the log in notepad by double clicking it. Once it was open, I selected the contents of the log by using **Ctrl+A** then copying it with **Ctrl+C**, and then minimized the VM to go back to actual computer.

![screenshot of collecting sample log](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step4_run20.png)

I opened *Notepad* on my actual computer, pasted the contents of my VM log file in with **Ctrl+V**, and then saved the file as "failed rdp log" on my desktop.

![screenshot of log on actual desktop](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step4_run21.png)

I then went back to the **LAW** custom log page I had open and retrieved the failed rdp log file from my desktop to use as the sample lot.

![screenshot of uploading log](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step4_run22.png)

After uploading the sample log, on the next page it shows some of what it looks like. So I then clicked *Next*.

![screenshop of uploaded log](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step4_run23.png)

The next page is for the *Collection path*. This is where the log actually lived on the VM. The dropdown box on the left side I chose Windows, and then entered the path on the VM that the log was located. Which was **C:\ProgramData\failed_rdp.log**

![screenshot of collection path](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step4_run24.png)

On the next section titled **Details**, I named the custom log **FAILED_RDP_WITH_GEO** (and it will gramatically append at the end with _CL which just stands for *custom log*. Then moved on to Review + Create.

![screenshot of naming the custom log](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step4_run25.png)

It will take some time for the log file to sync-up with the Virtual Machine. On to the [Next Step](https://github.com/ZeroTrustAccess/honeypot/blob/main/Step5_Log.md)




