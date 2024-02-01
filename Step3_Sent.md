# Chapter 3: The Watching Watcher - Sentinel

I searched for "sentinel" in the search bar at the top, and chose **Microsoft Sentinel** under *Services*.

![screenshot of searching for sentinel](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step3_sen1.png)

This is the **SIEM** (Security Information and Event Management) tool, that I used to visualize the attack data.

First step of course was to click **Create Microsoft Sentinel**.

![screenshot of sentenal screen](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step3_sen2.png)

On the first screen, all I had to do was choose the LAW I created previously, and then choose add at the bottom.

![screenshot of sentenal link to law](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step3_sen3.png)

## While the SIEM sets up...

None of these processess are instantaneous, and so while I waited for **Sentinel** to set up, I went back to the **Virtual Machine**.

![screenshot of going back to vm](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step3_sen4.png)

Now that the **VM** is set up, I want to copy the **Public IP address** and log into it with **Remote Desktop**.

![screenshot of copying IP in VM](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step3_sen5.png)

To do this, I had to click the search bar on my own computer and search for "Remote desktop", to find the app.

![screenshot of going to remote desktop](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step3_sen6.png)

When the Remote Desktop screen came up, I pasted the IP into box, then chose to login with another user.

![screenshot of going to remote desktop](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step3_sen7.png)

And then accepted the certificate warning.

![screenshot of certificate warning](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step3_sen8.png)

And boom!

![screenshot of vm](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step3_sen9.png)

From here, it was time to some work in the [virtual machine](https://github.com/ZeroTrustAccess/Honeypot/blob/main/Step4_Run.md)


