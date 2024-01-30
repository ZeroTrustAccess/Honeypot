# Azure Honeypot Project 2024

This project involves setting up a honeypot on Microsoft Azure and exposing it to the internet to monitor and analyze potential cyber threats. The goal is to gain insights into the types of attacks that a system may face and use this knowledge to improve system security.

## Project Objectives

- Set up a honeypot on Microsoft Azure.
- Expose the honeypot to the internet.
- Monitor and document any attempted attacks.
- Analyze the data collected by the honeypot.

## High-Level Overview of the Lab
 1. Create a **free Azure account** (which has about $200 in free  credits)
 2. Set up a **Virtual Machine** in Azure.
 3. Turn the external firewall and Windows Firewal off for the VM, exposing it to anyone on the internet to ping and attack.
 4. Create a **Log Repository in Azure** called a **Logs Analystics Workspace**, to ingest the logs from the Virtual Machine.
 5. Set up **Azure Sentinel** with Azure. (Microsoft's cloud-native SIEM)
 6. With that **SIEM**, create a map so that we can see all of the **attacker data**.
 7. Use **Powershell** to extract the IP addresses from the Windows Logs, and send it to a Third Party API, to derive all of the geographic location to be sent back to the Virtual Machine to create a **custom log** of data so we know where these attacks are coming from.

## Getting Started

These instructions will guide you on how to set up the honeypot on your own Azure account.

### Prerequisites

- An active Microsoft Azure account.
- Basic knowledge of cybersecurity principles.

### Setup and Installation

1. [Step 1: Create a Virtual Machine](https://github.com/ZeroTrustAccess/Honeypot/blob/main/Step1_VM.md)
2. [Step 2: Create a Logs Analytics Workspace](https://github.com/ZeroTrustAccess/Honeypot/blob/main/Step2_LAW.md)
3. [Step 3: Set up SIEM - Microsoft Sentinel](https://github.com/ZeroTrustAccess/Honeypot/blob/main/Step3_Sent.md)
4. [Step 4: Journey Into The Machine](https://github.com/ZeroTrustAccess/Honeypot/blob/main/Step4_Run.md)
5. [Step 5: logs, logs, logs](https://github.com/ZeroTrustAccess/Honeypot/blob/main/Step5_Log.md)
6. 
   ...

## Usage

Explain how to use the honeypot once it's set up.


## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

This project is directly inspired from Josh Madakor's YouTube Channel.
