# Azure-HoneyPot


## Create && Name a Resource Group

## Create && Name an Azure Virtual Machine ( VM )
- Put VMs in East US 2 ( This is for the data center location )
- Select Windows 10 Pro Image
- Default Size is fine
- Under Administrator Account
- make a username && password ( To log in VM )
- Selected Inbound ports should be RDP ( 3389 )
- Skip Disk setup ( Go next to Networking )
- For NIC Network Security Group Select Advanced ( This is like our Firewall )
- Then for Configure Network Security Group ( Create a new one )
- Remove default rule
- Create our own inbound rule ( Add an inbound rule )
- Destination port ranges put a star ( * ) for anything
- Protocol select Any
- Action Allow
- Priority make it low like 100
- Name doesn't matter just name it ( DANGER_ANY_INBOUND )
- then add rule then ok ( This will allow all traffic from the internet into our virtual machine )
- REVIEW + CREATE
- AFTER VALIDATION PASSES CLICK CREATE

## Next make a log analytics workspaces next ( to ingest logs from the virtual machine )
- This will ingest the windows event logs && 
- we will create our own custom log that contains geographic information so we can discover wher ethe attackers are coming from
- Our SIEM will connect to this log analytics workspace to display that data

## Log Analytics 
- cretae workspaces
- assign to to the resource group
- put in same region as vm
- REVIEW + CREATE 
- AFTER VALIDATION PASSES CLICK CREATE

- After go to Security center to enable the ability to gather logs from the virtual machine innto the log analytics workspaces
- Once in security center on the left go to pricing and settings and click the log analytics workspaces we just created
- Then tun Azure defender on here and turn SQL servers off because we dont need to do anything with them
- THEN SAVE IT
- On the left select data collection and select ALL EVENTS AND SAVE
- then go back to log analytics workspaces and connect it to the virtual machine

## Connect virtual machine
- Click connect
- On your own computer open you RDP 
- Paste the VMs IP Address in and click connect
- enter the username and password used to create the VM
- Accept the certificate warning


## Setup Azure Sentinel ( this is our SIEM we are going to use to visualize the attack )
- Create Azure Sentinel
- Select the log analytics workspace we want to connect it to 