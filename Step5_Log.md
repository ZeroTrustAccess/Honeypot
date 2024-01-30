# Step 5: Logs, Logs, Logs.

Within the left menu in the **Logs Analytics Workspace**, I clicked *Logs*, and after closing the pop-up query window, at the top of the window on the right next to the number 1, I started to type "SecurityEvent". This will alow me to view the Security Event logs over on the VM, which is also how I will view the custom logs I created.

![screenshot of security events log](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step5_log1.png)

After choosing SecurityEvents, I clicked the blue Run button above, and after the lower window began populating, there were two tabs: Results and Charts. Clicking on Results showed me the contents of the Security Events log from my virtual machine.

![screenshot of the log](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step5_log2.png)

Next to SecurityEvent, if I typed a pipe | then "where EventID == 4625" and then clicked run, it would show mw all the failed login attempts that are being logged in the VM by that EventID in the last 24 hours. (The screenshot was taken on a later date from my original set-up and therefore didn't contain any actual logs of my failed login attempts.)

![screenshot of eventid 4625](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step5_log3.png)

## It was at this point...

One of the biggest things I have struggled with in this project is the *reorganization* that Microsoft Azure has undergone since the initial tutorials I found online, and any videos I have been following along with. It was at **this point** where I hit a major issue when it came to the continuation of this project.

In Josh Madakor, and others' SIEM tutorial's using Azure, this would be the point where I am supposed to take the log results that I'm receiving from the VM in the query, and extract the different bits of data to make the entire log easier to read and digest. The *old way* in which this was done was fairly straight-forward yet tedious. Within the query you could right-click the log and choose **extract** and actually use a **Field Extraction Wizard** to sort-of guide you through the process of extracting the data from these logs and creating new columns within the log as it was coming, to make everything easier to read.

Despite all of my searching online, I was unable to find any other videos of anyone doing this successfully with the latest version of Azure in 2024. So, I did what I do best, and just buckled up and starting digging to try and figure it out.

## Mistake of the MMA-Based Log

In an earlier step, I documented how I created the custom log in the first place, according to Josh Madakor's instructions, and when I came upon a key difference in the **Custom log creation** process, I had found that Microsoft had updated Azure, and had done away with the old way of custom logging. Instead of just following along and creating a custom log, like the video, I was met with the choice. Create a **DCR-Based** or **MMA-Based** log.

At first, I chose the first option (DCR), but the input field's on the screen didn't match the tutorial I was following, so I backed-out and chose MMA instead. This matched, visually, to what I was seeing on screen and so I jsut continued to push forward. However, at the point where I actually needed to extract data from the logs, Microsoft had apparently discontinued the ability to in March of 2023. This meant, there was no way that I was able to use the MMA-Based log that I had created (at least to my knowledge) and do what I needed to do.

I spent a lot of time swimming through the menus and exploring the differnet sections in the Logs Analytics Workspace, and finally came upon a hint in the *Tables* section. After opening it, there was a huge list of analytics that were already defaultly apart of Azure, and when I scrolled down the list a bit, I was able to find the custom MMA log I created earlier.

![screenshot of analytics](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step5_log5.png)

To the right side, I found the three dots, which always opened up to some sort of optinos or settings, and found a few new paths to go down.

![image](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step5_log6.png)

I first chose **Manage Table**, seeing as though it had the cogwheel icon, and I was trying to find a way to alter the custom log that I had created. But after exploring through, I found nothing that seemed even remotely useful for what I needed to do. But when I went into the option **Edit Schema**, I thought I had found the answer.

![screenshot of edit schema](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step5_log7.png)

Here I found options to create custom columns within the custom log that I had created! But... no matter what I tried, the Save button at the button remained grayed-out. I did some more digging and after some long confusing conversations with Co-Pilot, I went back into the manage table section of my log, and clicked to remove the default workspace settings for the custom log.

![image](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step5_log8.png)

This, accidentally, allowed me to actually save the changes I had made in the **edit Schema** menu for my custom log. Finally, I was able to "add more columns" to my custom log. I thought that this would be the solution to my issue, and continued to try to extract and redirect the "lattitude" information from the log into it's own column.

Yet, despite trying everything I could think of, it just didn't work. Every time I ran the query, the log would come up, and *indeed* there would be a new column that I had created, but it was blank. Nothing I could do seemed to make the actual latitude data move from the **RawData** column, to my new column.

I went back to Bing, and back to digging through whatever was available on the Azure site, because my google searches had proved to be fruitless. Apparently, everything was moving toward the DCR-Based logs, since there was a newer and better way to incorporate and display the information within the logs.

Problem was, I had no idea what any of that meant, and I had already been working on this project for several weeks at this point, on the weekends, and my time to use my remaining credit within Azure was running out. So, after doing some more reading through the tutorial pages on Azure, and searching through some youtube videos, I came upon **KQL**.

## KQL - Kusto to the rescue.

I had no idea what KQL was. But, it looked similar to the SQL that I had been using in the **Google Cybersecurity Professional** certificate training I had done. And after some playing around and some reading, I saw that you could use KQL syntax just like SQL or a programming language, in the query where I was calling up my logs, to sort-of "customize them" as they were generated.

I could see this was a more evolved form of extraction, but still had no idea what the hell I was doing. So back to Bing, and I started painstakingly contstructing my KQL syntax to make my logs actually appear the way that I wanted them to.

Apparently there were two ways to do what I needed to do, through KQL commands called **parsing** and **extending**. I had no idea how to use either of these, but with AI and the power of Co-Pilot to answer my questions as I went, I started small.

Apparently:
1. **Parse**: The parse operator is used to evaluate a string expression and parse its value into one or more calculated columns. Here’s an example of how to use it:
    | parse [ kind= kind [ flags= regexFlags ]] expression with [ * ] stringConstant columnName [: columnType] [ * ] , ...

In this example, parse is used to search for a stringConstant within an expression and assign the value to a columnName.

2. **Extend**: The extend operator is used to create calculated columns and append them to the result set1. Here’s an example of how to use it:
StormEvents | project EndTime, StartTime | extend Duration = EndTime - StartTime

In this example, extend is used to create a new column called Duration, which is the difference between EndTime and StartTime.

This only confused me. So with only the one data point to focus on--**latitude**-- I was able to come up with an expression using the **extend** operator:

![screenshot of first kql syntax](https://github.com/ZeroTrustAccess/Honeypot/blob/main/step5_log9.png)

Admittedly, I had no idea what any of this was. I had to really break down into chunks, and ask Co-Pilot a million questions to get anywhere.
Obviously, the **FAILED_RDP_WITH_GEO_CL** was the query command I used to summon the log in the first place. The next part made a little bit of sense to me. I knew that the | symbol was called a "pipe", and was used in other languages to *do more than one thing* at the same time. I experienced this in both my SQL training with Google, and all of the self-study I did to try and learn HTML,CSS, C+, and Python.

It made sense, then, that following my input to call my logs through the query, would be the beginning of setting the extend operator into motion.
