Uhoh! I forgot what the Root password on the ProxMox GNU/Linux VM. Gotta fix that first.

**Fix (Boot into Single-User Mode to Reset Root Password)** 
  1.	Reboot the ProxMox machine.
  2.	At the GRUB menu, press e to edit the boot entry.
  3.	Find the line that starts with linux — go to the end of that line and append:
    > init=/bin/bash
  4.	Press Ctrl+X or F10 to boot with this setting.

This will drop you into a root shell without needing a password. Then do this:
  1.	Remount the root filesystem as read/write:
    > mount -o remount,rw /
  2.	Set a new root password:
    > passwd
  3.	Reboot the system:
    > exec /sbin/init



    
 
Why Start with a Domain Controller? A Domain Controller is the core of a Windows domain environment. It manages:
  
  - Centralized authentication (via Active Directory)
  - User and computer accounts
  - Group policies (GPOs)
  - Authorization and access control
   
**Benefits of Having a Dedicated Domain Controller** 
  - Centralized User Management	All accounts are managed via AD — no need to set up users on each VM
  -	Group Policy Control Push security, updates, software, and login rules across all domain-joined machines
  -	Simulates Enterprise Environments	Practice joining machines to a domain, delegating permissions, and running AD-integrated services
  -	Better Lab Scalability	Makes it easier to add file servers, DNS, WSUS, print servers, etc., later
  -	Foundation for Real-World Roles	Essential for roles like System Admin, SOC analyst, Threat Hunter, etc.
 
**Network Overview:** 
  -	Domain Controller (LAB-DC-01) — 10.0.0.10
  -	File Server (optional) — 10.0.0.11
  -	Workstations for Users — 10.0.0.20–10.0.0.30 range
  -	Switch/Router — implied, all devices on same subnet 10.0.0.0/24

<img width="609" height="241" alt="image" src="https://github.com/user-attachments/assets/c021a298-fb15-466d-86fb-c5a73f81630b" />

**Diagram**
 
                                +--------------------------------+
                                |           LAB-DC-01            |
                                |      (Domain Controller)       |
                                |           10.0.0.10            |
                                +---------------+----------------+
                                                |
                                         [Network Switch]
                                                |
               -------------------------------------------------------------------------
              |                     |                         |                         |             
            PETER                 MICHAEL                   SAMIR                      BILL    
             PC                     PC                        PC                        PC         
          10.0.0.20              10.0.0.21                 10.0.0.22                 10.0.0.23 
